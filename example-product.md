
# Example Product JSON

- Basic
- Special price
- Special price and price text
- Alt prices
- Instalments
- Extra
- Full

---


### Basic

Example product with a regular price:
```json
{
  "external_id": "10001",
  "sku": "SM-F936BZABEUE",
  "ean": "8806094504972",
  "mpn": null,
  "price": 13999.00,
  "special_price": null,
  "special_from_date": null,
  "special_to_date": null,
  "is_in_stock": true,
  "stock_qty": 5,
  "extra": null
}
```

### Special price

| Field | Type | Description |
| --- | --- | --- |
| `price` | Number |  |
| `special_price` | Number |  |
| `special_from_date` | String (ISO 8601 datetime) |  |
| `special_to_date` | String (ISO 8601 datetime) |  |

Example product with a special price:
```json
{
  "external_id": "10001",
  "sku": "SM-F936BZABEUE",
  "ean": "8806094504972",
  "mpn": null,
  "price": 13999.00,
  "special_price": 12999.00,
  "special_from_date": null,
  "special_to_date": null,
  "is_in_stock": true,
  "stock_qty": 5,
  "extra": null
}
```

Example product with a special price active in specified date-time range:
```json
{
  "external_id": "10001",
  "sku": "SM-F936BZABEUE",
  "ean": "8806094504972",
  "mpn": null,
  "price": 13999.00,
  "special_price": 12999.00,
  "special_from_date": "2022-08-14T22:00:00.000Z",
  "special_to_date": "2022-08-31T21:59:59.000Z",
  "is_in_stock": true,
  "stock_qty": 5,
  "extra": null
}
```

### Special price and price text

| Field | Type | Description |
| --- | --- | --- |
| `price` | Number |  |
| `price_text` | Number |  |
| `special_price` | Number |  |
| `special_from_date` | Date (ISO 8601) |  |
| `special_to_date` | Date (ISO 8601) |  |

Example product with a special price:
```json
{
  "external_id": "10001",
  "sku": "SM-F936BZABEUE",
  "ean": "8806094504972",
  "mpn": null,
  "price": 13999.00,
  "price_text": "Lowest price in previous 30 days",
  "special_price": 12999.00,
  "special_from_date": null,
  "special_to_date": null,
  "is_in_stock": true,
  "stock_qty": 5,
  "extra": null
}
```

Example product with a special price active in specified date-time range:
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
  "stock_qty": 5,
  "extra": null
}
```

### Instalments

Example product with option of payment in instalments (12 or 24 months):
```json
{
  "external_id": "10001",
  "sku": "SM-F936BZABEUE",
  "ean": "8806094504972",
  "mpn": null,
  "price": 13999.00,
  "special_price": null,
  "special_from_date": null,
  "special_to_date": null,
  "is_in_stock": true,
  "stock_qty": 5,
  "instalments": [
    {
      "amount": 1166.58,
      "period": 12
    },
    {
      "amount": 583.29,
      "period": 24
    }
  ],
  "extra": null
}
```

### Extra

Example product with an extra data - loyalty points:
```json
{
  "external_id": "10001",
  "sku": null,
  "ean": "8806090419157",
  "mpn": null,
  "price": 36990.00,
  "special_price": 34990.00,
  "special_from_date": null,
  "special_to_date": null,
  "is_in_stock": true,
  "stock_qty": 15,
  "extra": {
    "loyalty_points": 34
  }
}
```

> **Note**
> `loyalty_points` - it's just an example of custom data from a partner, it could be anything else.
>
> Extra data has to be communicated and approved before or during the integration process in order to be accepted and used in ESIS App.

### Full

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
      "price_text": "Lowest price in previous 30 days",
      "special_price": 1725.26,
      "currency": "EUR"
    }
  ],
  "instalments": [
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

---

Datetime format
- ISO 8601
- Example: "2022-08-31T18:00:00.000Z"

currency - 3-letter ISO code
- [ISO 4217 - Wiki](https://en.wikipedia.org/wiki/ISO_4217)
