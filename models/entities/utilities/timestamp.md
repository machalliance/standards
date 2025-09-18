# MACH Alliance • Open Data Model Utility Object: `Timestamp`

## Table of contents

- [Purpose](#purpose)
- [Object: Timestamp](#object-timestamp)
- [Sample Objects](#sample-objects)
- [Usage Examples](#usage-examples)
- [Implementation Guidelines](#implementation-guidelines)
- [Related Utility Objects](#related-utility-objects)

---

## Purpose

A standardized utility object for representing time-related information across all entities in the MACH Alliance Common Data Model. This ensures consistent handling of dates, times, timezones, and duration across commerce engines, order management systems, scheduling systems, and analytics platforms.

The Timestamp utility object provides:
- Standardized time representation
- Consistent timezone handling
- Duration calculations
- Time range support
- Audit trail capabilities

---

## Object: Timestamp

| Field         | Description                                    | Practice     |
|---------------|------------------------------------------------|--------------|
| `value`       | ISO 8601 timestamp (e.g., "2024-01-15T10:30:00Z") | SHOULD   |
| `timezone`    | IANA timezone identifier (e.g., "America/New_York") | COULD    |
| `format`      | Display format hint (e.g., "date", "datetime", "time") | COULD    |

---

## Sample Objects

### Sample Object: Basic Timestamp

```jsonc
{
  "value": "2024-01-15T10:30:00Z"
}
```

### Sample Object: Timestamp with Timezone

```jsonc
{
  "value": "2024-01-15T10:30:00Z",
  "timezone": "America/New_York",
  "format": "datetime"
}
```

### Sample Object: Date Only

```jsonc
{
  "value": "2024-01-15T00:00:00Z",
  "format": "date"
}
```

### Sample Object: Time Only

```jsonc
{
  "value": "2024-01-01T14:30:00Z",
  "timezone": "Europe/London",
  "format": "time"
}
```

---

## Usage Examples

### In Order Entity

```jsonc
{
  "id": "ORDER-001",
  "created_at": {
    "value": "2024-01-15T10:30:00Z",
    "timezone": "America/New_York"
  },
  "updated_at": {
    "value": "2024-01-15T14:45:00Z",
    "timezone": "America/New_York"
  },
  "estimated_delivery": {
    "value": "2024-01-20T17:00:00Z",
    "timezone": "America/New_York",
    "format": "datetime"
  }
}
```

### In Campaign Entity

```jsonc
{
  "id": "CAMPAIGN-001",
  "name": "Summer Sale 2024",
  "start_date": {
    "value": "2024-06-01T00:00:00Z",
    "format": "date"
  },
  "end_date": {
    "value": "2024-08-31T23:59:59Z",
    "format": "date"
  },
  "created_at": {
    "value": "2024-01-15T09:00:00Z"
  }
}
```

### In Product Entity

```jsonc
{
  "id": "PROD-001",
  "name": "Organic Cotton T-Shirt",
  "created_at": {
    "value": "2024-01-01T00:00:00Z"
  },
  "updated_at": {
    "value": "2024-01-15T16:30:00Z"
  },
  "available_from": {
    "value": "2024-02-01T00:00:00Z",
    "format": "date"
  }
}
```

### In Customer Entity

```jsonc
{
  "id": "CUST-001",
  "name": "John Doe",
  "registered_at": {
    "value": "2023-12-01T14:30:00Z",
    "timezone": "America/New_York"
  },
  "last_login_at": {
    "value": "2024-01-15T10:15:00Z",
    "timezone": "America/New_York"
  },
  "birth_date": {
    "value": "1990-05-15T00:00:00Z",
    "format": "date"
  }
}
```

---

## Implementation Guidelines

### ISO 8601 Format
- Use ISO 8601 standard for all timestamps
- Include timezone information when relevant
- Use 'Z' suffix for UTC timestamps
- Support fractional seconds when needed

### Timezone Handling
- Use IANA timezone identifiers
- Common timezones: UTC, America/New_York, Europe/London, Asia/Tokyo
- Consider daylight saving time transitions
- Handle timezone conversions appropriately

### Format Types
- **date**: Date only (YYYY-MM-DD)
- **time**: Time only (HH:MM:SS)
- **datetime**: Full date and time
- **duration**: Time duration (P1D, PT2H30M)

### Best Practices
- Always use ISO 8601 format for `value` field
- Include timezone for user-facing timestamps
- Use consistent timezone across related timestamps
- Consider timezone for business logic
- Handle timezone conversions in display layer

### Common Use Cases
- **Creation/Update Times**: Audit trail timestamps
- **Scheduled Events**: Campaign start/end dates
- **Availability Windows**: Product availability periods
- **User Activity**: Login times, session tracking
- **Business Hours**: Operating hours and time ranges

---

## Related Utility Objects

- **[money](money.md)**: Financial transactions with timestamps
- **[address](address.md)**: Location-based timezone considerations
- **[contact](contact.md)**: Contact information with time-based preferences

---

> This MACH Alliance Canonical Data Model is intentionally __vendor-neutral__ and serves as a foundation for interoperability across composable architectures. It is __continually evolving__ through community contributions, which are reviewed and approved collaboratively.
>
> All contributions are made under the __Creative Commons Attribution 4.0 International License (CC BY 4.0)__. By submitting a contribution, you agree to license your content under <a href="https://creativecommons.org/licenses/by/4.0/deed.en">CC BY 4.0</a>, allowing others to share and adapt the material with proper attribution. 
