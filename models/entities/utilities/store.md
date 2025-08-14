# MACH Alliance • Open Data Model Utility Object: `Store`

## Table of contents

- [Purpose](#purpose)
    - [Key Use Cases](#key-use-cases)
- [Object Schema](#object-schema)
    - [Market Configuration](#market-configuration)
    - [Brand Configuration](#brand-configuration)
    - [Capabilities](#capabilities)
- [Sample Objects](#sample-objects)
    - [Physical Store](#physical-store)
    - [Online Store (Country/Market Site)](#online-store-countrymarket-site)
    - [Pop-up Store](#pop-up-store)
    - [Marketplace Partner Store](#marketplace-partner-store)
- [Core Components & Relationships](#core-components--relationships)
    - [Components](#components)
    - [Typical Relationships](#typical-relationships)
- [Implementation Guidelines](#implementation-guidelines)
    - [Store Types](#store-types)
    - [Market Configuration](#market-configuration-1)
    - [Integration Patterns](#integration-patterns)
- [Typical Pitfalls](#typical-pitfalls)

---

## Purpose
The Store utility object provides a standardized representation for physical stores, online sites, marketplaces, and other commercial locations. It supports multi-channel commerce scenarios including B2B, B2C, and hybrid models across different countries, markets, and brands.

### Key Use Cases
- Physical retail stores and locations
- eCommerce websites and online stores
- Market-specific sites (country/market/brand sites)
- Pop-up stores and temporary locations
- Partner locations and marketplaces
- Multi-brand and multi-market configurations

---

## Object Schema

| Field | Type | Description | Practice |
|-------|------|-------------|----------|
| `id` | string | Unique store identifier | SHOULD |
| `name` | object | Localized store name | SHOULD |
| `type` | string | Store type (`physical`, `online`, `marketplace`, `popup`, `partner`) | SHOULD |
| `status` | string | Operational status (`active`, `inactive`, `temporarily_closed`, `permanently_closed`) | SHOULD |
| `external_references` | object | Cross-system identifiers for integration | SHOULD |
| `address` | object | Physical location using [address](../address.md) utility object | COULD |
| `contact` | object | Contact information using [contact](../contact.md) utility object | COULD |
| `market` | object | Market configuration (country, region, language) | SHOULD |
| `brand` | object | Brand configuration and identity | COULD |
| `capabilities` | array | Available services and features | COULD |
| `operating_hours` | object | Store operating schedule | COULD |
| `extensions` | object | Namespaced extension data | RECOMMENDED |

### Market Configuration

| Field | Type | Description | Practice |
|-------|------|-------------|----------|
| `country` | string | ISO 3166-1 alpha-2 country code | SHOULD |
| `region` | string | State/province/region code | COULD |
| `currency` | string | ISO 4217 currency code | SHOULD |
| `timezone` | string | IANA timezone identifier | SHOULD |
| `language` | array | Supported languages using [language](../language.md) utility objects | SHOULD |
| `defaultLanguage` | string | Primary language code | SHOULD |

### Brand Configuration

| Field | Type | Description | Practice |
|-------|------|-------------|----------|
| `brand_Id` | string | Brand identifier | COULD |
| `brand_name` | string | Brand display name | COULD |
| `brand_slug` | string | URL-friendly brand identifier | COULD |
| `brandLogo` | object | Brand logo using [Media](../media.md) utility object | COULD |

### Capabilities

| Capability | Description | Context |
|------------|-------------|---------|
| `pickup` | Click and collect services | Physical stores |
| `delivery` | Local delivery services | Physical stores |
| `returns` | Return and exchange services | All store types |
| `consultation` | In-person consultation services | Physical stores |
| `events` | Store events and workshops | Physical stores |
| `onlineOrdering` | Online ordering capabilities | All store types |
| `mobileApp` | Mobile app integration | Online stores |
| `loyaltyProgram` | Loyalty program participation | All store types |

---

## Sample Objects

### Physical Store

```jsonc
{
  "id": "store-nyc-001",
  "name": {
    "en": "New York Flagship Store",
    "es": "Tienda Principal de Nueva York"
  },
  "type": "physical",
  "status": "active",
  "external_references": {
    "pos": "POS-NYC-001",
    "inventory": "INV-NYC-001",
    "crm": "STORE-NYC-001"
  },
  "address": {
    "line1": "123 Fifth Avenue",
    "line2": "Suite 100",
    "city": "New York",
    "region": "NY",
    "postal_code": "10003",
    "country": "US"
  },
  "contact": {
    "phone": "+1-212-555-0123",
    "email": "nyc@example.com"
  },
  "market": {
    "country": "US",
    "region": "NY",
    "currency": "USD",
    "timezone": "America/New_York",
    "language": [
      {
        "code": "en",
        "name": "English",
        "locale": "en-US"
      },
      {
        "code": "es",
        "name": "Spanish",
        "locale": "es-US"
      }
    ],
    "defaultLanguage": "en"
  },
  "brand": {
    "brand_id": "brand-premium",
    "brand_name": "Premium Brand",
    "brand_slug": "premium"
  },
  "capabilities": ["pickup", "delivery", "returns", "consultation", "events"],
  "operating_hours": {
    "monday": {"open": "09:00", "close": "21:00"},
    "tuesday": {"open": "09:00", "close": "21:00"},
    "wednesday": {"open": "09:00", "close": "21:00"},
    "thursday": {"open": "09:00", "close": "21:00"},
    "friday": {"open": "09:00", "close": "22:00"},
    "saturday": {"open": "10:00", "close": "22:00"},
    "sunday": {"open": "11:00", "close": "19:00"}
  },
  "extensions": {
    "analytics": {
      "storeCode": "NYC001",
      "region": "Northeast",
      "source": "analytics_platform"
    },
    "inventory": {
      "warehouse_id": "WH-NYC-001",
      "source": "inventory_system"
    }
  }
}
```

### Online Store (Country/Market Site)

```jsonc
{
  "id": "store-us-online",
  "name": {
    "en": "US Online Store",
    "es": "Tienda en Línea EE.UU."
  },
  "type": "online",
  "status": "active",
  "external_references": {
    "commerce": "COMMERCE-US-001",
    "cms": "CMS-US-001",
    "analytics": "ANALYTICS-US-001"
  },
  "market": {
    "country": "US",
    "currency": "USD",
    "timezone": "America/New_York",
    "language": [
      {
        "code": "en",
        "name": "English",
        "locale": "en-US"
      },
      {
        "code": "es",
        "name": "Spanish",
        "locale": "es-US"
      }
    ],
    "defaultLanguage": "en"
  },
  "brand": {
    "brand_id": "brand-global",
    "brand_name": "Global Brand",
    "brand_slug": "global"
  },
  "capabilities": ["onlineOrdering", "mobileApp", "loyaltyProgram"],
  "extensions": {
    "seo": {
      "domain": "us.example.com",
      "primary_language": "en",
      "source": "cms"
    },
    "analytics": {
      "tracking_id": "GA-US-001",
      "region": "North America",
      "source": "analytics_platform"
    }
  }
}
```

### Pop-up Store

```jsonc
{
  "id": "store-popup-holiday-2024",
  "name": {
    "en": "Holiday Pop-up Store",
    "es": "Tienda Temporal de Vacaciones"
  },
  "type": "popup",
  "status": "active",
  "external_references": {
    "pos": "POS-POPUP-001",
    "inventory": "INV-POPUP-001"
  },
  "address": {
    "line1": "456 Shopping Center",
    "city": "Los Angeles",
    "region": "CA",
    "postal_code": "90210",
    "country": "US"
  },
  "market": {
    "country": "US",
    "region": "CA",
    "currency": "USD",
    "timezone": "America/Los_Angeles",
    "language": [
      {
        "code": "en",
        "name": "English",
        "locale": "en-US"
      }
    ],
    "defaultLanguage": "en"
  },
  "capabilities": ["pickup", "returns"],
  "operating_hours": {
    "monday": {"open": "10:00", "close": "20:00"},
    "tuesday": {"open": "10:00", "close": "20:00"},
    "wednesday": {"open": "10:00", "close": "20:00"},
    "thursday": {"open": "10:00", "close": "20:00"},
    "friday": {"open": "10:00", "close": "21:00"},
    "saturday": {"open": "10:00", "close": "21:00"},
    "sunday": {"open": "11:00", "close": "19:00"}
  },
  "extensions": {
    "temporary": {
      "start_date": "2024-11-01T00:00:00Z",
      "end_date": "2024-12-31T23:59:59Z",
      "source": "store_management"
    }
  }
}
```

### Marketplace Partner Store

```jsonc
{
  "id": "store-marketplace-amazon",
  "name": {
    "en": "Amazon Marketplace Store",
    "es": "Tienda de Amazon Marketplace"
  },
  "type": "marketplace",
  "status": "active",
  "external_references": {
    "amazon": "AMZ-SELLER-001",
    "inventory": "INV-AMZ-001"
  },
  "market": {
    "country": "US",
    "currency": "USD",
    "timezone": "America/New_York",
    "language": [
      {
        "code": "en",
        "name": "English",
        "locale": "en-US"
      }
    ],
    "defaultLanguage": "en"
  },
  "brand": {
    "brand_id": "brand-marketplace",
    "brand_name": "Marketplace Brand"
  },
  "capabilities": ["online_ordering", "marketplace_integration"],
  "extensions": {
    "marketplace": {
      "platform": "amazon",
      "seller_id": "A1B2C3D4E5F6G7",
      "source": "marketplace_integration"
    }
  }
}
```

---

## Core Components & Relationships

### Components

| Concept | Description | Typical Source of Truth |
|---------|-------------|-------------------------|
| **Store** | Physical or virtual commercial location | Store Management System |
| **Market** | Geographic and cultural configuration | Localization System |
| **Brand** | Brand identity and configuration | Brand Management System |
| **Capabilities** | Available services and features | Store Management System |


---

## Implementation Guidelines

### Store Types
- **Physical**: Brick-and-mortar locations with addresses
- **Online**: eCommerce websites and digital storefronts
- **Marketplace**: Third-party platform integrations
- **Popup**: Temporary or seasonal locations
- **Partner**: Affiliate or reseller locations

### Market Configuration
- Use ISO standards for country codes (ISO 3166-1 alpha-2)
- Use IANA timezone identifiers for timezone
- Support multiple languages per market
- Define default language for each market

### Integration Patterns
- Use `external_references` to maintain relationships across systems
- Include `source` in extensions for data lineage
- Support both single-brand and multi-brand configurations
- Enable market-specific customization through extensions

---

## Typical Pitfalls

- **Inconsistent market definitions** across systems - Use standardized country and language codes
- **Missing timezone information** - Always include timezone for proper scheduling and localization
- **Inadequate language support** - Support multiple languages per market with proper fallbacks
- **Poor capability management** - Clearly define what services each store type offers
- **Missing operating hours** - Include operating hours for physical stores and customer service
- **Insufficient brand configuration** - Support multi-brand scenarios with proper brand identification

---

> This MACH Alliance Canonical Data Model is intentionally __vendor-neutral__ and serves as a foundation for interoperability across composable architectures. It is __continually evolving__ through community contributions, which are reviewed and approved collaboratively.
>
> All contributions are made under the __Creative Commons Attribution 4.0 International License (CC BY 4.0)__. By submitting a contribution, you agree to license your content under <a href="https://creativecommons.org/licenses/by/4.0/deed.en">CC BY 4.0</a>, allowing others to share and adapt the material with proper attribution. 

