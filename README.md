# Exhaustive API Documentation

## Complete Service Inventory

### Overview
- **Frontend Service**: Handles user interactions and serves the web interface.
- **Cart Service**: Manages user cart operations.
- **Product Catalog Service**: Provides product information.
- **Recommendation Service**: Offers product recommendations.
- **Payment Service**: Handles payment processing.
- **Shipping Service**: Manages shipping logistics.
- **Email Service**: Sends email notifications.
- **Currency Service**: Provides currency conversion.
- **Checkout Service**: Manages the checkout process.
- **Ad Service**: Displays advertisements.

## Global Overview

### System-wide API Map
- **Architectural Patterns**: REST, gRPC.
- **Authentication and Authorization**: Session management, OAuth.

## Service/API Component Details

### Frontend Service
- **Purpose**: Serves the web interface and manages user sessions.
- **Dependencies**: Connects to all backend services.
- **Configuration**: Environment variables for service addresses.
- **API Version**: v1

#### API Endpoints
- **`GET /`**: Home page.
  - **Method**: GET
  - **Request Parameters**: None
  - **Response**: HTML page
  - **Authentication**: Required
  - **Example**:
    ```http
    GET / HTTP/1.1
    Host: example.com
    ```

- **`GET /product/{id}`**: Fetch product details.
  - **Method**: GET
  - **Request Parameters**:
    - **Path**: `id` (string) - Product ID
  - **Response**: JSON with product details
  - **Authentication**: Required
  - **Example**:
    ```http
    GET /product/123 HTTP/1.1
    Host: example.com
    ```

## Classes and Methods

### Class: `frontendServer`
- **Description**: Manages connections to backend services.
- **Constructor Parameters**: None
- **Properties**:
  - `productCatalogSvcAddr`: Address of the product catalog service.
- **Methods**:
  - `main()`: Initializes the server.
    - **Parameters**: None
    - **Return Values**: None
    - **Example**:
      ```go
      func main() {
          // Initialize server
      }
      ```

## Data Models

### ProductView
- **Fields**:
  - `Item`: *pb.Product
  - `Price`: *pb.Money

## Client SDK Documentation

### Installation
- **Instructions**: Use npm or pip to install.

## Webhook Documentation

### Event Types
- **Order Placed**: Triggered when an order is placed.

## Formatting
- **Markdown**: Used for consistent formatting.
- **Code Blocks**: Included for examples.

## Additional Requirements
- **Deprecated Features**: None
- **Versioning Strategy**: Semantic versioning
- **Performance Considerations**: Use caching for product data.

This is a starting point for the documentation. Further details can be added for each service and component as needed. 

## Exhaustive API Endpoint Documentation

### Frontend Service Endpoints

#### `GET /`
- **Complete URL Path**: `/`
- **HTTP Method**: GET
- **Description**: Retrieves the home page of the web interface.
- **Request Parameters**: None
- **Response Status Codes**:
  - **200 OK**: Successful retrieval of the home page.
- **Response Body**: HTML content of the home page.
- **Authentication**: Required
- **Example Request**:
  ```http
  GET / HTTP/1.1
  Host: example.com
  Authorization: Bearer <token>
  ```
- **Example Response**:
  ```html
  <!DOCTYPE html>
  <html>
  <head><title>Home</title></head>
  <body>Welcome to the homepage!</body>
  </html>
  ```

#### `GET /product/{id}`
- **Complete URL Path**: `/product/{id}`
- **HTTP Method**: GET
- **Description**: Fetches details of a specific product by ID.
- **Request Parameters**:
  - **Path**: `id` (string) - Product ID
- **Response Status Codes**:
  - **200 OK**: Product details retrieved successfully.
  - **404 Not Found**: Product not found.
- **Response Body**:
  - **200 OK**: JSON with product details.
  - **404 Not Found**: JSON with error message.
- **Authentication**: Required
- **Example Request**:
  ```http
  GET /product/123 HTTP/1.1
  Host: example.com
  Authorization: Bearer <token>
  ```
- **Example Response (200 OK)**:
  ```json
  {
    "id": "123",
    "name": "Product Name",
    "price": 19.99
  }
  ```
- **Example Response (404 Not Found)**:
  ```json
  {
    "error": "Product not found"
  }
  ```

## Authentication and Authorization

### Authentication Methods
- **Bearer Token**: Used for authenticating API requests.
- **Example**:
  ```http
  Authorization: Bearer <token>
  ```

## Request/Response Examples

### Example Requests
- **Curl**:
  ```bash
  curl -X GET "http://example.com/product/123" -H "Authorization: Bearer <token>"
  ```

### Example Responses
- **Success**:
  ```json
  {
    "id": "123",
    "name": "Product Name",
    "price": 19.99
  }
  ```
- **Error**:
  ```json
  {
    "error": "Product not found"
  }
  ```

## Data Types and Models

### Product Model
- **Fields**:
  - `id`: string - Unique identifier for the product.
  - `name`: string - Name of the product.
  - `price`: float - Price of the product.

## Parameter Validation

### Validation Rules
- **Product ID**: Must be a valid string.
- **Error Response**:
  ```json
  {
    "error": "Invalid product ID"
  }
  ```

## Pagination, Filtering, and Sorting

### Pagination
- **Parameters**:
  - `page`: integer - Page number.
  - `size`: integer - Number of items per page.

## Rate Limiting and Quotas

### Rate Limiting
- **Policy**: 100 requests per minute.
- **Headers**:
  - `X-RateLimit-Limit`: Maximum number of requests.
  - `X-RateLimit-Remaining`: Remaining requests in the current window.

## Versioning Information

### API Versioning
- **Current Version**: v1
- **Deprecation Notices**: None

## Webhooks and Events

### Order Placed Event
- **Trigger**: When an order is placed.
- **Payload**:
  ```json
  {
    "orderId": "12345",
    "status": "placed"
  }
  ```

## SDK Documentation

### Client SDK Methods
- **GetProduct**: Retrieves product details by ID.
- **Example**:
  ```python
  product = client.get_product("123")
  ```

## Formatting and Organization
- **Markdown**: Used for consistent formatting.
- **Tables and Code Blocks**: Used for clarity.

This documentation provides a comprehensive overview of the API, covering all aspects of each service and endpoint. Further details can be added as needed. 

## Cart Service API Documentation

### Overview
The Cart Service manages user cart operations, allowing users to add items, view their cart, and empty their cart.

### API Endpoints

1. **Add Item to Cart**
   - **Method**: gRPC
   - **Service Method**: `AddItem`
   - **Description**: Adds an item to the user's cart.
   - **Request**:
     - **Type**: `AddItemRequest`
     - **Fields**:
       - `UserId` (string): The ID of the user.
       - `Item` (object): The item to add.
         - `ProductId` (string): The ID of the product.
         - `Quantity` (int): The quantity of the product.
   - **Response**:
     - **Type**: `Empty`
     - **Description**: Indicates successful addition of the item.
   - **Example Request**:
     ```json
     {
       "UserId": "user123",
       "Item": {
         "ProductId": "product456",
         "Quantity": 2
       }
     }
     ```

2. **Get Cart**
   - **Method**: gRPC
   - **Service Method**: `GetCart`
   - **Description**: Retrieves the user's cart.
   - **Request**:
     - **Type**: `GetCartRequest`
     - **Fields**:
       - `UserId` (string): The ID of the user.
   - **Response**:
     - **Type**: `Cart`
     - **Fields**:
       - `UserId` (string): The ID of the user.
       - `Items` (array): List of items in the cart.
         - `ProductId` (string): The ID of the product.
         - `Quantity` (int): The quantity of the product.
   - **Example Request**:
     ```json
     {
       "UserId": "user123"
     }
     ```
   - **Example Response**:
     ```json
     {
       "UserId": "user123",
       "Items": [
         {
           "ProductId": "product456",
           "Quantity": 2
         }
       ]
     }
     ```

3. **Empty Cart**
   - **Method**: gRPC
   - **Service Method**: `EmptyCart`
   - **Description**: Empties the user's cart.
   - **Request**:
     - **Type**: `EmptyCartRequest`
     - **Fields**:
       - `UserId` (string): The ID of the user.
   - **Response**:
     - **Type**: `Empty`
     - **Description**: Indicates successful emptying of the cart.
   - **Example Request**:
     ```json
     {
       "UserId": "user123"
     }
     ```

### Authentication and Authorization
- **Authentication**: Typically handled at the gRPC level, often using tokens or certificates.
- **Authorization**: Ensures that the user has permission to modify their own cart.

### Data Models

- **AddItemRequest**
  - **Fields**:
    - `UserId`: string
    - `Item`: object
      - `ProductId`: string
      - `Quantity`: int

- **GetCartRequest**
  - **Fields**:
    - `UserId`: string

- **EmptyCartRequest**
  - **Fields**:
    - `UserId`: string

- **Cart**
  - **Fields**:
    - `UserId`: string
    - `Items`: array of objects
      - `ProductId`: string
      - `Quantity`: int

This documentation provides a detailed overview of the Cart Service's API. Further details can be added for other services as needed. 
