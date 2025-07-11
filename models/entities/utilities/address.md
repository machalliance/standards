# MACH Alliance, Open Data Model Utility Object: `Address`

## Table of contents

- [Purpose](#purpose)
- [Object: Address](#object-address)
- [Sample Objects](#sample-objects)
  - [US Address](#us-address)
  - [European Address](#european-address)
  - [International Address](#international-address)
  - [Minimal Address](#minimal-address)
- [Usage Examples](#usage-examples)
  - [In Customer Profile](#in-customer-profile)
  - [In Order Entity](#in-order-entity)
  - [In Cart with Address Selection](#in-cart-with-address-selection)
- [Implementation Guidelines](#implementation-guidelines)
  - [Country Codes](#country-codes)
  - [Address Formatting](#address-formatting)
  - [Validation Rules](#validation-rules)
  - [Best Practices](#best-practices)
  - [Regional Considerations](#regional-considerations)
- [Common Country Codes](#common-country-codes)
- [Related Utility Objects](#related-utility-objects)


### Purpose

A standardized utility object for representing physical addresses across all entities in the MACH Alliance Common Data Model. This ensures consistent handling of location information for shipping, billing, customer profiles, and business addresses across commerce platforms, order management systems, and customer relationship management.

The Address utility object provides:
- Standardized address structure
- International address support
- Consistent formatting across systems
- Support for different address types
- Validation and normalization capabilities

---

## Object: Address

| Field         | Description                                    | Practice     |
|---------------|------------------------------------------------|--------------|
| `line1`       | Primary address line (street number and name)  | SHOULD   |
| `line2`       | Secondary address line (apartment, suite, etc.)| COULD    |
| `city`        | City or locality name                          | SHOULD   |
| `region`      | State, province, or region                     | SHOULD   |
| `postalCode`  | Postal or ZIP code                             | SHOULD   |
| `country`     | ISO 3166-1 alpha-2 country code                | SHOULD   |

---

## Sample Objects

### US Address

```jsonc
{
  "line1": "123 Main Street",
  "line2": "Suite 100",
  "city": "New York",
  "region": "NY",
  "postalCode": "10001",
  "country": "US"
}
```

### European Address

```jsonc
{
  "line1": "456 High Street",
  "line2": "Apartment 5B",
  "city": "London",
  "region": "Greater London",
  "postalCode": "SW1A 1AA",
  "country": "GB"
}
```

### International Address

```jsonc
{
  "line1": "789 Rue de la Paix",
  "line2": "Étage 3",
  "city": "Paris",
  "region": "Île-de-France",
  "postalCode": "75001",
  "country": "FR"
}
```

### Minimal Address

```jsonc
{
  "line1": "123 Business Blvd",
  "city": "Business City",
  "region": "BusinessState",
  "postalCode": "54321",
  "country": "US"
}
```

---

## Usage Examples

### In Customer Profile

```jsonc
{
  "id": "CUST-001",
  "name": "John Doe",
  "addresses": [
    {
      "type": "billing",
      "address": {
        "line1": "123 Main Street",
        "line2": "Suite 100",
        "city": "New York",
        "region": "NY",
        "postalCode": "10001",
        "country": "US"
      }
    },
    {
      "type": "shipping",
      "address": {
        "line1": "456 Oak Avenue",
        "city": "Los Angeles",
        "region": "CA",
        "postalCode": "90210",
        "country": "US"
      }
    }
  ]
}
```

### In Order Entity

```jsonc
{
  "id": "ORDER-001",
  "customerId": "CUST-001",
  "billingAddress": {
    "line1": "123 Main Street",
    "line2": "Suite 100",
    "city": "New York",
    "region": "NY",
    "postalCode": "10001",
    "country": "US"
  },
  "shippingAddress": {
    "line1": "456 Oak Avenue",
    "city": "Los Angeles",
    "region": "CA",
    "postalCode": "90210",
    "country": "US"
  }
}
```

### In Cart with Address Selection

```jsonc
{
  "id": "CART-001",
  "customerId": "CUST-001",
  "addresses": [
    {
      "type": "shipping",
      "address": {
        "line1": "456 Oak Avenue",
        "city": "Los Angeles",
        "region": "CA",
        "postalCode": "90210",
        "country": "US"
      },
      "contact": {
        "name": "John Doe",
        "phone": "+1234567890"
      }
    }
  ]
}
```

---

## Implementation Guidelines

### Country Codes
- Use ISO 3166-1 alpha-2 country codes
- Common codes: US, GB, FR, DE, CA, AU, JP, CN
- Always use uppercase 2-letter codes

### Address Formatting
- `line1`: Street number and name
- `line2`: Optional secondary information (apartment, suite, etc.)
- `city`: Full city name
- `region`: State, province, or region name or code
- `postalCode`: Postal code in local format
- `country`: ISO country code

### Validation Rules
- `line1` is required and should not be empty
- `city` is required and should not be empty
- `country` is required and must be a valid ISO 3166-1 alpha-2 code
- `postalCode` format should match the country's standard
- `region` should be appropriate for the specified country

### Best Practices
- Always include `country` for international compatibility
- Use consistent formatting for the same address across systems
- Consider address validation services for accuracy
- Support international address formats
- Normalize addresses for consistent storage and comparison

### Regional Considerations
- **US**: Use 2-letter state codes (NY, CA, TX)
- **Canada**: Use 2-letter province codes (ON, BC, QC)
- **UK**: Use full region names or postal codes
- **International**: Use appropriate regional identifiers

---

## Common Country Codes

| Code | Country | Example Region Format |
|------|---------|----------------------|
| US | United States | NY, CA, TX (2-letter state codes) |
| GB | United Kingdom | Greater London, Scotland |
| FR | France | Île-de-France, Provence |
| DE | Germany | Bayern, Nordrhein-Westfalen |
| CA | Canada | ON, BC, QC (2-letter province codes) |
| AU | Australia | NSW, VIC, QLD (2-letter state codes) |
| JP | Japan | Tokyo, Osaka |
| CN | China | Beijing, Shanghai |

---

## Related Utility Objects

- **Contact**: Contact information associated with addresses
- **Money**: Monetary values for shipping costs
- **ShippingMethod**: Shipping options and rates

---

> This MACH Alliance Canonical Data Model is intentionally __vendor-neutral__ and serves as a foundation for interoperability across composable architectures. It is __continually evolving__ through community contributions, which are reviewed and approved collaboratively.
>
> All contributions are made under the __Creative Commons Attribution 4.0 International License (CC BY 4.0)__. By submitting a contribution, you agree to license your content under <a href="https://creativecommons.org/licenses/by/4.0/deed.en">CC BY 4.0</a>, allowing others to share and adapt the material with proper attribution. 
