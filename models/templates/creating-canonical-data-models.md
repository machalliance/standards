
# Guide to creating canonical data models

## Purpose

This guide enables teams to define, review, and manage canonical entity models that fit within a MACH-based, composable architecture. The aim is to support semantic clarity and interoperability without over-engineering or bloating models with unnecessary detail.

Models built using this guide should:

- Be easy to review and reason about  
- Capture shared understanding across systems and teams  
- Emphasize reuse via **utility objects**
- Isolate context-specific extensions via **traits**  
- Encourage minimalism: not every use case needs to be modeled into the entity itself  

---
This guide is intended as a living "standard" comprised of best practice recipies. If you are designing a new entity:
- Use this as a baseline
- Contribute improvements via PRs or discussion threads
- Share your examples and patterns

## Quick start:
Each model:
- Promotes semantic clarity and shared understanding
- Avoids unnecessary detail and complexity
- Encourages consistent use of utility objects (e.g. `Address`)
- Uses `traits` for context-specific, namespaced extensions

Use the ./master-entity-template.md as baseline


## Design Principles

- Less is more: Avoid modeling everything—focus on what is shared
- Composable by design: Prefer small, stable objects over large, rigid schemas
- Versionable and explainable: Make the model clear to non-engineers
- Traits over meta: Use structured traits, not catch-all `meta` blobs

### 2. Use Utility Objects

Reference shared objects like `Address`, `Money`, `PhoneNumber`.  
Do not redefine their structure inside the model.

---

### 3. Structure approach: Traits by Concern or schema first

Use traits to group optional data under namespaces like:
- `marketing`
- `loyalty`
- `service`
... and provide json examples of `trait.service`.

Each trait should:
- Have a clear domain responsibility
- Include a `source` key
- Be optional and additive

Trait schema validation, where needed:
- Alternatively all traits could be entensible objects. This can aid implementatoin and schema validation.



---

#### Canonical Schema: Traits - the key interoperable ingredient

Use `traits` to support semantic grouping of optional fields in a structured and extensible way.

> `traits` is a dictionary of namespaced objects that allows each domain (e.g., marketing, loyalty, service) to manage its own data cleanly—without polluting the core schema.

#### Declaring Source Systems
When using `traits` to extend a canonical entity model, we recommended including the **source system**—the system of authority where the data is stored or managed.
Declaring `source` inside each trait aims to ensure your MACH architecture remains reliable, composable, and conflict-free. Standardize it across your model for future-proof interoperability.

This improves:
- **Traceability** – Understand where a value comes from
- **Auditability** – Know which system is responsible
- **Interoperability** – Enable safe round-tripping across MACH services, systems and interfaces
- **Conflict resolution** – Avoid overwrites from the wrong system - or at least dettect them.

#### Traits Structure

Include a `source` field at the trait or sub-trait level:

```json
"traits": {
  "namespace": {
    "field": "value",
    "source": "system-name"
  }
}
```
#### Traits Examples

##### Availability (channel, geography)

```json
"traits": {
  "availability": {
    "channelAvailability": ["web","store"],
    "regionAvailability": ["EU"]
  }
}
```

##### Marketing Consent

```json
"traits": {
  "marketing": {
    "consentStatus": "optedIn",
    "consentGivenAt": "2025-01-12T09:34:00Z",
    "consentText": "I accept great news weekly...",
    "source": "voyado"
  }
}
```

##### Order Status

```json
"traits": {
  "order": {
    "pendingStatus": "awaitingFulfillment",
    "lastSynced": "2025-06-01T10:22:00Z",
    "source": "pipe17"
  }
}
```

##### Loyalty

```json
"traits": {
  "loyalty": {
    "tier": "gold",
    "points": 3500,
    "nextRewardAt": 5000,
    "source": "talonone",
    "channels": "retail"
  }
}
```


## Review Checklist

| Question | ✓ |
|----------|---|
| Are utility objects reused? | ? |
| Is the model lean and readable? | ? |
| Are traits used for non-core fields? | ? |
| Does each trait declare its source system? | ? |
| Will it work across 80% of known use cases? | ? |
| Are edge cases handled in examples, not schema? | ? |


## canonical entity example: customer

### entity schema

| Field         | Description | Practice    |
|---------------|-------------|-------------|
| `id`          | Unique identifier (e.g. UUID or slug). | SHOULD |
| `type`        | `person` or `company`. | SHOULD |
| `status`      | `active`, `inactive`, `archived`. | SHOULD |
| `referenceIds`| Map of external system IDs to ease orchestration logic | SHOULD |
| `createdAt`   | ISO 8601 creation timestamp. | SHOULD |
| `updatedAt`   | ISO 8601 update timestamp. | SHOULD |
| `traits`      | Namespaced dictionary grouped by domain concern. | RECOMMENDED |
| `person`      | Object if `type = person`. | COULD |
| `company`     | Object if `type = company`. | COULD |
| `addresses`   | List of typed addresses (via utility object). | RECOMMENDED |

---

### sample JSON

```json
{
  "id": "cus_001",
  "type": "person",
  "status": "active",
  "referenceIds": {
    "crmContactId": "123456",
    "commercetools": "customer-98765"
  },
  "createdAt": "2025-06-01T12:00:00Z",
  "updatedAt": "2025-06-10T12:30:00Z",
  "traits": {
    "marketing": {
      "consent": "optedIn",
      "source": "voyado"
    },
    "loyalty": {
      "points": 200,
      "tier": "silver",
      "source": "talonone"
    }
  },
  "person": {
    "firstName": "Emma",
    "lastName": "Larsen",
    "email": "emma@example.com",
    "phone": "+45 12345678"
  },
  "addresses": [
    {
      "type": "shipping",
      "address": {
        "line1": "Strandvejen 100",
        "city": "Aarhus",
        "region": "Midtjylland",
        "postalCode": "8000",
        "country": "DK"
      }
    }
  ]
}
```

### sample JSON of alternative structure 
This approach can easily be validated by a schema.
>References are always of an object that must have type and id and `traits` are in this sample an object with type and values.

```json
{
    "id": "cus_001",
    "type": "person",
    "status": "active",
    "references": [ // References are always of an object that must have type and id
        {
            "type": "commercetools",
            "id": "12345"
        },
        {
            "type": "hubspot",
            "id": "abc12345"
        }
    ],
    "createdAt": "2025-06-01T12:00:00Z",
    "updatedAt": "2025-06-10T12:30:00Z",
    "traits": [  // Traits are always of an object that must have type and values
        {
            "type": "marketing",
            "values": [ // Values are always an object that must have name and value
                {
                    "name": "consent",
                    "value": "opedIn"
                },
                {
                    "name": "source",
                    "value": "voyado"
                }
            ]
        },
        {
            "type": "loyalty",
            "values": [
                {
                    "name": "points",
                    "value": "200"
                },
                {
                    "name": "tier",
                    "value": "silver"
                },
                {
                    "name": "source",
                    "value": "talonone"
                }
            ]
        }
    ],
    "person": {
        "firstName": "Emma",
        "lastName": "Larsen",
        "email": "emma@example.com",
        "phone": "+45 12345678"
    },
    "addresses": [
        {
            "type": "shipping",
            "address": {
                "line1": "Strandvejen 100",
                "city": "Aarhus",
                "region": "Midtjylland",
                "postalCode": "8000",
                "country": "DK"
            }
        }
    ]
}
