# API Documentation

## /admin/metrics/invocations
- **Method**: POST
- **Description**: Retrieves invocation metrics for a specified model and application.
- **Authentication**: Requires valid Cognito token.

### Request Parameters
- **Body**:
  - `model_id` (Optional, string): ID of the model.
  - `app_id` (Required, string): ID of the application.
  - `start_date` (Optional, string): Start date in yyyy-dd-mm format.
  - `end_date` (Optional, string): End date in yyyy-dd-mm format.

### Response Format
- **Success**: 200 OK
  ```json
  {
    "invocations": [
      {
        "timestamp": "2023-10-01T12:00:00Z",
        "count": 10
      }
    ]
  }
  ```
- **Fields**:
  - `timestamp`: ISO 8601 formatted date and time.
  - `count`: Number of invocations.

### Error Responses
- **400 Bad Request**: Invalid date format.
- **401 Unauthorized**: Missing or invalid token.

## /admin/metrics/extraction-jobs
- **Method**: POST
- **Description**: Retrieves metrics for document extraction jobs.
- **Authentication**: Requires valid Cognito token.

### Request Parameters
- **Body**:
  - `app_id` (Required, string): ID of the application.
  - `start_date` (Optional, string): Start date in yyyy-dd-mm format.
  - `end_date` (Optional, string): End date in yyyy-dd-mm format.

### Response Format
- **Success**: 200 OK
  ```json
  {
    "jobs": [
      {
        "job_id": "12345",
        "status": "completed"
      }
    ]
  }
  ```
- **Fields**:
  - `job_id`: Unique identifier for the job.
  - `status`: Current status of the job.

### Error Responses
- **400 Bad Request**: Invalid date format.
- **401 Unauthorized**: Missing or invalid token.

## /admin/metrics/vector-stores
- **Method**: POST
- **Description**: Retrieves metrics for vector stores.
- **Authentication**: Requires valid Cognito token.

### Request Parameters
- **Body**:
  - `app_id` (Required, string): ID of the application.
  - `start_date` (Optional, string): Start date in yyyy-dd-mm format.
  - `end_date` (Optional, string): End date in yyyy-dd-mm format.

### Response Format
- **Success**: 200 OK
  ```json
  {
    "vector_stores": [
      {
        "store_id": "67890",
        "size": 1000
      }
    ]
  }
  ```
- **Fields**:
  - `store_id`: Unique identifier for the vector store.
  - `size`: Number of vectors stored.

### Error Responses
- **400 Bad Request**: Invalid date format.
- **401 Unauthorized**: Missing or invalid token.

## Rate Limits and Usage Constraints
- No specific rate limits are defined, but standard AWS API Gateway limits apply.

## Dependencies and Prerequisites
- Requires AWS Cognito for authentication.
- DynamoDB is used for storing metrics data. 
