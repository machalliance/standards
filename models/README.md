# MACH Open Data Model initiative

[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](./CHANGELOG.md)
[![Last Updated](https://img.shields.io/badge/last%20updated-August%202025-green.svg)](.)
[![Entities](https://img.shields.io/badge/entities-11-orange.svg)](./entities)
[![Recipes](https://img.shields.io/badge/recipes-2-purple.svg)](./recipes)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

> **Last Updated:** August 2025 | **Version:** 1.0.0 | **Status:** Initial Release

## Table of Contents
- [MACH Open Data Model initiative](#mach-open-data-model-initiative)
  - [Table of Contents](#table-of-contents)
  - [What it is](#what-it-is)
    - [Example: Customer Entity](#example-customer-entity)
  - [Current status](#current-status)
  - [Who it's for](#who-its-for)
  - [Why we are doing this](#why-we-are-doing-this)
  - [Getting Started](#getting-started)
    - [Quick Start Guide](#quick-start-guide)
    - [Understanding the Model Structure](#understanding-the-model-structure)
    - [Entity Coverage Matrix](#entity-coverage-matrix)
    - [Core Entities Available](#core-entities-available)
      - [Identity \& Customer Data](#identity-customer-data)
      - [Product Information](#product-information)
      - [Commerce Operations](#commerce-operations)
      - [Utility Objects](#utility-objects)
    - [Popular Recipes](#popular-recipes)
  - [Contributing](#contributing)
  - [Format and Philosophy](#format-and-philosophy)
  - [From Recipes to Real-World Integration](#from-recipes-to-real-world-integration)
  - [Use these recipes to:](#use-these-recipes-to)
  - [Implementation Notes](#implementation-notes)
    - [Attribute Schema Design](#attribute-schema-design)
  - [Contributors \& Stewardship](#contributors-stewardship)

## What it is

The MACH Alliance Open Data Model (ODM) initiative is the natural next step in enabling interoperability across composable ecosystems. It serves as a semantic interoperability layer: a "Rosetta Stone" for understanding how to translate data between systems in hybrid commerce architectures. It provides canonical reference models and implementation guidance that enable architects to design effective data integration across commerce platforms while preparing organizations for AI-powered ecosystems.

After defining the MACH reference architecture and principles of composability, the next logical foundation is a shared, human-readable data models and recipes that vendors, platforms, and integrators can align around—without requiring tight coupling to any specific technology.

### Example: Customer Entity
Here's a simple example of what an ODM entity looks like:

```json
{
  "id": "cust_123456",
  "email": "john.doe@example.com",
  "profile": {
    "firstName": "John",
    "lastName": "Doe",
    "dateOfBirth": "1990-01-15"
  },
  "extensions": {
    "loyalty": {
      "tier": "gold",
      "points": 15000
    }
  }
}
```

This standardized structure works across any CRM, CDP, or commerce platform, eliminating custom mappings for every integration.

## Current status

- **Initial release (August 2025)** - Core project structure with 11 entities across identity, product catalog, commerce operations, and utilities, plus 2 PDP orchestration recipes
- **Next planned release (Q4 2025)** - Order management entities (Order, Cart, Fulfillment) and checkout orchestration recipes
- **2026 Roadmap** - AI/Agent communication standards, advanced orchestration patterns, and marketplace entities

For more information, visit the [current open issues](https://github.com/machalliance/standards/issues) and [Changelog](./CHANGELOG.md).

## Who it's for

The entities and recipes are designed to be understood by architects and decision-makers as they are building differentiated implementations. By being vendor-neutral and approach agnostic, these recipes allow stakeholders to understand and contribute to model design **before** implementation by providing real-world knowledge to assist in answering the question:
> "What are you trying to achieve with your integration?"

## Why we are doing this

By documenting how entities such as Customer, Order, Product (and more) interact and best practices for common tasks across vendors (recipes) the MACH Alliance is demystifying how processes and data move between composable applications such as CMS, PIM, CRM, loyalty, and commerce platforms.

The intent is that these models can be used by architects (either directly, or via LLM tools) to _rapidly_ build composable solutions by having a set of patterns and practices that are known to work for specific scenarios.

## Getting Started

### Quick Start Guide
1. **New to ODM?** Start with the [Customer entity](entities/identity/customer.md) to understand the structure
2. **Ready to integrate?** Try the [PDP Orchestration recipe](recipes/PDP-orchestration-on-the-fly.md) for a complete integration example
3. **Building your model?** Use the [entity template](templates/master-entity-template.md) as your starting point

### Understanding the Model Structure
- **Entities** - Core business objects (Customer, Product, Order) with standardized fields
- **Utility Objects** - Reusable components (Address, Media) shared across entities
- **Recipes** - Real-world integration patterns showing how entities work together
- **Extensions** - Namespaced fields for vendor-specific or custom data

### Entity Coverage Matrix
| Domain               | Entities                                       | Status           |
| -------------------- | ---------------------------------------------- | ---------------- |
| Identity & Customer  | Customer                                       | ✅ Complete       |
| Product Catalog      | Product, Category, Product Type                | ✅ Complete       |
| Commerce Operations  | Inventory, Pricing, Promotion, Coupon Instance | ✅ Complete       |
| Order Management     | Order, Cart, Fulfillment                       | 🚧 Coming Q4 2025 |
| Content & Media      | Media (utility)                                | ✅ Complete       |
| Location & Geography | Address (utility), Store Location              | ✅ Address done   |
| Internationalization | Language (utility)                             | ✅ Complete       |

### Core Entities Available

#### Identity & Customer Data
- **[Customer](entities/identity/customer.md)** - Unified customer profile supporting B2B/B2C scenarios

#### Product Information
- **[Product](entities/product/product.md)** - Product catalog with variants and digital products
- **[Category](entities/product/category.md)** - Hierarchical product categorization
- **[Product Type](entities/product/product-type.md)** - Attribute definitions and product classification

#### Commerce Operations
- **[Inventory](entities/inventory/inventory.md)** - Multi-location stock and availability
- **[Pricing](entities/pricing/pricing.md)** - Tiered, bulk, and multi-currency pricing
- **[Promotion](entities/promotion/promotion.md)** - Discount rules and campaign management
- **[Coupon Instance](entities/promotion/coupon-instance.md)** - Individual coupon tracking and redemption

#### Utility Objects
- **[Address](entities/utilities/address.md)** - International address formats with validation
- **[Media](entities/utilities/media.md)** - Images, videos, and digital assets
- **[Language](entities/utilities/language.md)** - Locale and internationalization support

### Popular Recipes
- **[PDP Orchestration (on the fly)](recipes/PDP-orchestration-on-the-fly.md)** - Real-time product detail page composition
- **[PDP Orchestration (optimized access)](recipes/PDP-orchestration-optimized-access.md)** - Pre-optimized product data access layer

## Contributing

While the MACH Alliance and members have contributed to the initial effort, this project is also a call-to-action for others to help contribute their knowledge. For more information, visit [How to contribute](./CONTRIBUTING.md).

---

## Format and Philosophy

Each [Entity](entities) and [Recipe](recipes) includes:
- **Markdown formatted documentation (`.md`)** for human or machine-readable documentation, narrative context, and sample use case recipes.
- **Object definitions, JSON and YAML samples** for clear, structured example representation of entities and extensions.
- **Extensions** to support modularity, reuse, and domain-specific concerns for clearer contextual interoperability.

We chose Markdown and JSON for their balance of **accessibility and precision**:
- **Markdown** enables understanding without context—useful in early alignment or design stages, especially across teams unfamiliar with a given stack or vendor.
- **JSON** provides copy-pasteable clarity for developers, and a foundation for code generation or LLM-based tooling.

> [!TIP]
> The [entity template](templates/master-entity-template.md) contains more details of the format with examples

Recipes include greater detail for meeting specific use cases, including:

- Business objective
- Typical pitfalls
- Data flows
  - Actors / Stakeholders
  - Trigger Points / Events
  - Diagrams
- Systems Involved
- Data Requirements
- Success Metrics / KPIs
- Security & Compliance Notes

> [!TIP]
> The [recipe template](templates/master-recipe-template.md) contains more details of the format with examples

---

## From Recipes to Real-World Integration
| Stage                               | Format/Tool                 | Best When...                                                                                                         |
| ----------------------------------- | --------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| **Design & Understanding**          | Markdown + JSON             | You’re defining the model collaboratively and don’t know the integration goal yet                                    |
| **Standard Messaging**              | AsyncAPI                    | You want ecosystem-wide publish/subscribe contracts (MQTT, Kafka, AMQP)                                              |
| **API Contracts**                   | OpenAPI (YAML)              | You are defining synchronous HTTP-based services with stable interfaces                                              |
| **Data Validation / Code Gen**      | JSON Schema / TS            | You’re ready for strict validation or scaffolding code                                                               |
| **Platform-Specific Automation**    | YAML (e.g. Cloud providers) | You’re working within a known platform's infrastructure                                                              |
| **Orchestration / LLM Integration** | LLM + MCP/A2A               | You have context and goals defined and want to auto-generate runtime logic or agent-to-agent information interchange |

---

## Use these recipes to:

- Align vendors on what "interoperability-ready" actually means
- Prototype integrations without premature coupling
- Create compatibility layers across hybrid or legacy systems
- Seed future enhancements like OpenAPI specs, orchestration layer logic, or LLM integrations

> [!TIP]
> These models and recipes are a starting point to provide a framework for others to contribute entities and recipes in additional domains

---

## Implementation Notes

### Attribute Schema Design
- Design flexible attribute systems that support multiple data types and validation rules
- Implement conditional attributes based on other attribute values
- Support localization of attribute labels and validation messages

## Contributors & Stewardship

These recipes were developed under the guidance of the **MACH Alliance Interoperability Task Force**, an open working group of technical leaders from across the MACH ecosystem.

**Contributors include**:
- Adam Peter Nielsen, Novicell
- Mark Demeny, MACH Alliance (mark.demeny@machalliance.org)
- Dom Selvon, MACH Alliance
- Filip Rakowski, Alokai
- Daniele Stroppa, AWS
- Subhasri Vadyar, Valtech
- Sana Remekie, Conscia
- Melanie Jensen, Apply Digital
- ...and many others contributing through real-world use cases, architecture demos, and platform research.

> [!IMPORTANT]
> Want to [contribute](CONTRIBUTING.md)? Join the task force or open a pull request with your model insights.

---
