# User API

![User API Diagram](../../assets/diagrams/user_api.png "User API Diagram")

In this section, you will find a step-by-step explanation of how each of the user API methods works under the hood. Plus some other details.

The available methods are:

- [GET /user/profile](#user-profile-steps) for getting complete information about the user calling it.
- [POST /user/update](#user-update-steps) for updating information about the user calling it.
- [POST /user/accept-terms](#user-accept-terms-steps) is used only internally when first accessing the Dashboard. Provides a legally compliant method for marking users who have accepted the TOS and PP, thereby granting them access to the Dashboard.
- [DELETE /user/delete](#user-delete-steps) is used only internally when going through the account deletion prompt in the Dashboard. Will delete ALL user data IRREVERSABLY.

See [API Documentation](../API/v1/USER.md) for more information regarding how to use the API methods discussed here.

## User Profile steps

1. The API authenticates the request using Congito and then calls a lambda function.
1. The lambda function retrieves the full user item from both the User Info Database and the Cognito User Pool, then returns it in a JSON response to the user.

## User Update steps

1. The API authenticates the request using Congito and then calls a lambda function.
1. The function first checks the data to see if it meets the requirements. If it does, it updates all the fields in the Congito User Pool that are present.

## User Accept Terms steps

1. The API authenticates the request using Congito and then calls a lambda function.
1. First, the function will retrieve all legally required information from the Cognito User Pool.
1. Then, it will store the information in an S3 Bucket with Object Lock enabled, combining any other information required from the request itself and the server.

## User Delete steps

1. The API authenticates the request using Congito and then calls a lambda function.
1. Delete the user from the Cognito User Pool.
1. Delete the Database entry from the User Info Database.
1. Delete all entries related to the user from the Job Requests Database.
1. Delete all files associated with the user from the S3 Bucket.
1. If an error occurs, send an email to the admin to complete the process manually.
