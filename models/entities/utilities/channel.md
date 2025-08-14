# MACH Alliance • Open Data Model Utility Object: `Channel`

## Table of Contents

- [Purpose](#purpose)
  - [Key Use Cases](#key-use-cases)
- [Channel Types](#channel-types)
  - [Sales Channels](#sales-channels)
  - [Marketing Channels](#marketing-channels)
  - [Service Channels](#service-channels)
  - [Fulfillment Channels](#fulfillment-channels)
- [Usage Guidelines](#usage-guidelines)
  - [Channel Selection](#channel-selection)
  - [Channel Combinations](#channel-combinations)
  - [Channel Validation](#channel-validation)
- [Sample Usage](#sample-usage)
  - [Product Availability](#product-availability)
  - [Campaign Targeting](#campaign-targeting)
  - [Catalog Assignment](#catalog-assignment)
- [Migration Guide](#migration-guide)
  - [From Legacy Channel Names](#from-legacy-channel-names)
  - [Implementation Steps](#implementation-steps)

---

### Purpose
The Channel utility object provides standardized channel definitions for consistent usage across all MACH Alliance entities. It defines the different types of channels where commerce activities occur, enabling consistent channel targeting and availability management.

### Key Use Cases
- Product availability across sales channels
- Campaign targeting across marketing channels
- Discount application across commerce channels
- Catalog assignment across retail channels
- Order fulfillment across service channels

---

## Channel Types

### Sales Channels
Channels where products are sold and transactions occur.

| Channel | Description | Context |
|---------|-------------|---------|
| `web` | eCommerce website and online storefront | Primary digital sales channel |
| `mobile` | Mobile applications and mobile-optimized web | Mobile commerce |
| `store` | Physical retail locations and in-store sales | Brick-and-mortar retail |
| `api` | Programmatic access for B2B and integrations | B2B commerce, marketplace integrations |
| `marketplace` | Third-party marketplace platforms | Amazon, eBay, etc. |
| `social` | Social commerce platforms | Instagram Shop, Facebook Marketplace |
| `voice` | Voice commerce and smart speakers | Amazon Alexa, Google Assistant |

### Marketing Channels
Channels used for marketing communications and campaigns.

| Channel | Description | Context |
|---------|-------------|---------|
| `email` | Email marketing campaigns | Newsletter, promotional emails |
| `sms` | Text message marketing | SMS campaigns, notifications |
| `push` | Push notifications | Mobile app notifications |
| `socialMedia` | Social media advertising | Facebook, Instagram, Twitter ads |
| `display` | Display advertising | Banner ads, retargeting |
| `search` | Search engine marketing | Google Ads, Bing Ads |
| `affiliate` | Affiliate marketing | Partner promotions |

### Service Channels
Channels for customer service and support.

| Channel | Description | Context |
|---------|-------------|---------|
| `chat` | Live chat and messaging | Customer support |
| `phone` | Phone support | Call centers |
| `video` | Video consultations | Virtual appointments |
| `inPerson` | In-person consultations | Store appointments |

### Fulfillment Channels
Channels for order fulfillment and delivery.

| Channel | Description | Context |
|---------|-------------|---------|
| `pickup` | Click and collect, store pickup | BOPIS (Buy Online, Pickup In Store) |
| `delivery` | Home delivery services | Standard shipping |
| `sameDay` | Sameday delivery | Express delivery services |
| `curbside` | Curbside pickup | Contactless pickup |

---

## Usage Guidelines

### Channel Selection
- Use **Sales Channels** for product availability, pricing, and catalog assignments
- Use **Marketing Channels** for campaign targeting and promotional activities
- Use **Service Channels** for customer support and consultation services
- Use **Fulfillment Channels** for order fulfillment and delivery options

### Channel Combinations
```json
// Sales channel example
"channels": ["web", "mobile", "store"]

// Marketing channel example  
"channels": ["email", "socialMedia", "push"]

// Mixed channels (avoid when possible)
"channels": ["web", "email", "pickup"]
```

### Channel Validation
- Validate that channel combinations make sense for the entity type
- Ensure channel availability aligns with store capabilities
- Consider channel-specific business rules and limitations

---

## Sample Usage

### Product Availability
```json
{
  "channels": ["web", "mobile", "store"],
  "channelSpecificPricing": {
    "web": { "amount": 29.99, "currency": "USD" },
    "mobile": { "amount": 27.99, "currency": "USD" },
    "store": { "amount": 29.99, "currency": "USD" }
  }
}
```

### Campaign Targeting
```json
{
  "channels": ["email", "socialMedia", "push"],
  "channelSpecificContent": {
    "email": { "subject": "Special Offer Inside" },
    "socialMedia": { "hashtags": ["#sale", "#limitedtime"] },
    "push": { "title": "Flash Sale Alert!" }
  }
}
```

### Catalog Assignment
```json
{
  "channels": ["web", "mobile"],
  "channelSpecificFeatures": {
    "web": { "featured": true, "sort_order": 1 },
    "mobile": { "featured": false, "sort_order": 3 }
  }
}
```

---

## Migration Guide

### From Legacy Channel Names
| Legacy Name | Standard Name | Notes |
|-------------|---------------|-------|
| `storefront` | `web` | E-commerce website |
| `in-store` | `store` | Physical retail |
| `mobileApp` | `mobile` | Mobile applications |
| `marketplace` | `marketplace` | No change needed |
| `social` | `socialMedia` | Marketing context |
| `social` | `social` | Sales context (social commerce) |

### Implementation Steps
1. **Audit existing channel usage** across all entities
2. **Map legacy names** to standard channel names
3. **Update entity schemas** to use standard channels
4. **Validate channel combinations** for business logic
5. **Update documentation** and examples

---

> This MACH Alliance Canonical Data Model is intentionally __vendor-neutral__ and serves as a foundation for interoperability across composable architectures. It is __continually evolving__ through community contributions, which are reviewed and approved collaboratively.
>
> All contributions are made under the __Creative Commons Attribution 4.0 International License (CC BY 4.0)__. By submitting a contribution, you agree to license your content under <a href="https://creativecommons.org/licenses/by/4.0/deed.en">CC BY 4.0</a>, allowing others to share and adapt the material with proper attribution. 
