
# Examples: Product (JSON)

- [Basic](#basic)
- [Special price](#special-price)
- [Special price and price text](#special-price-and-price-text)
- [Alt prices](#alt-prices)
- [Installments](#installments)
- [Extra](#extra)
- [Full](#full)

---
### <a name="basic"></a> Basic

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

---
### <a name="special-price"></a> Special price

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

| Field | Format | Description |
| --- | --- | --- |
| `price` | Number |  |
| `special_price` | Number |  |
| `special_from_date` | Datetime (ISO 8601) |  |
| `special_to_date` | Datetime (ISO 8601) |  |

---
### <a name="special-price-and-price-text"></a> Special price and price text

Example product with a special price:
```json
{
  "external_id": "10001",
  "sku": "SM-F936BZABEUE",
  "ean": "8806094504972",
  "mpn": null,
  "price": 13999.00,
  "price_text": "Lowest price in the last 30 days",
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
  "price_text": "Lowest price in the last 30 days",
  "special_price": 12999.00,
  "special_from_date": "2022-08-14T22:00:00.000Z",
  "special_to_date": "2022-08-31T21:59:59.000Z",
  "is_in_stock": true,
  "stock_qty": 5,
  "extra": null
}
```

| Field | Format | Description |
| --- | --- | --- |
| `price` | Number |  |
| `price_text` | String |  |
| `special_price` | Number |  |
| `special_from_date` | Datetime (ISO 8601) |  |
| `special_to_date` | Datetime (ISO 8601) |  |

---
### <a name="alt-prices"></a> Alt prices

Example product with price and alt price in EUR:
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

Example product with price, special_price, price_text, and alt price in EUR:
```json
{
  "external_id": "10001",
  "sku": "SM-F936BZABEUE",
  "ean": "8806094504972",
  "mpn": null,
  "price": 13999.00,
  "price_text": "Najniža cijena u zadnjih 30 dana",
  "special_price": 12999.00,
  "special_from_date": null,
  "special_to_date": null,
  "is_in_stock": true,
  "stock_qty": 5,
  "alt_prices": [
    {
      "price": 1857.99,
      "price_text": "Lowest price in the last 30 days",
      "special_price": 1725.26,
      "currency": "EUR"
    }
  ],
  "extra": null
}
```

| Field | Format | Description |
| --- | --- | --- |
| `alt_prices` | Array |  |

#### Alt price object

Example
```json
{
  "price": 1857.99,
  "price_text": "Lowest price in the last 30 days",
  "special_price": 1725.26,
  "currency": "EUR"
}
```

| Field | Format | Description |
| --- | --- | --- |
| `price` | Number | Required |
| `price_text` | String |  |
| `special_price` | Number | Required if the product has special price |
| `currency` | String | Required |

---
### <a name="installments"></a> Installments

Example product with option of payment in installments (12 or 24 months):
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
  "installments": [
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

| Field | Format | Description |
| --- | --- | --- |
| `installments` | Array |  |

#### Installment object

Example
```json
{
  "amount": 1166.58,
  "period": 12
}
```

| Field | Format | Description |
| --- | --- | --- |
| `amount` | Number |  |
| `period` | Number |  |

---
### <a name="extra"></a> Extra

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
>
> - `loyalty_points` - it's just an example of custom data from a partner, it could be anything else.
> - Extra data has to be communicated and approved before or during the integration process in order to be accepted and used in ESIS App.

---
### <a name="full"></a> Full

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
      "price_text": "Lowest price in the last 30 days",
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
