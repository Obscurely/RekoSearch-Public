# Endpoint Documentation: /jobs

Manage file processing jobs (list, get details, delete)

<!--toc:start-->

- [User Available](#user-available)
  - [Jobs Get](#jobs-get) (GET /get)
  - [Jobs List](#jobs-list) (GET /list)
  - [Jobs Get Object Url](#jobs-get-object-url) (GET /get-object-url)
  - [Jobs Delete](#jobs-delete) (DELETE /delete)
- [Additional Resources](#additional-resources)
<!--toc:end-->

Check [API README.md](../README.md) for the BASE URL.

If you are interested in the inner workings check [Additional Resources](#additional-resources).

## User Available

### Jobs Get

**Description**  
Get all info about a job including links to the results if available.

**URL**  
`/api/v1/jobs/get`

**Method**  
`GET`

**Authentication Required**  
Yes

**Headers**

```
Authorization: {token}
```

**Query Parameters**

| Parameter | Required | Type   | Description       |
| --------- | -------- | ------ | ----------------- |
| job-id    | Yes      | number | The id of the job |

**Successful Response**

- **Status Code**: 200 OK
- **Response Body**:

```json
{
  "job_info": {
    "user_id": "user-id",
    "job_id": 1,
    "job_name": "Job Name",
    "date": "2020-01-01 12:00:00.000000000 UTC",
    "total_size": 5020,
    "credits_spent": 2,
    "email": "example@domain.com",
    "object_uuid_names": {
      "uuid.png": "file.png"
    },
    "media_length": {
      "uuid.png": 1
    },
    "failed_to_process": {},
    "status": "success"
  },
  "results": {
    "uuid.png": {
      "full": "https://rekosearch-bucket-url/link-to.json",
      "min": "https://rekosearch-bucket-url/link-to.min.json"
    }
  }
}
```

**Error Responses**

| Status Code | Description  | Response Body                                                                                         |
| ----------- | ------------ | ----------------------------------------------------------------------------------------------------- |
| 400         | Bad Request  | `{"message": "The job-id query parameter is missing", "affected_query_parameter": "job-id: number" }` |
| 401         | Unauthorized | `{"message": "Unauthorized"}`                                                                         |
| 404         | Not Found    | `{"message": "The job does not exist", "affected_query_parameter": "job-id: number"}`                 |
| 500         | Server Error | `{"message": "Internal server failure message"}`                                                      |

**Example**

```bash
curl -X GET \
  https://rekosearch.com/api/v1/jobs/get?job-id=1 \
  -H 'Authorization: token123'
```

### Jobs List

**Description**  
Get a list of all jobs for the current user. The id, name, size, date, cost, short hand status and status meaning of each job.

**URL**  
`/api/v1/jobs/list`

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
  "jobs": [
    {
      "job_id": 1,
      "job_name": "Job Name",
      "date": "2020-01-01 12:00:00.000000000 UTC",
      "total_size": 10240,
      "credits_spent": 1,
      "status": "success",
      "status_meaning": "Job completed successfully"
    }
  ]
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
  https://rekosearch.com/api/v1/jobs/list \
  -H 'Authorization: token123'
```

### Jobs Get Object Url

**Description**  
Get the URL of a specific object in a job i.e the link to a file.

**URL**  
`/api/v1/jobs/get-object-url`

**Method**  
`GET`

**Authentication Required**  
Yes

**Headers**

```
Authorization: {token}
```

**Query Parameters**

| Parameter   | Required | Type   | Description                                             |
| ----------- | -------- | ------ | ------------------------------------------------------- |
| job-id      | Yes      | number | The id of the job                                       |
| object-uuid | Yes      | number | The uuid of the object/file (find this using /jobs/get) |

**Successful Response**

- **Status Code**: 200 OK
- **NOTE**: It doesn't check if the object exists or not. So you might get a link to a non-existing object.
- **Response Body**:

```json
{
  "url": "https://rekosearch-bucket-url/link-to-object"
}
```

**Error Responses**

| Status Code | Description  | Response Body                                                                             |
| ----------- | ------------ | ----------------------------------------------------------------------------------------- |
| 400         | Bad Request  | `{"message": "The X query parameter is missing", "affected_query_parameter": "X: type" }` |
| 401         | Unauthorized | `{"message": "Unauthorized"}`                                                             |
| 500         | Server Error | `{"message": "Internal server failure message"}`                                          |

**Example**

```bash
curl -X GET \
  https://rekosearch.com/api/v1/jobs/get-object-url?job-id=1&object-uuid=uuid.ext \
  -H 'Authorization: token123'
```

### Jobs Delete

**Description**  
Delete a job. This will remove all data related to the job including the files.

**URL**  
`/api/v1/jobs/delete`

**Method**  
`DELETE`

**Authentication Required**  
Yes

**Headers**

```
Authorization: {token}
```

**Query Parameters**

| Parameter | Required | Type   | Description                 |
| --------- | -------- | ------ | --------------------------- |
| job-id    | Yes      | number | The id of the job to delete |

**Successful Response**

- **Status Code**: 200 OK
- **Response Body**:

```json
{
  "message": "Ok"
}
```

**Error Responses**

| Status Code | Description  | Response Body                                                                                         |
| ----------- | ------------ | ----------------------------------------------------------------------------------------------------- |
| 400         | Bad Request  | `{"message": "The job-id query parameter is missing", "affected_query_parameter": "job-id: number" }` |
| 401         | Unauthorized | `{"message": "Unauthorized"}`                                                                         |
| 500         | Server Error | `{"message": "Internal server failure message"}`                                                      |

**Example**

```bash
curl -X DELETE \
  https://rekosearch.com/api/v1/jobs/delete?job-id=1 \
  -H 'Authorization: token123'
```

## Additional Resources

- [Infrastructure Documentation](../../Infrastructure/README.md)
- [Logic Documentation](../../Logic/README.md)
