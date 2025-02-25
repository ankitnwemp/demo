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

- **`GET /cart`**: View cart.
  - **Method**: GET
  - **Request Parameters**: None
  - **Response**: JSON with cart details
  - **Authentication**: Required
  - **Example**:
    ```http
    GET /cart HTTP/1.1
    Host: example.com
    ```

- **`POST /cart`**: Add to cart.
  - **Method**: POST
  - **Request Parameters**:
    - **Body**: JSON with product ID and quantity
  - **Response**: Redirect to cart
  - **Authentication**: Required
  - **Example**:
    ```http
    POST /cart HTTP/1.1
    Host: example.com
    Content-Type: application/json

    {
      "product_id": "123",
      "quantity": 2
    }
    ```

- **`POST /cart/empty`**: Empty cart.
  - **Method**: POST
  - **Request Parameters**: None
  - **Response**: Redirect to home
  - **Authentication**: Required
  - **Example**:
    ```http
    POST /cart/empty HTTP/1.1
    Host: example.com
    ```

- **`POST /setCurrency`**: Set currency.
  - **Method**: POST
  - **Request Parameters**:
    - **Body**: JSON with currency code
  - **Response**: Redirect to home
  - **Authentication**: Required
  - **Example**:
    ```http
    POST /setCurrency HTTP/1.1
    Host: example.com
    Content-Type: application/json

    {
      "currency": "USD"
    }
    ```

- **`GET /logout`**: Logout.
  - **Method**: GET
  - **Request Parameters**: None
  - **Response**: Redirect to home
  - **Authentication**: Required
  - **Example**:
    ```http
    GET /logout HTTP/1.1
    Host: example.com
    ```

- **`POST /cart/checkout`**: Checkout.
  - **Method**: POST
  - **Request Parameters**:
    - **Body**: JSON with order details
  - **Response**: Order confirmation
  - **Authentication**: Required
  - **Example**:
    ```http
    POST /cart/checkout HTTP/1.1
    Host: example.com
    Content-Type: application/json

    {
      "email": "user@example.com",
      "street_address": "123 Main St",
      "zip_code": "12345",
      "city": "Anytown",
      "state": "CA",
      "country": "USA",
      "credit_card_number": "4111111111111111",
      "credit_card_expiration_month": "12",
      "credit_card_expiration_year": "2025",
      "credit_card_cvv": "123"
    }
    ```

- **`GET /assistant`**: Shopping assistant.
  - **Method**: GET
  - **Request Parameters**: None
  - **Response**: HTML page
  - **Authentication**: Required
  - **Example**:
    ```http
    GET /assistant HTTP/1.1
    Host: example.com
    ```

- **`GET /product-meta/{ids}`**: Fetch product metadata.
  - **Method**: GET
  - **Request Parameters**:
    - **Path**: `ids` (string) - Comma-separated product IDs
  - **Response**: JSON with product metadata
  - **Authentication**: Required
  - **Example**:
    ```http
    GET /product-meta/123,456 HTTP/1.1
    Host: example.com
    ```

- **`POST /bot`**: Chatbot interaction.
  - **Method**: POST
  - **Request Parameters**:
    - **Body**: JSON with message
  - **Response**: JSON with chatbot response
  - **Authentication**: Required
  - **Example**:
    ```http
    POST /bot HTTP/1.1
    Host: example.com
    Content-Type: application/json

    {
      "message": "Hello"
    }
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

## Product Catalog Service API Documentation

### Overview
The Product Catalog Service provides product information, including listings, details, and search functionality.

### API Endpoints

1. **List Products**
   - **Method**: gRPC
   - **Service Method**: `ListProducts`
   - **Description**: Retrieves a list of all products.
   - **Request**:
     - **Type**: `Empty`
     - **Fields**: None
   - **Response**:
     - **Type**: `ListProductsResponse`
     - **Fields**:
       - `Products` (array): List of products.
   - **Example Request**:
     ```json
     {}
     ```
   - **Example Response**:
     ```json
     {
       "Products": [
         {
           "Id": "product1",
           "Name": "Product 1",
           "Description": "Description of Product 1",
           "Price": 29.99
         }
       ]
     }
     ```

2. **Get Product**
   - **Method**: gRPC
   - **Service Method**: `GetProduct`
   - **Description**: Fetches details of a specific product by ID.
   - **Request**:
     - **Type**: `GetProductRequest`
     - **Fields**:
       - `Id` (string): The ID of the product.
   - **Response**:
     - **Type**: `Product`
     - **Fields**:
       - `Id` (string): The ID of the product.
       - `Name` (string): The name of the product.
       - `Description` (string): The description of the product.
       - `Price` (float): The price of the product.
   - **Example Request**:
     ```json
     {
       "Id": "product1"
     }
     ```
   - **Example Response**:
     ```json
     {
       "Id": "product1",
       "Name": "Product 1",
       "Description": "Description of Product 1",
       "Price": 29.99
     }
     ```

3. **Search Products**
   - **Method**: gRPC
   - **Service Method**: `SearchProducts`
   - **Description**: Searches for products based on a query string.
   - **Request**:
     - **Type**: `SearchProductsRequest`
     - **Fields**:
       - `Query` (string): The search query.
   - **Response**:
     - **Type**: `SearchProductsResponse`
     - **Fields**:
       - `Results` (array): List of products matching the query.
   - **Example Request**:
     ```json
     {
       "Query": "Product"
     }
     ```
   - **Example Response**:
     ```json
     {
       "Results": [
         {
           "Id": "product1",
           "Name": "Product 1",
           "Description": "Description of Product 1",
           "Price": 29.99
         }
       ]
     }
     ```

### Authentication and Authorization
- **Authentication**: Typically handled at the gRPC level, often using tokens or certificates.
- **Authorization**: Ensures that the user has permission to access product information.

### Data Models

- **GetProductRequest**
  - **Fields**:
    - `Id`: string

- **SearchProductsRequest**
  - **Fields**:
    - `Query`: string

- **Product**
  - **Fields**:
    - `Id`: string
    - `Name`: string
    - `Description`: string
    - `Price`: float

- **ListProductsResponse**
  - **Fields**:
    - `Products`: array of `Product`

- **SearchProductsResponse**
  - **Fields**:
    - `Results`: array of `Product`

## Recommendation Service API Documentation

### Overview
The Recommendation Service offers product recommendations.

### API Endpoints

1. **List Recommendations**
   - **Method**: gRPC
   - **Service Method**: `ListRecommendations`
   - **Description**: Provides a list of recommended products.
   - **Request**:
     - **Type**: `ListRecommendationsRequest`
     - **Fields**:
       - `UserId` (string): The ID of the user.
       - `ProductIds` (array): List of product IDs for which recommendations are sought.
   - **Response**:
     - **Type**: `ListRecommendationsResponse`
     - **Fields**:
       - `ProductIds` (array): List of recommended product IDs.
   - **Example Request**:
     ```json
     {
       "UserId": "user123",
       "ProductIds": ["product1", "product2"]
     }
     ```
   - **Example Response**:
     ```json
     {
       "ProductIds": ["product3", "product4"]
     }
     ```

### Authentication and Authorization
- **Authentication**: Typically handled at the gRPC level, often using tokens or certificates.
- **Authorization**: Ensures that the user has permission to access recommendations.

### Data Models

- **ListRecommendationsRequest**
  - **Fields**:
    - `UserId`: string
    - `ProductIds`: array of strings

- **ListRecommendationsResponse**
  - **Fields**:
    - `ProductIds`: array of strings

## Payment Service API Documentation

### Overview
The Payment Service handles payment processing.

### API Endpoints

1. **Charge**
   - **Method**: gRPC
   - **Service Method**: `Charge`
   - **Description**: Processes a payment charge.
   - **Request**:
     - **Type**: `ChargeRequest`
     - **Fields**:
       - `Amount` (object): The amount to charge.
         - `CurrencyCode` (string): The currency code.
         - `Units` (int): The whole units of the amount.
         - `Nanos` (int): The fractional units of the amount.
       - `CreditCard` (object): The credit card information.
         - `Number` (string): The credit card number.
         - `Cvv` (int): The CVV code.
         - `ExpirationMonth` (int): The expiration month.
         - `ExpirationYear` (int): The expiration year.
   - **Response**:
     - **Type**: `ChargeResponse`
     - **Fields**:
       - `TransactionId` (string): The transaction ID.
   - **Example Request**:
     ```json
     {
       "Amount": {
         "CurrencyCode": "USD",
         "Units": 100,
         "Nanos": 0
       },
       "CreditCard": {
         "Number": "4111111111111111",
         "Cvv": 123,
         "ExpirationMonth": 12,
         "ExpirationYear": 2025
       }
     }
     ```
   - **Example Response**:
     ```json
     {
       "TransactionId": "txn_123456789"
     }
     ```

### Authentication and Authorization
- **Authentication**: Typically handled at the gRPC level, often using tokens or certificates.
- **Authorization**: Ensures that the user has permission to perform the transaction.

### Data Models

- **ChargeRequest**
  - **Fields**:
    - `Amount`: object
      - `CurrencyCode`: string
      - `Units`: int
      - `Nanos`: int
    - `CreditCard`: object
      - `Number`: string
      - `Cvv`: int
      - `ExpirationMonth`: int
      - `ExpirationYear`: int

- **ChargeResponse**
  - **Fields**:
    - `TransactionId`: string

## Shipping Service API Documentation

### Overview
The Shipping Service manages shipping logistics.

### API Endpoints

1. **Get Quote**
   - **Method**: gRPC
   - **Service Method**: `GetQuote`
   - **Description**: Retrieves a shipping quote.
   - **Request**:
     - **Type**: `GetQuoteRequest`
     - **Fields**:
       - `Address` (object): The shipping address.
         - `StreetAddress` (string): The street address.
         - `City` (string): The city.
         - `State` (string): The state.
         - `Country` (string): The country.
         - `ZipCode` (string): The zip code.
       - `Items` (array): List of items to ship.
         - `ProductId` (string): The ID of the product.
         - `Quantity` (int): The quantity of the product.
   - **Response**:
     - **Type**: `GetQuoteResponse`
     - **Fields**:
       - `Cost` (object): The cost of shipping.
         - `CurrencyCode` (string): The currency code.
         - `Units` (int): The whole units of the cost.
         - `Nanos` (int): The fractional units of the cost.
   - **Example Request**:
     ```json
     {
       "Address": {
         "StreetAddress": "123 Main St",
         "City": "Anytown",
         "State": "CA",
         "Country": "USA",
         "ZipCode": "12345"
       },
       "Items": [
         {
           "ProductId": "product1",
           "Quantity": 2
         }
       ]
     }
     ```
   - **Example Response**:
     ```json
     {
       "Cost": {
         "CurrencyCode": "USD",
         "Units": 10,
         "Nanos": 0
       }
     }
     ```

2. **Ship Order**
   - **Method**: gRPC
   - **Service Method**: `ShipOrder`
   - **Description**: Processes the shipping of an order.
   - **Request**:
     - **Type**: `ShipOrderRequest`
     - **Fields**:
       - `OrderId` (string): The ID of the order.
   - **Response**:
     - **Type**: `ShipOrderResponse`
     - **Fields**:
       - `TrackingId` (string): The tracking ID for the shipment.
   - **Example Request**:
     ```json
     {
       "OrderId": "order123"
     }
     ```
   - **Example Response**:
     ```json
     {
       "TrackingId": "track_123456789"
     }
     ```

### Authentication and Authorization
- **Authentication**: Typically handled at the gRPC level, often using tokens or certificates.
- **Authorization**: Ensures that the user has permission to ship the order.

### Data Models

- **GetQuoteRequest**
  - **Fields**:
    - `Address`: object
      - `StreetAddress`: string
      - `City`: string
      - `State`: string
      - `Country`: string
      - `ZipCode`: string
    - `Items`: array of objects
      - `ProductId`: string
      - `Quantity`: int

- **GetQuoteResponse**
  - **Fields**:
    - `Cost`: object
      - `CurrencyCode`: string
      - `Units`: int
      - `Nanos`: int

- **ShipOrderRequest**
  - **Fields**:
    - `OrderId`: string

- **ShipOrderResponse**
  - **Fields**:
    - `TrackingId`: string

## Email Service API Documentation

### Overview
The Email Service sends email notifications.

### API Endpoints

1. **Send Order Confirmation**
   - **Method**: gRPC
   - **Service Method**: `SendOrderConfirmation`
   - **Description**: Sends an order confirmation email.
   - **Request**:
     - **Type**: `SendOrderConfirmationRequest`
     - **Fields**:
       - `OrderId` (string): The ID of the order.
       - `Email` (string): The email address to send the confirmation to.
   - **Response**:
     - **Type**: `SendOrderConfirmationResponse`
     - **Fields**:
       - `Success` (bool): Indicates if the email was sent successfully.
   - **Example Request**:
     ```json
     {
       "OrderId": "order123",
       "Email": "user@example.com"
     }
     ```
   - **Example Response**:
     ```json
     {
       "Success": true
     }
     ```

### Authentication and Authorization
- **Authentication**: Typically handled at the gRPC level, often using tokens or certificates.
- **Authorization**: Ensures that the user has permission to send the email.

### Data Models

- **SendOrderConfirmationRequest**
  - **Fields**:
    - `OrderId`: string
    - `Email`: string

- **SendOrderConfirmationResponse**
  - **Fields**:
    - `Success`: bool

## Currency Service API Documentation

### Overview
The Currency Service provides currency conversion.

### API Endpoints

1. **Get Supported Currencies**
   - **Method**: gRPC
   - **Service Method**: `GetSupportedCurrencies`
   - **Description**: Lists supported currencies.
   - **Request**:
     - **Type**: `Empty`
     - **Fields**: None
   - **Response**:
     - **Type**: `GetSupportedCurrenciesResponse`
     - **Fields**:
       - `CurrencyCodes` (array): List of supported currency codes.
   - **Example Request**:
     ```json
     {}
     ```
   - **Example Response**:
     ```json
     {
       "CurrencyCodes": ["USD", "EUR", "JPY"]
     }
     ```

2. **Convert**
   - **Method**: gRPC
   - **Service Method**: `Convert`
   - **Description**: Converts an amount from one currency to another.
   - **Request**:
     - **Type**: `CurrencyConversionRequest`
     - **Fields**:
       - `FromCurrency` (string): The currency code to convert from.
       - `ToCurrency` (string): The currency code to convert to.
       - `Amount` (object): The amount to convert.
         - `CurrencyCode` (string): The currency code of the amount.
         - `Units` (int): The whole units of the amount.
         - `Nanos` (int): The fractional units of the amount.
   - **Response**:
     - **Type**: `Money`
     - **Fields**:
       - `CurrencyCode` (string): The currency code of the converted amount.
       - `Units` (int): The whole units of the converted amount.
       - `Nanos` (int): The fractional units of the converted amount.
   - **Example Request**:
     ```json
     {
       "FromCurrency": "USD",
       "ToCurrency": "EUR",
       "Amount": {
         "CurrencyCode": "USD",
         "Units": 100,
         "Nanos": 0
       }
     }
     ```
   - **Example Response**:
     ```json
     {
       "CurrencyCode": "EUR",
       "Units": 85,
       "Nanos": 0
     }
     ```

### Authentication and Authorization
- **Authentication**: Typically handled at the gRPC level, often using tokens or certificates.
- **Authorization**: Ensures that the user has permission to perform currency conversion.

### Data Models

- **CurrencyConversionRequest**
  - **Fields**:
    - `FromCurrency`: string
    - `ToCurrency`: string
    - `Amount`: object
      - `CurrencyCode`: string
      - `Units`: int
      - `Nanos`: int

- **GetSupportedCurrenciesResponse**
  - **Fields**:
    - `CurrencyCodes`: array of strings

- **Money**
  - **Fields**:
    - `CurrencyCode`: string
    - `Units`: int
    - `Nanos`: int

## Checkout Service API Documentation

### Overview
The Checkout Service manages the checkout process.

### API Endpoints

1. **Place Order**
   - **Method**: gRPC
   - **Service Method**: `PlaceOrder`
   - **Description**: Places an order.
   - **Request**:
     - **Type**: `PlaceOrderRequest`
     - **Fields**:
       - `UserId` (string): The ID of the user.
       - `Cart` (object): The user's cart.
         - `UserId` (string): The ID of the user.
         - `Items` (array): List of items in the cart.
           - `ProductId` (string): The ID of the product.
           - `Quantity` (int): The quantity of the product.
       - `Address` (object): The shipping address.
         - `StreetAddress` (string): The street address.
         - `City` (string): The city.
         - `State` (string): The state.
         - `Country` (string): The country.
         - `ZipCode` (string): The zip code.
       - `CreditCard` (object): The credit card information.
         - `Number` (string): The credit card number.
         - `Cvv` (int): The CVV code.
         - `ExpirationMonth` (int): The expiration month.
         - `ExpirationYear` (int): The expiration year.
   - **Response**:
     - **Type**: `PlaceOrderResponse`
     - **Fields**:
       - `OrderId` (string): The ID of the order.
   - **Example Request**:
     ```json
     {
       "UserId": "user123",
       "Cart": {
         "UserId": "user123",
         "Items": [
           {
             "ProductId": "product1",
             "Quantity": 2
           }
         ]
       },
       "Address": {
         "StreetAddress": "123 Main St",
         "City": "Anytown",
         "State": "CA",
         "Country": "USA",
         "ZipCode": "12345"
       },
       "CreditCard": {
         "Number": "4111111111111111",
         "Cvv": 123,
         "ExpirationMonth": 12,
         "ExpirationYear": 2025
       }
     }
     ```
   - **Example Response**:
     ```json
     {
       "OrderId": "order123"
     }
     ```

### Authentication and Authorization
- **Authentication**: Typically handled at the gRPC level, often using tokens or certificates.
- **Authorization**: Ensures that the user has permission to place the order.

### Data Models

- **PlaceOrderRequest**
  - **Fields**:
    - `UserId`: string
    - `Cart`: object
      - `UserId`: string
      - `Items`: array of objects
        - `ProductId`: string
        - `Quantity`: int
    - `Address`: object
      - `StreetAddress`: string
      - `City`: string
      - `State`: string
      - `Country`: string
      - `ZipCode`: string
    - `CreditCard`: object
      - `Number`: string
      - `Cvv`: int
      - `ExpirationMonth`: int
      - `ExpirationYear`: int

- **PlaceOrderResponse**
  - **Fields**:
    - `OrderId`: string

## Ad Service API Documentation

### Overview
The Ad Service displays advertisements.

### API Endpoints

1. **Get Ads**
   - **Method**: gRPC
   - **Service Method**: `GetAds`
   - **Description**: Retrieves advertisements based on context.
   - **Request**:
     - **Type**: `AdRequest`
     - **Fields**:
       - `ContextKeys` (array): List of context keys for ad targeting.
   - **Response**:
     - **Type**: `AdResponse`
     - **Fields**:
       - `Ads` (array): List of ads.
         - `RedirectUrl` (string): The URL to redirect to when the ad is clicked.
         - `Text` (string): The ad text.
   - **Example Request**:
     ```json
     {
       "ContextKeys": ["electronics", "sale"]
     }
     ```
   - **Example Response**:
     ```json
     {
       "Ads": [
         {
           "RedirectUrl": "http://example.com",
           "Text": "Great deals on electronics!"
         }
       ]
     }
     ```

### Authentication and Authorization
- **Authentication**: Typically handled at the gRPC level, often using tokens or certificates.
- **Authorization**: Ensures that the user has permission to view ads.

### Data Models

- **AdRequest**
  - **Fields**:
    - `ContextKeys`: array of strings

- **AdResponse**
  - **Fields**:
    - `Ads`: array of objects
      - `RedirectUrl`: string
      - `Text`: string

This documentation provides a comprehensive overview of the API, covering all aspects of each service and endpoint. Further details can be added as needed.
