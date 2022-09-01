
# eSIS Partner API v1

> Sometimes referred as "ESIS Sync API"

- [Documentation](README.md)
  - [Intro](#intro)
    - [Document conventions](#document-conventions)
    - [Authentication](#authentication)
    - [Request format](#request-format)
    - [Response format](#response-format)
  - [Products](#products)
  - [Products API](#products-api)


- [Examples - product json](example-product.md)

- [Alt Prices](alt-prices.md)


---

## <a name="intro"></a> Intro

The eSIS Partner API:
- Is RESTful
- Uses JWT for machine to machine authentication.
- Always returns responses in JSON.

### <a name="document-conventions"></a> Document conventions

Endpoints are described with an HTTP method and a path. Example:

```
GET /api/v1/products
```

Prepend your eSIS Partner URL to the path to get the full endpoint URL. In example, if your Partner URL is https://company.esis-platform.com, then use the following endpoint URL:
```
GET https://company.esis-platform.com/api/v1/products
```

Curly braces, `{}`, in the path indicate a placeholder value that you must replace with your use case specific value. Example:

```
GET /api/v1/products/{external_id}
```

The body of requests and responses for each resource is described in a JSON format table. Each table lists a resource's properties, their data types, whether or not they're required, and descriptions.

### <a name="authentication"></a> Authentication

Client must be a verified partner to make API requests. Partner can authorize against the API using a JWT access token that is provided for partner’s use.

To retrieve or store data with ESIS API partner’s app first need to authenticate with JWT bearer token. Each request must be authenticated. Clients can include JWT in HTTP header `Authorization: Bearer {token}`.

If a client fails to include a valid access token, it will receive a 401 response with an error message `Unauthorized`.

```json
{
  "error": "Unauthorized"
}
```

### <a name="request-format"></a> Request format

The eSIS Partner API is a HTTP JSON API.
- Clients must supply a `Content-Type: application/json` header in PUT and POST requests.
- Clients must set an `Accept: application/json` header on all requests.
- Clients may get a `text/plain` response in case of an error like a bad request.

The documented JSON properties for this API are case sensitive.

### <a name="response-format"></a> Response format

The eSIS Partner API responds to successful requests with HTTP status codes in the 200 or 300 range. When you create or update a resource, the API renders the resulting JSON representation in the response body.

#### 200 range
The request was successful. The status is:
- 200 for successful GET, PUT, PATCH, DELETE requests
- 201 for most POST requests

#### 400 range
The request was not successful. The content type of the response *may* be `text/plain` for API-level error messages, such as when trying to call the API without SSL. The content type is `application/json` for business-level error messages because the response includes a JSON object with information about the error.

#### 500 range

We recommend treating any 500 status codes as a warning or temporary state. However, if the status persists and we don't have a publicly announced maintenance or service disruption, contact us at support@esis-platform.com.

---

## <a name="products"></a> Products

**Basic** example of a product object (JSON):
```json
{
  "external_id": "10001",
  "sku": "SM-A415FZBDEUF",
  "ean": null,
  "mpn": null,
  "price": 36990.00,
  "special_price": null,
  "special_from_date": null,
  "special_to_date": null,
  "is_in_stock": true,
  "stock_qty": null,
  "extra": {}
}
```

**Full** example of a product object (JSON):
```json
{
  "external_id": "10001",
  "sku": "SM-F936BZABEUE",
  "ean": "8806094504972",
  "mpn": null,
  "price": 13999.00,
  "price_text": "Lowest price in previous 30 days",
  "special_price": 12999.00,
  "special_from_date": "2022-08-14T22:00:00.000Z",
  "special_to_date": "2022-08-31T21:59:59.000Z",
  "is_in_stock": true,
  "stock_qty": 12,
  "alt_prices": [
    {
      "price": 1857.99,
      "special_price": 1725.26,
      "currency": "EUR"
    }
  ],
  "installments": [
    {
      "amount": 1083.25,
      "period": 12
    },
    {
      "amount": 541.625,
      "period": 24
    }
  ],
  "extra": {
    "loyalty_points": 5
  }
}
```

### Product data fields

| Field | Type |  |
| --- | --- | --- |
| `external_id` | String \| Number | Required |
| `sku` | String | Required* |
| `ean` | String \| Number | Required* |
| `mpn` | String \| Number |  |
| `price` | String | Required |
| `price_text` | String |  |
| `special_price` | Number |  |
| `special_from_date` | String |  |
| `special_to_date` | String |  |
| `is_in_stock` | Boolean | Required |
| `stock_qty` | Number |  |
| `alt_prices` | Array |  |
| `installments` | Array |  |
| `extra` | Object |  |

\* you MUST provide either `sku` or `ean`. if available, it is recommended to send both.

##### SKU

> **Note**
> `sku` MUST be a Samsung's model code.

Examples
```
SM-A415FZBDEUF
QE75QN900BTXXH
RB34A7B5E22/EZ
```

##### Dates

Example
```
2022-08-31T21:59:59.000Z
```

Syntax
- Max 25 alphanumeric characters
- ISO 8601  
  - YYYY-MM-DDThh:mmZ

---

## <a name="products-api"></a> Products API

### List
```
GET /api/v1/products
```

List all products.

#### Parameters

- **offset** - How many results to skip
  - Optional
  - Default: 0


- **limit** - How many results to take
  - Optional
  - Default: 100


#### Example response

Status: 200 OK
```json
{
  "status": "success",
  "message": "Request Successful",
  "data": [
    {
      "external_id": "10001",
      "sku": "SM-A415FZBDEUF",
      "ean": "8806090419157",
      "mpn": null,
      "price": 36990.00,
      "special_price": 34990.00,
      "special_from_date": null,
      "special_to_date": null,
      "is_in_stock": true,
      "stock_qty": 15,
      "extra": {}
    },
    {
      "external_id": "10002",
      "sku": "SM-A415FZBDEUF",
      "ean": "8806090419157",
      "mpn": null,
      "price": 36990.00,
      "special_price": 34990.00,
      "special_from_date": null,
      "special_to_date": null,
      "is_in_stock": true,
      "stock_qty": 7,
      "extra": {
        "loyalty_poitns": 34
      }
    }
  ]
}
```

### Show
```
GET /api/v1/products/{external_id}
```

Get a single product by `external_id`.

#### Parameters

- **external_id** - Partner’s product ID
  - Required

#### Example responses

Status: 200 OK
```json
{
    "status": "success",
    "data": {
      "external_id": "10001",
      "sku": "SM-A415FZBDEUF",
      "ean": "8806090419157",
      "mpn": null,
      "price": 36990.00,
      "special_price": 34990.00,
      "special_from_date": null,
      "special_to_date": null,
      "is_in_stock": true,
      "stock_qty": 15,
      "extra": {
        "loyalty_poitns": 34
      }
    },
    "message": "Request Successful"
}
```

Status: 404 Not Found
```json
{
    "status": "failed",
    "message": "Product not found",
    "data": {}
}
```

### Create Product
```
POST /api/v1/products
```

Create a new product.

#### Example request
Headers
```
Authorization: Bearer {token}
Content-Type: application/json
Accept: application/json
```
Body
```json
{
  "external_id": "10001",
  "sku": "SM-A415FZBDEUF",
  "ean": "8806090419157",
  "mpn": null,
  "price": 36990.00,
  "special_price": 34990.00,
  "special_from_date": null,
  "special_to_date": null,
  "is_in_stock": true,
  "stock_qty": 15,
  "extra": {
    "loyalty_poitns": 34
  }
}
```

#### Example responses

Status: 201 Created
```json
{
  "status": "success",
  "data": {
    "_id": "5ec92239ec3f2a53cf0a1991",
    "external_id": "10001",
    "sku": "SM-A415FZBDEUF",
    "ean": "8806090419157",
    "mpn": "",
    "price": 36990.00,
    "special_price": 34990.00,
    "special_from_date": null,
    "special_to_date": null,
    "is_in_stock": true,
    "stock_qty": null,
    "extra": {
      "loyalty_points": 34
    },
    "createdAt": "2020-05-23T13:16:41.797Z",
    "updatedAt": "2020-05-23T13:16:41.797Z",
    "__v": 0
  },
  "message": "Request Successful"
}
```

Status: 400 Bad Request
```json

{
    "status": "failed",
    "message": "Invalid request",
    "data": {}
}
```

Status: 422 Unprocessable Entity
```json
{
  "status": "failed",
  "data": {
    "details": [
      {
        "message": "\"price\" must be a number",
        "path": [
          "price"
        ]
      }
    ]
  },
  "message": "\"price\" must be a number"
}
```

### Create Or Update Product
```
POST /api/v1/products/create_or_update
```
Creates new partner’s product if the product does not already exist, or updates an existing product identified by `external_id`.

#### Example Request
```json
{
  "external_id": "10001",
  "sku": "SM-A415FZBDEUF",
  "ean": "8806090419157",
  "mpn": null,
  "price": 36990.00,
  "special_price": 34990.00,
  "special_from_date": null,
  "special_to_date": null,
  "is_in_stock": true,
  "stock_qty": 15,
  "extra": {
    "loyalty_poitns": 34
  }
}
```

#### Example Response

If the product was created:

Status: 201 Created
```json
{
    "status": "success",
    "data": {
      "external_id": "10001",
      "sku": "SM-A415FZBDEUF",
      "ean": "8806090419157",
      "mpn": null,
      "price": 36990.00,
      "special_price": 34990.00,
      "special_from_date": null,
      "special_to_date": null,
      "is_in_stock": true,
      "stock_qty": 15,
      "extra": {
        "loyalty_poitns": 34
      }
    },
    "message": "Request Successful"
}
```

If an existing product was updated:

Status: 200 OK
```json
{
    "status": "success",
    "data": {
      "external_id": "10001",
      "sku": "SM-A415FZBDEUF",
      "ean": "8806090419157",
      "mpn": null,
      "price": 36990.00,
      "special_price": 34990.00,
      "special_from_date": null,
      "special_to_date": null,
      "is_in_stock": true,
      "stock_qty": 15,
      "extra": {
        "loyalty_poitns": 34
      }
    },
    "message": "Request Successful"
}
```

### Create Or Update Many Products
```
POST /api/v1/products/create_or_update_many
```

Accepts an array of up to *1000* product objects. For each product, the product is created if it does not already exist, or the existing product is updated.

Each individual product object can identify an existing product by ~~sku, ean or by~~ external_id.

#### Example Request
```json
{
  "products": [
    {
      "external_id": "10001",
      "sku": "SM-A415FZBDEUF",
      "ean": "8806090419157",
      "mpn": null,
      "price": 36990.00,
      "special_price": 34990.00,
      "special_from_date": null,
      "special_to_date": null,
      "is_in_stock": true,
      "stock_qty": 15,
      "extra": {
        "loyalty_poitns": 34
      }
    },
    {
      "external_id": "10002",
      "sku": "SM-A415FZBDEUF",
      "ean": "8806090419157",
      "mpn": null,
      "price": 36990.00,
      "special_price": 34990.00,
      "special_from_date": null,
      "special_to_date": null,
      "is_in_stock": true,
      "stock_qty": 15,
      "extra": {}
    },
  ]
}
```

#### Example response:
```
```

### Update
```
PUT /api/v1/products/{external_id}
```

#### Parameters

- **external_id** - Partner’s product ID
  - Required


### Update (partial)
```
PATCH /api/v1/products/{external_id}
```

The PATCH method is used for partial changes to existing products.

#### Parameters

- **external_id** - Partner’s product ID
  - Required


### Delete
```
DELETE /api/v1/products/{external_id}
```
Delete an existing product by `external_id`.


#### Parameters

- **external_id** - Partner’s product ID
  - Required

#### Example responses
Status: 200 OK
```json
{
    "status": "success",
    "data": {
        "_id": "5ec91e8bec3f2b53cf0a198f",
        "external_id": "10123",
        "sku": "SM-A712FZKUSEE",
        "ean": "8806030255328",
        "mpn": "",
        "price": 1234.55,
        "special_price": null,
        "special_from_date": null,
        "special_to_date": null,
        "is_in_stock": true,
        "stock_qty": null,
        "extra": {
            "loyalty_points": 15
        },
        "createdAt": "2020-05-23T13:00:59.438Z",
        "updatedAt": "2020-05-23T13:00:59.438Z",
        "__v": 0
    },
    "message": "Request Successful"
}
```

### Delete Many Products
```
DELETE /api/v1/products/delete_many
```
Delete many products.

#### Example request body
```json
{
  "products": [
    { "external_id": 10001 },
    { "external_id": 10002 },
    { "external_id": 99999 }
  ]
}
```

#### Example responses
```json
{
  "status": "success",
  "message": "Request Successful",
  "data": {
    "deleted": 2
  }
}
```

### Sync All Products
```
POST /api/v1/products/sync_all
```

Accepts an array of up to *1000* product objects. For each product, the product is created if it does not already exist, or the existing product is updated.

> **NOTE: If there were existing products in database not referenced in the request they will be treated as they are not longer available from partner and therefore deleted from eSIS platform.**

This endpoint is proposed for use cases where it’s easier for a partner to send complete list of currently available products.

#### Example request body
```json
{
  "products": [
    {
      "external_id": "10001",
      "sku": "SM-A415FZBDEUF",
      "ean": "8806090419157",
      "mpn": "",
      "price": 36990.00,
      "special_price": null,
      "special_from_date": null,
      "special_to_date": null,
      "is_in_stock": true,
      "stock_qty": 5,
      "extra": null
    },
    {
      "external_id": "10002",
      "sku": "SM-A415FZBDEUF",
      "ean": "8806090419157",
      "mpn": "",
      "price": 36990.00,
      "special_price": null,
      "special_from_date": null,
      "special_to_date": null,
      "is_in_stock": true,
      "stock_qty": 5,
      "extra": null
    }
  ]
}
```

#### Example response

Status: 200 OK
```json
{
  "status": "success",
  "message": "Request Successful",
  "data": [
    {
      "_id": "5ec91a88ec3f2a53cf0a198d",
      "external_id": "10001",
      "sku": "SM-A415FZBDEUF",
      "ean": "8806090419157",
      "mpn": "",
      "price": 36990,
      "special_price": 34990,
      "special_from_date": null,
      "special_to_date": null,
      "is_in_stock": true,
      "stock_qty": 15,
      "extra": {},
      "__v": 0,
      "createdAt": "2020-05-23T12:43:52.709Z",
      "updatedAt": "2020-05-23T12:43:52.709Z"
    },
    {
      "_id": "3cf0a198d5ec91a88ec3f2a5",
      "external_id": "10002",
      "sku": "SM-A415FZBDEUF",
      "ean": "8806090419157",
      "mpn": "",
      "price": 36990,
      "special_price": 34990,
      "special_from_date": null,
      "special_to_date": null,
      "is_in_stock": true,
      "stock_qty": 15,
      "extra": {},
      "__v": 0,
      "createdAt": "2020-05-23T12:43:52.709Z",
      "updatedAt": "2020-05-23T12:43:52.709Z"
    }
  ]
}
```
