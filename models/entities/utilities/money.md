# MACH Alliance • Open Data Model Utility Object: `Money`

## Table of contents

- [MACH Alliance • Open Data Model Utility Object: `Money`](#mach-alliance--open-data-model-utility-object-money)
  - [Table of contents](#table-of-contents)
  - [Purpose](#purpose)
  - [Object: Money](#object-money)
  - [Sample Objects](#sample-objects)
    - [Sample Object: Basic Money Object](#sample-object-basic-money-object)
    - [Sample Object: Money with High Precision](#sample-object-money-with-high-precision)
    - [Sample Object: Zero Amount](#sample-object-zero-amount)
    - [Sample Object: Negative Amount (for refunds, discounts)](#sample-object-negative-amount-for-refunds-discounts)
  - [Usage Examples](#usage-examples)
    - [In Pricing Entity](#in-pricing-entity)
    - [In Cart Totals](#in-cart-totals)
    - [In Campaign Budget](#in-campaign-budget)
    - [In Exchange Rate Context](#in-exchange-rate-context)
  - [Implementation Guidelines](#implementation-guidelines)
    - [Currency Codes](#currency-codes)
    - [Precision](#precision)
    - [Validation Rules](#validation-rules)
    - [Negative Amount Usage](#negative-amount-usage)
    - [Best Practices](#best-practices)
    - [Optional Fields Usage](#optional-fields-usage)
  - [Common Currency Examples](#common-currency-examples)
  - [Related Utility Objects](#related-utility-objects)


---

## Purpose

A standardized utility object for representing monetary values and currencies across all entities in the MACH Alliance Common Data Model. This ensures consistent handling of currency amounts, precision, and formatting across commerce engines, payment systems, pricing engines, and financial reporting.

The Money utility object provides:
- Consistent currency representation
- Standardized precision handling
- Cross-system monetary value exchange
- Audit trail for financial transactions
- Support for multiple currency scenarios

---

## Object: Money

| Field       | Description                                                                    | Practice |
| ----------- | ------------------------------------------------------------------------------ | -------- |
| `amount`    | Numeric value of the monetary amount                                           | SHOULD   |
| `currency`  | ISO 4217 currency code (e.g., "EUR", "USD")                                    | SHOULD   |
| `name`      | Human-readable currency name                                                   | COULD    |
| `symbol`    | Currency symbol for display                                                    | COULD    |
| `precision` | Number of decimal places when displaying minor units like cent (0, 2, 3, etc.) | COULD    |

---

## Sample Objects

### Sample Object: Basic Money Object

```jsonc
{
  "amount": 34.95,
  "currency": "EUR"
}
```

### Sample Object: Money with High Precision

```jsonc
{
  "amount": 1234.5678,
  "currency": "USD"
}
```

### Sample Object: Zero Amount

```jsonc
{
  "amount": 0.00,
  "currency": "EUR"
}
```

### Sample Object: Negative Amount (for refunds, discounts)

```jsonc
{
  "amount": -15.50,
  "currency": "USD"
}
```

---

## Usage Examples

### In Pricing Entity

```jsonc
{
  "id": "PRICE-001",
  "product_id": "PROD-001",
  "list_price": {
    "amount": 39.95,
    "currency": "EUR"
  },
  "sale_price": {
    "amount": 34.95,
    "currency": "EUR"
  }
}
```

### In Cart Totals

```jsonc
{
  "totals": {
    "subtotal": 69.90,
    "discount": 5.00,
    "shipping": 5.00,
    "tax": 12.00,
    "grand_total": 81.90,
    "currency": "EUR"
  }
}
```

### In Campaign Budget

```jsonc
{
  "id": "CAMPAIGN-001",
  "name": "Spring Sale 2024",
  "budget": {
    "amount": 50000.00,
    "currency": "EUR"
  }
}
```

### In Exchange Rate Context

```jsonc
{
  "exchangeRates": [
    {
      "from": {
        "currency": "EUR",
        "name": "Euro",
        "symbol": "€",
        "precision": 2
      },
      "to": {
        "currency": "USD",
        "name": "US Dollar",
        "symbol": "$",
        "precision": 2
      },
      "rate": 1.1,
      "timestamp": "2024-01-01T00:00:00Z"
    }
  ]
}
```
---

## Implementation Guidelines

### Currency Codes
- Use ISO 4217 standard currency codes
- Common codes: EUR, USD, GBP, JPY, CAD, AUD
- Always use uppercase 3-letter codes

### Precision
- Most currencies use 2 decimal places (e.g., 34.95)
- Some currencies use 0 decimal places (e.g., JPY: 1000)
- Some currencies use 3 decimal places (e.g., BHD: 1.234)
- Store amounts as numbers, not strings

### Validation Rules
- `amount` must be a valid number
- `currency` must be a valid ISO 4217 code
- Zero amounts are valid

### Negative Amount Usage
- **Appropriate**: Refunds, credit adjustments, accounting reversals
- **Avoid**: Discounts should typically use separate discount tracking (see [promotion](../promotion/promotion.md) entities) rather than negative money amounts
- **Consider context**: In totals calculations, negative amounts may be appropriate for display purposes

### Best Practices
- Always include both `amount` and `currency` fields
- Use consistent precision for the same currency
- Consider using a decimal library for financial calculations
- Validate currency codes against supported currencies

### Optional Fields Usage
- **`name`** and **`symbol`**: Include when building user interfaces that display currency information
- **`precision`**: Include when the system needs to format amounts for display or when precision differs from currency defaults
- For simple API exchanges between systems, `amount` and `currency` are typically sufficient

## Common Currency Examples

| Code | Name              | Symbol | Precision |
| ---- | ----------------- | ------ | --------- |
| EUR  | Euro              | €      | 2         |
| USD  | US Dollar         | $      | 2         |
| GBP  | British Pound     | £      | 2         |
| JPY  | Japanese Yen      | ¥      | 0         |
| CAD  | Canadian Dollar   | C$     | 2         |
| AUD  | Australian Dollar | A$     | 2         |
| CHF  | Swiss Franc       | CHF    | 2         |
| CNY  | Chinese Yuan      | ¥      | 2         |
| INR  | Indian Rupee      | ₹      | 2         |
| BRL  | Brazilian Real    | R$     | 2         |

---

## Related Utility Objects

- **[address](address.md)**: Location information for billing/shipping
- **[Media](media.md)**: Digital assets for financial documents
- **Carrier**: Shipping information with cost implications

---

> This MACH Alliance Canonical Data Model is intentionally __vendor-neutral__ and serves as a foundation for interoperability across composable architectures. It is __continually evolving__ through community contributions, which are reviewed and approved collaboratively.
>
> All contributions are made under the __Creative Commons Attribution 4.0 International License (CC BY 4.0)__. By submitting a contribution, you agree to license your content under <a href="https://creativecommons.org/licenses/by/4.0/deed.en">CC BY 4.0</a>, allowing others to share and adapt the material with proper attribution.
