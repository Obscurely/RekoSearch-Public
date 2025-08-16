# Endpoint Documentation: /upload

Create and upload data for new file-processing jobs

<!--toc:start-->

- [Endpoint Documentation: /upload](#endpoint-documentation-upload)
  - [User Available](#user-available)
    - [Upload/Job Generation](#uploadjob-generation)
    - [Complete Multipart Upload](#complete-multipart-upload)
  - [Additional Resources](#additional-resources)
  <!--toc:end-->

Check [API README.md](../README.md) for the BASE URL.

If you are interested in the inner workings check [Additional Resources](#additional-resources).

## User Available

### Upload/Job Generation

**Description**  
Generate a new job and get URLs for uploading files (and other info about the new job).

**URL**  
`/api/v1/upload/gen`

**Method**  
`POST`

**Authentication Required**  
Yes

**Headers**

```
Authorization: {token}
Send-Email: Boolean (?1 or ?0 for wether to send update emails)
Content-Type: application/json
Accept: application/json
```

**Request Body**

```json
{
  "job_name": "Job Name (Optional Field, jobs can be nameless)",
  "objects": [
    {
      "object_name": "file.png",
      "content_length": 4778394,
      "media_length": 1,
      "object_id": 15
    }
    {
      "object_name": "file.mp4",
      "content_length": 477839400,
      "media_length": 8,
      "object_id": 17
    }
  ]
}
```

Notes:

- The job_name field is optional. If not provided, the job will be nameless.
- The content_lenght field is the size of the file in bytes.
- The media_length is as follows depending on the file type:
  - For images, it is 1 (doesn't matter what you input, but you have to input something).
  - For videos, it is the length of the video in seconds.
  - For audio, it is the length of the audio in seconds.
  - For PDFs and TIFFs, it is the number of pages.
- The object id an OPTIONAL uniqued identifier for the object returned in the response as well you can use to identify objects with the same names.

Restrictions:

- The job_name cannot be longer than 20 characters.
- The objects have to be end in one of the following formats: "png", "jpg", "mp4", "mov", "tiff", "pdf", "mp3", "mp4", "wav", "flac", "amr", "ogg",
  "webm".
- There can't be more than 1000 objects in a single job.
- Image files cannot be larger than 15MB.
- Video files cannot be longer than 2 hours or larger than 10GB.
- Audio files cannot be longer than 4 hours or larger than 2GB. They also must be in English (US).
- PDFs and TIFFs cannot have more than 50 pages or be larger than 500MB.

**Successful Response**

- **Status Code**: 200 OK
- **Response Body**:

```json
{
  "message": "You had enough credits to perform this operation.",
  "credits_before": 100,
  "credits_now": 97,
  "credits_used": 3,
  "job_id": 1,
  "job_name": "Job Name (if provided)",
  "metadata_filename_key": "x-amz-meta-original-filename",
  "pre_signed_uploads": [
    {
      "object_name": "file.png",
      "object_uuid": "uuid.png",
      "object_id": 15,
      "object_key": "user-id/job-id/uuid.png",
      "upload_type": "PutObject",
      "upload_id": "0",
      "urls": [
        "https://rekosearch-bucket-url/put-object-url-to-upload-to"
      ],
      "part_sizes": [4778394],
      "part_count": 1,
      "expiration_in_secs": 420
    }
    {
      "object_name": "file.mp4",
      "object_uuid": "uuid.mp4",
      "object_id": 17,
      "object_key": "user-id/job-id/uuid.mp4",
      "upload_type": "MultipartUpload",
      "upload_id": "upload-id",
      "urls": [
        "https://rekosearch-bucket-url/upload-part-url1",
        "https://rekosearch-bucket-url/upload-part-url2",
        "https://rekosearch-bucket-url/upload-part-url2",
      ],
      "part_sizes": [
        159279800,
        159279800,
        159279800
      ],
      "part_count": 3,
      "expiration_in_secs": 13950
    }
  ],
  "manifest_upload": {
    "object_name": "DONE",
    "object_key": "user-id/job-id/DONE",
    "upload_type": "PutObject",
    "url": "https://rekosearch-bucket-url/put-manifest-object-url-to-upload-to",
    "size": 0,
    "expiration_in_secs": 28470
  }
}
```

Notes:

- The message field indicates whether the user had enough credits to perform the operation.
- The credits_before field indicates the number of credits the user had before the operation.
- The credits_now field indicates the number of credits the user has after the operation.
- The credits_used field indicates the number of credits used for this operation.
- The job_id field indicates the ID of the new job.
- The job_name field indicates the name of the new job (if provided).
- The metadata_filename_key field indicates the key used to store the original filename in S3.
- The pre_signed_uploads field contains an array of objects with the following fields:
  - object_name: The name of the object to upload.
  - object_uuid: The UUID created for the object in S3.
  - object_id: The ID of the object.
  - object_key: The key used to store the object in S3.
  - upload_type: The type of upload (PutObject or MultipartUpload).
  - upload_id: The ID of the upload (if applicable).
  - urls: An array of URLs for uploading the object.
  - part_sizes: An array of sizes for each part (if applicable).
  - part_count: The number of parts (if applicable).
  - expiration_in_secs: The expiration time in seconds for the URLs.

How to upload the files and strat the job:

1. Upload the files using the provided URLs.
   - For PutObject uploads, use the provided URL to upload the file.
   - For MultipartUpload, use the provided URLs to upload each part of the file. The file
     should be split into parts according to the part_sizes array. At the end of the upload, you need to call the [/complete-multipart](#complete-multipart-upload) endpoint to finalize the upload.
2. Upload the manifest file using the provided URL in the manifest_upload field. The manifest file should just be an empty object. Once the manifest file is uploaded, the files will the shortly there after processed.

**Error Responses**

| Status Code | Description  | Response Body                                                                                                   |
| ----------- | ------------ | --------------------------------------------------------------------------------------------------------------- |
| 400         | Bad Request  | `{"message": "Invalid input error message + potentially another field regarding the bad part." }`               |
| 401         | Unauthorized | `{"message": "Unauthorized"}` or `{"message": "Failed. You do not have enough credits for the requested job."}` |
| 500         | Server Error | `{"message": "Internal server failure message"}`                                                                |

**Example**

```bash
curl -X POST \
  https://rekosearch.com/api/v1/upload/gen \
  -H 'Authorization: token123' \
  -H 'Content-Type: application/json' \
  -d '{
    "job_name": "Job Name",
    "objects": [
      {
        "object_name": "file.png",
        "content_length": 4778394,
        "media_length": 1,
        "object_id": 15
      },
      {
        "object_name": "file.mp4",
        "content_length": 477839400,
        "media_length": 8,
        "object_id": 17
      }
    ]'
```

### Complete Multipart Upload

**Description**  
Finalize the upload of a multipart file.

**URL**  
`/api/v1/upload/complete-multipart`

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
  "object_key": "userid/jobid/object_uuid",
  "upload_id": "upload-id",
  "job_id": 1,
  "parts": [
    {
      "part_number": 1,
      "etag": "stoastn"
    },
    {
      "part_number": 2,
      "etag": "stats"
    }
  ]
}
```

Notes:

- The object_key field is the key used to store the object in S3. You will find in the /upload/gen response.
- The upload_id field is the ID of the upload (provided in the /upload/gen response).
- The job_id field is the ID of the job (provided in the /upload/gen response).
- The parts field is an array of objects with the following fields:
  - part_number: The part number of the uploaded part.
  - etag: The ETag of the uploaded part. This is provided by S3 when the part is uploaded.

**Successful Response**

- **Status Code**: 200 OK
- **Response Body**:

```json
{
  "message": "Successfully completed the multipart upload!"
}
```

**Error Responses**

| Status Code | Description          | Response Body                                                                                                                                                                                            |
| ----------- | -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 400         | Bad Request          | `{"message": "Wrong body, missing part or too many parts" }`                                                                                                                                             |
| 401         | Unauthorized         | `{"message": "Unauthorized"}`                                                                                                                                                                            |
| 404         | Not Found            | `{"message": "The given upload id has not been found under the given job id!"}`                                                                                                                          |
| 422         | Unprocessable Entity | `{"message": "Failed to complete multipart upload. Please thorougly check your part numbers and etags. Also make sure the provided object_key is right. If they are good than this is a server error."}` |
| 500         | Server Error         | `{"message": "Internal server failure message"}`                                                                                                                                                         |

**Example**

```bash
curl -X POST \
  https://rekosearch.com/api/v1/upload/complete-multipart \
  -H 'Authorization: token123' \
  -H 'Content-Type: application/json' \
  -d '{
    "object_key": "userid/jobid/object_uuid",
    "upload_id": "upload-id",
    "job_id": 1,
    "parts": [
      {
        "part_number": 1,
        "etag": "stoastn"
      },
      {
        "part_number": 2,
        "etag": "stats"
      }
    ]'
```

## Additional Resources

- [Application Documentation](../../Application/README.md)
- [Infrastructure Documentation](../../Infrastructure/README.md)
