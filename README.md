# API Documentation

## Endpoints

### Home Endpoint

- **Path:** `/`
- **Method:** GET
- **Description:** Retrieves the home page with a list of products, currencies, and cart details.
- **Authentication:** None required.
- **Request Parameters:**
  - **Path Parameters:** None
  - **Query Parameters:** None
  - **Request Body Parameters:** None
- **Response Format:**
  - **Success Response:**
    - **Status Code:** 200 OK
    - **Sample JSON Response:**
      ```json
      {
        "show_currency": true,
        "currencies": [...],
        "products": [...],
        "cart_size": 0,
        "banner_color": "string",
        "ad": {...}
      }
      ```
    - **Description:** Returns the home page data including products and cart size.
  - **Error Responses:**
    - **Status Code:** 500 Internal Server Error
    - **Error Message Format:** JSON with error details
- **Rate Limits:** None specified.
- **Dependencies:** Requires access to product and cart services.

### Product Endpoint

- **Path:** `/product/{id}`
- **Method:** GET
- **Description:** Retrieves details of a specific product by ID.
- **Authentication:** None required.
- **Request Parameters:**
  - **Path Parameters:**
    - `id` (string, required): The ID of the product.
  - **Query Parameters:** None
  - **Request Body Parameters:** None
- **Response Format:**
  - **Success Response:**
    - **Status Code:** 200 OK
    - **Sample JSON Response:**
      ```json
      {
        "product": {...},
        "currencies": [...],
        "recommendations": [...],
        "cart_size": 0,
        "packagingInfo": {...}
      }
      ```
    - **Description:** Returns product details, recommendations, and cart size.
  - **Error Responses:**
    - **Status Code:** 400 Bad Request, 500 Internal Server Error
    - **Error Message Format:** JSON with error details
- **Rate Limits:** None specified.
- **Dependencies:** Requires access to product, currency, and recommendation services.

### Add to Cart Endpoint

- **Path:** `/cart`
- **Method:** POST
- **Description:** Adds a product to the cart.
- **Authentication:** None required.
- **Request Parameters:**
  - **Path Parameters:** None
  - **Query Parameters:** None
  - **Request Body Parameters:**
    - `quantity` (integer, required): The quantity of the product to add.
    - `product_id` (string, required): The ID of the product.
- **Response Format:**
  - **Success Response:**
    - **Status Code:** 302 Found
    - **Headers:** Location header set to `/cart`
  - **Error Responses:**
    - **Status Code:** 422 Unprocessable Entity, 500 Internal Server Error
    - **Error Message Format:** JSON with error details
- **Rate Limits:** None specified.
- **Dependencies:** Requires access to product and cart services.

### Empty Cart Endpoint

- **Path:** `/cart/empty`
- **Method:** POST
- **Description:** Empties the user's cart.
- **Authentication:** None required.
- **Request Parameters:**
  - **Path Parameters:** None
  - **Query Parameters:** None
  - **Request Body Parameters:** None
- **Response Format:**
  - **Success Response:**
    - **Status Code:** 302 Found
    - **Headers:** Location header set to `/`
  - **Error Responses:**
    - **Status Code:** 500 Internal Server Error
    - **Error Message Format:** JSON with error details
- **Rate Limits:** None specified.
- **Dependencies:** Requires access to cart services. 
