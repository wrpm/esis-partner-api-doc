
# Alt Prices [CRO] - Dual currency and price text

> **Warning**
>
> **This section only applies to Croatian partners**

---
**Goal**

- Show product prices in two currencies at the same time (HRK and EUR).
- Show custom text related to the `price` field
  - for products with `special_price` (where `price` field is crossed out )
  - (example: "najniža cijena u posljednjih 30 dana")

---

## Summary

For product with price, special price, and price text as in table below

|  | HRK | EUR | Note |
| --- | --- | --- | --- |
| price | 13999.00 HRK | 1857.99 EUR | "najniža cijena u posljednjih 30 dana" |
| special_price | 12999.00 HRK | 1725.26 EUR |  |

for which the display would be something similar to

> **12999.00 HRK** ~~13999.00 HRK~~ \*
>
> **1725.26 EUR** ~~1857.99 EUR~~ \*
>
> \* najniža cijena u posljednjih 30 dana

partners should send a product object (JSON):
```json
{
  "external_id": "10001",
  "sku": "SM-F936BZABEUE",
  "ean": "8806094504972",
  "mpn": null,
  "price": 13999.00,
  "price_text": "najniža cijena u posljednjih 30 dana",
  "special_price": 12999.00,
  "special_from_date": "2022-08-14T22:00:00.000Z",
  "special_to_date": "2022-08-31T21:59:59.000Z",
  "is_in_stock": true,
  "stock_qty": 5,
  "alt_prices": [
    {
      "price": 1857.99,
      "special_price": 1725.26,
      "currency": "EUR"
    }
  ],
  "extra": null
}
```

---

## New fields


### Field: `alt_prices`

Supports multiple prices in different currencies.

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `alt_prices` | Array | optional | Array of _AltPrice_ objects |

###### AltPrice Object

Example:
```json
{
  "price": 1857.99,
  "special_price": 1725.26,
  "currency": "EUR"
}
```

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `price` | Number | required |  |
| `special_price` | Number | optional, required if the product has `special_price` |  |
| `currency` | String | required | 3 letter currency codes (ISO 4217) |


##### Example product with a `price` (HRK and EUR):

|  | HRK | EUR | Note |
| --- | --- | --- | --- |
| price | 13999.00 HRK | 1857.99 EUR |  |

JSON:
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
  "alt_prices": [
    {
      "price": 1857.99,
      "currency": "EUR"
    }
  ],
  "extra": null
}
```

##### Example product with a `special_price` (HRK and EUR):

|  | HRK | EUR | Note |
| --- | --- | --- | --- |
| price | 13999.00 HRK | 1857.99 EUR |  |
| special_price | 12999.00 HRK | 1725.26 EUR |  |

JSON:
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
  "alt_prices": [
    {
      "price": 1857.99,
      "special_price": 1725.26,
      "currency": "EUR"
    }
  ],
  "extra": null
}
```

---

#### Field: `price_text`

Supports custom text related to the product price (`price` field).


| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `price_text` | String | optional | Optional text explaining price (`price` field), usually for products with `special_price`  |


##### Example with field `price` and `alt_prices`

```json
{
  "external_id": "10001",
  "sku": "SM-F936BZABEUE",
  "ean": "8806094504972",
  "mpn": null,
  "price": 13999.00,
  "price_text": "Lowest price in the last 30 days",
  "special_price": null,
  "special_from_date": null,
  "special_to_date": null,
  "is_in_stock": true,
  "stock_qty": 12,
  "alt_prices": [
    {
      "price": 1857.99,
      "currency": "EUR"
    }
  ]
}
```

##### Example with field `special_price` and `alt_prices`

```json
{
  "external_id": "10001",
  "sku": "SM-F936BZABEUE",
  "ean": "8806094504972",
  "mpn": null,
  "price": 13999.00,
  "price_text": "Lowest price in the last 30 days",
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
  ]
}
```
