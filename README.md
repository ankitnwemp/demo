# API Documentation

## Overview

### Frontend Service
The `frontend` service is responsible for handling user interactions and serving the web interface. It connects to various backend services to fetch and display data.

## Modules

### Module: `main.go`
- **Purpose**: This module initializes the frontend server, sets up routes, and manages connections to other services.
- **Dependencies and Imports**:
  - `context`, `fmt`, `net/http`, `os`, `time` for standard operations.
  - `cloud.google.com/go/profiler` for profiling.
  - `github.com/gorilla/mux` for routing.
  - `github.com/pkg/errors` for error handling.
  - `github.com/sirupsen/logrus` for logging.
  - `go.opentelemetry.io` packages for tracing.
  - `google.golang.org/grpc` for gRPC connections.
- **Configuration Options**:
  - Environment variables for service addresses and enabling tracing/profiling.

## Classes

### Class: `frontendServer`
- **Description**: Manages connections to various backend services.
- **Constructor Parameters**: None explicitly defined; initialized in `main`.
- **Properties**:
  - `productCatalogSvcAddr`, `currencySvcAddr`, `cartSvcAddr`, etc.: Addresses for respective services.
  - `productCatalogSvcConn`, `currencySvcConn`, etc.: gRPC connections to services.
- **Methods**:
  - `main()`: Initializes the server, sets up routes, and starts the HTTP server.
  - `initStats(log logrus.FieldLogger)`: Placeholder for initializing stats.
  - `initTracing(log logrus.FieldLogger, ctx context.Context, svc *frontendServer)`: Sets up tracing.
  - `initProfiling(log logrus.FieldLogger, service, version string)`: Initializes profiling.
  - `mustMapEnv(target *string, envKey string)`: Maps environment variables to service addresses.
  - `mustConnGRPC(ctx context.Context, conn **grpc.ClientConn, addr string)`: Establishes gRPC connections.

## Functions

### `main()`
- **Description**: Entry point for the frontend service. Sets up logging, tracing, profiling, and starts the HTTP server.
- **Parameters**: None.
- **Return Values**: None.
- **Exceptions Thrown**: Panics if environment variables are not set or gRPC connections fail.
- **Usage Example**:
  ```go
  func main() {
      // Initialize and start the frontend server
  }
  ```

### `initTracing()`
- **Description**: Initializes OpenTelemetry tracing.
- **Parameters**:
  - `log`: Logger for output.
  - `ctx`: Context for operations.
  - `svc`: Frontend server instance.
- **Return Values**: Tracer provider and error.
- **Exceptions Thrown**: Logs warning if trace exporter creation fails.
- **Usage Example**:
  ```go
  initTracing(log, ctx, svc)
  ```

### `initProfiling()`
- **Description**: Initializes Stackdriver profiling.
- **Parameters**:
  - `log`: Logger for output.
  - `service`: Service name.
  - `version`: Service version.
- **Return Values**: None.
- **Exceptions Thrown**: Logs warning if profiler initialization fails.
- **Usage Example**:
  ```go
  initProfiling(log, "frontend", "1.0.0")
  ```

### `mustMapEnv()`
- **Description**: Maps environment variables to service addresses.
- **Parameters**:
  - `target`: Pointer to the target string.
  - `envKey`: Environment variable key.
- **Return Values**: None.
- **Exceptions Thrown**: Panics if environment variable is not set.
- **Usage Example**:
  ```go
  mustMapEnv(&svc.productCatalogSvcAddr, "PRODUCT_CATALOG_SERVICE_ADDR")
  ```

### `mustConnGRPC()`
- **Description**: Establishes gRPC connections.
- **Parameters**:
  - `ctx`: Context for operations.
  - `conn`: Pointer to the gRPC connection.
  - `addr`: Address of the service.
- **Return Values**: None.
- **Exceptions Thrown**: Panics if gRPC connection fails.
- **Usage Example**:
  ```go
  mustConnGRPC(ctx, &svc.currencySvcConn, svc.currencySvcAddr)
  ```

## REST API Endpoints

- **`GET /`**: Home page.
- **`GET /product/{id}`**: Fetch product details.
- **`GET /cart`**: View cart.
- **`POST /cart`**: Add to cart.
- **`POST /cart/empty`**: Empty cart.
- **`POST /setCurrency`**: Set currency.
- **`GET /logout`**: Logout.
- **`POST /cart/checkout`**: Checkout.
- **`GET /assistant`**: Shopping assistant.
- **`GET /product-meta/{ids}`**: Fetch product metadata.
- **`POST /bot`**: Chatbot interaction. 
