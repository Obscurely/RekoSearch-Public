# OAuth 2.0 Authentication flow for RekoSearch

<!--toc:start-->
- [Step-by-step Authentication Flow](#step-by-step-authentication-flow)
- [Additional security considerations](#additional-security-considerations)
- [QOL](#qol)
<!--toc:end-->

Authentication is done using Cognito and the OAuth 2.0 standard, the industry
standard used by the likes of Google and Facebook. The outline of how it works
is as follows:

- **Login**: First, go to the /auth/login endpoint or access any route that
  requires authentication, as you will get redirected there. This will, in turn,
  redirect you to the Cognito login page.
- **Authentication**: Log in or sign up (optionally with MFA), and you will be
  redirected back to /auth/callback with an authorization code.
- **Token Exchange and Session Management**: The front end then exchanges the
  code for tokens, validates them, and stores them securely in the session.

## Step-by-step Authentication Flow

1. You go to the /auth/login endpoint on the front end. The front end sets a
   secure state string in the session, builds the login URI for the Cognito App
   Client and redirects you to that URI.
1. On the Cognito page, you log in/sign up (with MFA). After that, you'll be
   redirected to the front end's auth/callback endpoint with an Authorization
   Code as a parameter. The code is valid for only 3 minutes (the minimum AWS
   will allow) and one attempt at using it.
1. The front end first checks the state string in the URL parameters and
   validates it to be the same as the one stored in the session (This helps
   protect against CSRF attacks). Then, it exchanges the Code for Tokens.
1. The front end validates the ID token's signature and claims against the JWT
   standards and AWS Public Keys, ensuring the tokens' authenticity and
   integrity.
1. Finally, the front end will establish a session on the server and configure a
   secure HttpOnly cookie containing the session ID.

## Additional security considerations

- Access to the API is done via the access token. This token is valid for only
  30 minutes, after which the front end will renew it using the refresh token.
  This will be seamless for the user but prevent an attacker from being able to
  do damage for a long time. The refresh token is valid for a day, after which
  the front end will renew it (now user interaction is needed, just a tiny
  hiccup)
- Strong password policy: 12 characters minimum and at least one lowercase, one
  uppercase, one number and one symbol.
- All traffic is HTTPS.
- Sessions are invalidated after seven days.
- Secure headers are set for all of the responses.

## QOL

- Rate limiting which is configured to 100 per minute per IP, which is still a
  lot, so I might tweak it down.
- Exponential backoff is configured for Redis in case there is a heavy load.
- Every route that needs authentication checks if the tokens are present and not
  expired and if they are, it redirects the user to the authentication endpoint.
