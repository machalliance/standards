# MACH Open Data Model initiative

## Why we are doing this

The MACH Open Data Model initiative is the natural next step in enabling interoperability across composable ecosystems. After defining the MACH reference architecture and principles of composability, the next logical foundation is a shared, human-readable data models and recipes that vendors, platforms, and integrators can align around—without requiring tight coupling to any specific technology.

These models act as **pivot formats**—neutral reference points that allow MACH-aligned systems to speak the same conceptual language. They enable a consistent understanding of core entities like Customer, Order, Product, Consent, and more across CMS, PIM, CRM, loyalty, and commerce platforms.

Rather than prematurely optimizing for implementation or tooling, these recipes allow stakeholders to understand and contribute to model design **before** answering the question:  
> “What are you trying to achieve with your integration?”

---

## Format and Philosophy

Each [entity](entities) and [recipe](recipes) includes:
- **Markdown formatted documentation (`.md`)** for human or machine-readable documentation, narrative context, and sample use case recipes.
- **Object definitions and JSON samples** for clear, structured example representation of entities and traits.
- **Trait-based extensions** to support modularity, reuse, and domain-specific concerns for clearer contextual interoperability.

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
Data Requirements
Success Metrics / KPIs
Security & Compliance Notes

> [!TIP]
> The [recipe template](templates/master-recipe-template.md) contains more details of the format with examples

---

## From Recipes to Real-World Integration
| Stage | Format/Tool | Best When...|
|-|-|-|
| **Design & Understanding**        | Markdown + JSON    | You’re defining the model collaboratively and don’t know the integration goal yet |
| **Standard Messaging**            | AsyncAPI           | You want ecosystem-wide publish/subscribe contracts (MQTT, Kafka, AMQP)     |
| **API Contracts**                 | OpenAPI (YAML)     | You are defining synchronous HTTP-based services with stable interfaces      |
| **Data Validation / Code Gen**    | JSON Schema / TS   | You’re ready for strict validation or scaffolding code                      |
| **Platform-Specific Automation**  | YAML (e.g. Cloud providers)    | You’re working within a known platform's infrastructure                     |
| **Orchestration / LLM Integration** | LLM + MCP/A2A    | You have context and goals defined and want to auto-generate runtime logic og agent-toagent information interchange |

---

## Use these recipes to:

- Align vendors on what "interoperability-ready" actually means
- Prototype integrations without premature coupling
- Create compatibility layers across hybrid or legacy systems
- Seed future YAML schemas, OpenAPI specs, Orchestration layer logic or LLMs

> [!TIP]
> These models and recipes are not the end—they’re the beginning of better interoperability.

---

## Implementation Notes:

  **Attribute Schema Design**
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
