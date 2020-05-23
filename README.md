# eSIS Partner API v1

> _**NOTE**: This document is working version of the eSIS Partner API documentation. It will be changed, updated and improved in the coming days based on the more information, suggestions and limitations we gather from both our developers and our partners._

<!-- Intro
Document conventions
Authentication
Request format
Response format
200 range
400 range
500 range
Pagination
Products
List Products
Filters
Show Product
Create Product
Create Or Update Product
Example Response
Create Or Update Many Products
Update
Delete
Delete Many Products
Sync All Products -->

## Intro

The eSIS Partner API:
- Is RESTful
- Uses JWT for machine to machine authorization.
- Always returns responses in JSON.

### Document conventions

Endpoints are described with an HTTP method and a path. Example:

```
GET /api/v1/products
```

Prepend your eSIS Partner URL to the path to get the full endpoint URL. In example, if your Partner URL is https://company.esis-platform.com, then use the following endpoint URL:
```
GET https://company.esis-platform.com/api/v1/products
```

Curly braces, {}, in the path indicate a placeholder value that you must replace with your use case specific value. Example:

```
GET /api/v1/products/{external_id}
```

The body of requests and responses for each resource is described in a JSON format table. Each table lists a resource's properties, their data types, whether or not they're required, and descriptions.

### Authentication

Client must be a verified partner to make API requests. Partner can authorize against the API using a JWT access token that is provided for partner’s use.

> @TODO Document:
- [x] How to authenticate requests
- [x] Error messages related to invalid authentication
- [ ] Sensitivity around authentication information

To retrieve or store data with ESIS API partner’s app first need to authenticate with JWT bearer token. Each request must be authenticated. Clients can include JWT in HTTP header `Authorization: Bearer {token}`.

If a client fails to include a valid access token, it will receive a 401 response with an error message `Unauthorized`.

```json
{
  "error": "Unauthorized"
}
```

### Request format

The eSIS Partner API is a HTTP JSON API.
- Clients must supply a `Content-Type: application/json` header in PUT and POST requests.
- Clients must set an `Accept: application/json` header on all requests.
- Clients may get a `text/plain` response in case of an error like a bad request.

The documented JSON properties for this API are case sensitive.

### Response format

The eSIS Partner API responds to successful requests with HTTP status codes in the 200 or 300 range. When you create or update a resource, the API renders the resulting JSON representation in the response body ~~and sets a Location header pointing to the resource~~.

#### 200 range
The request was successful. The status is:
- 200 for successful GET, PUT, PATCH, DELETE requests
- 201 for most POST requests

#### 400 range
The request was not successful. The content type of the response *may* be `text/plain` for API-level error messages, such as when trying to call the API without SSL. The content type is `application/json` for business-level error messages because the response includes a JSON object with information about the error.

#### 500 range
~~A 503 response with a Retry-After header indicates a database timeout or deadlock. You can retry your request after the number of seconds specified in the Retry-After header.~~

~~If the 503 response doesn't have a Retry-After header, eSIS Partner API may be experiencing internal issues or undergoing scheduled maintenance. In such cases, check with support (support@esisapp.com) for any known issues.~~

We recommend treating any 500 status codes as a warning or temporary state. However, if the status persists and we don't have a publicly announced maintenance or service disruption, contact us at support@esis-platform.com.

#### Pagination

> _**NOTE:** Pagination is still in development._

By default, list endpoints return a maximum of *500* records per page. You can change the number of records on a per-request basis by passing a limit parameter in the request URL parameters. Also, you can specify offset parameter for skipping any number of results. Example:

```
GET /api/v1/products?offset=150&limit=150
```

However, you can't exceed *500* records per page.

## Products
> @TODO DOCUMENT:
- [ ] Product resource and it’s fields.

Example product:
```json
{
  "external_id": "10001",
  "sku": "SM-A415FZBDEUF",
  "ean": "8806090419157",
  "mpn": null,
  "price": 36990.00,
  "special_price": null,
  "special_from_date": null,
  "special_to_date": null,
  "is_in_stock": true,
  "stock_qty": null,
  "extra": null
}
```

<!-- Field
Type
Requirements
Description
sku
String
One of (sku, ean, mpn) fields is required.
Samsung’s product SKU (global)
ean
String
One of (sku, ean, mpn) fields is required.
Samsung’s product EAN
mpn
String
One of (sku, ean, mpn) fields is required.
Samsung’s product MPN
external_id
String
Required
Partner’s product ID
price
Number
Required
Partner’s listed price for the product.
special_price
Number
No
Partner’s discounted price for the product.
special_from_date
Date
No
Start of the period where discounted price is applied.
special_to_date
Date (ISO ???)
No
End of the period where discounted price is applied.
is_in_stock
Bool
One of (is_in_stock, stock_qty) fields is required.
Flag for having the product in partner’s stock.
stock_qty
Number
One of (is_in_stock, stock_qty) fields is required.
Number of products that the partner has in stock.
extra
Object
No
A container object for extra data on a product specific to a partner. -->

### List Products
```
GET /api/v1/products
```
List partner’s products.

#### Parameters

- **offset** - How many results to skip
  - Optional
  - Default: 0


- **limit** - How many results to take
  - Optional
  - Default: 100

##### Filters
> @TODO Document available filters for the list endpoint.

```
Status: 200 OK

{
    "status": "success",
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
        "extra": {
          "loyalty_poitns": 34
        }
      }
    ],
    "message": "Request Successful"
}
```

### Show Product
```
GET /api/v1/products/{external_id}
```
Get a single partner’s product by `external_id`.

#### Parameters

- **external_id** - Partner’s product ID
  - Required

### Create Product
```
POST /api/v1/products
```
Creates new partner’s product.

#### Example request
```
Authorization: Bearer {token}
Content-Type: application/json
Accept: application/json
```
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

### Create Or Update Product
```
POST /api/v1/products/create_or_update
```
Creates new partner’s product if the product does not already exist, or updates an existing product identified by `external_id`.

#### Example Request
```
Authorization: Bearer {token}
Content-Type: application/json
Accept: application/json
```
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

```
Status: 201 Created
Location: /api/v1/products/{new-product-sku}

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

```
Status: 200 OK
Location: /api/v1/products/{existing-product-sku}

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
      "external_id": "10001",
      "sku": "SM-A415ZFBDEUF",
      "ean": "8806090419158",
      ...
    },
    ...
  ]
}
```

#### Example response:
```
Status: 200 OK

{
  "affected": 140,
  "created": 100,
  "updated": 40,
  "failed": 10
}
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

### Delete
```
DELETE /api/v1/products/{external_id}
```

#### Parameters

- **external_id** - Partner’s product ID
  - Required

### Delete Many Products
```
DELETE /api/v1/products/delete_many
```

### Sync All Products
```
POST /api/v1/products/sync_all
```

Accepts an array of up to *1000* product objects. For each product, the product is created if it does not already exist, or the existing product is updated.

> **NOTE: If there were existing products in database not referenced in the request they will be treated as they are not longer available from partner and therefore deleted from eSIS platform.**

This endpoint is proposed for use cases where it’s easier for a partner to send complete list of currently available products.

### Example request
```json
{
  "products": [
    {
      "external_id": "10001",
      "sku": "SM-A415FZBDEUF",
      "ean": "8806090419157",
      "mpn": null,
      "price": 36990.00,
      "special_price": null,
      "special_from_date": null,
      "special_to_date": null,
      "is_in_stock": true,
      "stock_qty": null,
      "extra": null
    },
    {
      "external_id": "10002",
      "sku": "SM-A415FZBDEUF",
      "ean": "8806090419157",
      ...
    },
    ...
  ]
}
```

### Example response
```
Status: 200 OK

{
  "affected": 150,
  "created": 75,
  "updated": 50,
  "deleted": 25
}
```
