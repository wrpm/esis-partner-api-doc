# Example Product JSON

Example product with a regular price:
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

Example product with a discounted price and extra :
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
    "loyalty_poitns": 34
  }
}
```

Example product option of payment in installments (12 or 24 months):
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
  "installments": [
    {
      "amount": 3082.50,
      "period": 12
    },
    {
      "amount": 1541.25,
      "period": 24
    }
  ],
  "extra": null
}
