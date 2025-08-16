# API Documentation

<!--toc:start-->

- [Overview](#overview)
- [API Classes](#api-classes)
  - [User Endpoints](#user-endpoints)
  - [Jobs Endpoints](#jobs-endpoints)
  - [Upload Endpoints](#upload-endpoints)
- [Technical Implementation](#technical-implementation)
- [Additional Resources](#additional-resources)
<!--toc:end-->

## Overview

This API provides access to RekoSearch services. The base URL is `https://rekosearch.com/api/` with the following structure:

```txt
https://rekosearch.com/api/{version}/{class}/{endpoint}
```

**Available Versions:**

- v1 (latest)

**Note:** User API key authentication is coming soon. Currently, the API uses OAuth2 authentication (same as the frontend).

If you are interested in the inner workings check [Additional Resources](#additional-resources).

## API Classes

### User Endpoints

[/user](./v1/USER.md)

- Get, update, and delete user information

### Jobs Endpoints

[/jobs](./v1/JOBS.md)

- Manage file processing jobs (list, get details, delete)

### Upload Endpoints

[/upload](./v1/UPLOAD.MD)

- Create and upload data for new file-processing jobs

Each page indicates which endpoints are available for external users ("User Available") and those used internally ("Internally Used").

## Technical Implementation

The API request flow follows this path:

1. **Client Request** → HTTP request with method, body, headers, and parameters
2. **AWS Route53** → DNS resolution
3. **AWS CloudFront** → CDN that routes `/api` requests to API Gateway (caching disabled)
4. **AWS API Gateway** → Routes requests based on version, class, and endpoint
5. **Authentication** → Cognito-based authorization using id_tokens (refreshed every 30 minutes). Soon, USER API keys, too.
6. **AWS Lambda** → The function retrieves the user ID and any other required information and performs the required actions on DynamoDB (Database), S3 (File Storage), Cognito (User database) and more.
7. **Client Response** → Returns data to the client

## Additional Resources

- [Application Documentation](../Application/README.md)
- [Infrastructure Documentation](../Infrastructure/README.md)
