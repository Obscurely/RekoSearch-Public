# Endpoint Documentation: /user

Get, update, and delete user information

<!--toc:start-->

- [User Available](#user-available)
  - [User Profile](#user-profile) (GET /profile)
  - [User Update](#user-update) (POST /update)
- [Internally Used](#internally-used)
  - [User Accept Terms](#user-accept-terms) (POST /accept-terms)
  - [User Delete](#user-delete) (DELETE /delete)
- [Additional Resources](#additional-resources)
<!--toc:end-->

Check [API README.md](../README.md) for the BASE URL.

If you are interested in the inner workings check [Additional Resources](#additional-resources).

## User Available

### User Profile

**Description**  
Get the current user's profile information.

**URL**  
`/api/v1/user/profile`

**Method**  
`GET`

**Authentication Required**  
Yes

**Headers**

```
Authorization: {token}
```

**Successful Response**

- **Status Code**: 200 OK
- **Response Body**:

```json
{
  "user_id": "1234567890",
  "first_name": "John",
  "last_name": "Doe",
  "username": "johndoe",
  "email": "john.doe@domain.com",
  "birthdate": "1990-01-01",
  "credits": 100,
  "total_jobs": 10,
  "creation_date": "2023-01-01T12:00:00Z",
  "tos_version": "2025-04-08",
  "pp_version": "2025-04-08",
  "tos_accepted": true,
  "pp_accepted": true
}
```

**Error Responses**

| Status Code | Description  | Response Body                                    |
| ----------- | ------------ | ------------------------------------------------ |
| 401         | Unauthorized | `{"message": "Unauthorized"}`                    |
| 500         | Server Error | `{"message": "Internal server failure message"}` |

**Example**

```bash
curl -X GET \
  https://rekosearch.com/api/v1/user/profile \
  -H 'Authorization: token123'
```

### User Update

**Description**  
Update the current user's profile information: first name, last name, username, and birthdate.

**URL**  
`/api/v1/user/update`

**Method**  
`POST`

**Authentication Required**  
Yes

**Headers**

```
Authorization: {token}
Content-Type: application/json
Accept: application/json
```

**Request Body**

```json
{
  "first_name": "John",
  "last_name": "Doe",
  "username": "johndoe",
  "birthdate": "2010-08-08"
}
```

**Successful Response**

- **Status Code**: 200 OK
- **Response Body**:

```json
{
  "message": "User attributes updated successfully"
}
```

**Error Responses**

| Status Code | Description  | Response Body                                                       |
| ----------- | ------------ | ------------------------------------------------------------------- |
| 400         | Bad Request  | `{"message": "Error...", "example_format": {"field": "has to..."}}` |
| 401         | Unauthorized | `{"message": "Unauthorized"}`                                       |
| 500         | Server Error | `{"message": "Internal server error"}`                                |

**Example**

```bash
curl -X POST \
  https://rekosearch.com/api/v1/user/update \
  -H 'Authorization: token123' \
  -H 'Content-Type: application/json' \
  -d '{
    "first_name": "John",
    "last_name": "Doe",
    "username": "johndoe",
    "birthdate": "2010-08-08"'
```

## Internally Used

### User Accept Terms

**Description**  
Accept the Terms of Service (ToS) and Privacy Policy (PP) for the current user.

**URL**  
`/api/v1/user/accept-terms`

**Method**  
`POST`

**Authentication Required**  
Yes

**Headers**

```
Authorization: {token}
```

**Successful Response**

- **Status Code**: 200 OK
- **Response Body**:

```json
{
  "message": "User accepted the TOS and PP"
}
```

Or

```json
{
  "message": "User has already accepted the latest TOS and PP"
}
```

**Error Responses**

| Status Code | Description  | Response Body                                  |
| ----------- | ------------ | ---------------------------------------------- |
| 401         | Unauthorized | `{"message": "Unauthorized"}`                  |
| 500         | Server Error | `{"message": "Internal server failure message"}` |

**Example**

```bash
curl -X POST \
  https://rekosearch.com/api/v1/user/accept-terms \
  -H 'Authorization: token123'
```

### User Delete

**Description**  
PERMANENTLY AND IRREVERSIBLY DELETE THE USER CALLING IT WITHOUT ANY CONFIRMATION.

**URL**  
`/api/v1/user/delete`

**Method**  
`DELETE`

**Authentication Required**  
Yes

**Headers**

```
Authorization: {token}
```

**Successful Response**

- **Status Code**: 200 OK
- **Response Body**:

```json
{
  "message": "User (you) got deleted successfully"
}
```

**Error Responses**

| Status Code | Description  | Response Body                                  |
| ----------- | ------------ | ---------------------------------------------- |
| 401         | Unauthorized | `{"message": "Unauthorized"}`                  |
| 500         | Server Error | `{"message": "Internal server failure message"}` |

**Example**

```bash
curl -X DELETE \
  https://rekosearch.com/api/v1/user/delete \
  -H 'Authorization: token123'
```

## Additional Resources

- [Infrastructure Documentation](../../Infrastructure/README.md)
- [Logic Documentation](../../Logic/README.md)
