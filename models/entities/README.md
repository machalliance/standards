# MACH Alliance, Open Data Model Entity list
```mermaid
erDiagram
    %% Core Product relationships
    Product:::entity 1 to 1 "Product Type":::entity : "defined by"
    Product 1 to 1 Category:::entity : "classified by"
    Product 1 to 1 "Catalog (coming soon)":::entity : "belongs to"
    Product 0+ optionally to 1+ "Product(s)":::shouldRel : "has related"
    Product 0+ optionally to 1+ "Product Variants(s)":::shouldRel : "has variant"
    Product 0+ optionally to 1+ "Media(s)":::couldRel : "has media"
    Product 1 to 1+ Inventory:::entity : "has stock in"
    Product 0+ optionally to 1+ Pricing:::entity : "has pricing for"
    Product 1 optionally to 0+ "Shipping Method":::optionalRel : "eligible for"


    %% Cart relationships
    Cart:::entity 1 to 1 Customer:::entity : "belongs to"
    Cart 0+ optionally to 1+ Product:::entity : "contains"
    Cart 1 optionally to 0+ "Shipping Method":::optionalRel : "has"
    Cart 1 optionally to 0+ "Payment":::optionalRel : has

    %% Order relationships
    Order:::entity 1 to 1 Customer:::entity : "placed by"
    Order 1 to 1+ Product:::entity : "contains"
    Order 1 to 1 Payment:::entity : "paid via"
    Order 0+ optionally to 1 "Shipping Method":::entity : "shipped via"
    Order 0+ optionally to 1+ Promotion:::entity : "uses"
    Order 1 to 1+ "Order History":::entity : "tracks in"

    %% Promotion relationships
    Promotion:::entity 0+ optionally to 1+ Product:::entity : "applies to"
    Promotion 0+ optionally to 1+ "Coupon Instance":::couldRel : "generates"

    %% Customer relationships
    Customer:::entity 0+ optionally to 1+ Campaign:::entity : "targeted by"

    %% Pricing relationships
    Pricing:::entity 1 to 1 Product:::entity : "applies to"

    %% Inventory relationships
    Inventory:::entity 1 to 1 Product:::entity : "tracks"

    classDef entity fill:#ffd100, stroke:#ffd100,stroke-width:2px
    classDef shouldRel fill:#ffd10080, stroke:#ffd10080,stroke-width:1px
    classDef couldRel stroke:#b5b5b5, stroke-dasharray: 1 1, fill:#f3f3f3, stroke-width:2px

```
> [!NOTE]
> Unlinked entities are in progress.

## Product
- [Product](product/product.md)
- [Product Type](product/product-type.md)
- Catalog *(coming soon)*
- [Category](product/category.md)

## Cart
- [Cart](cart/cart.md)

## Order
- [Order](order/order.md)
- [Order History](order/order-history.md)
  
## Payment
- [Payment](payment/payment.md)

## Fulfillment
- [Fulfillment](fulfillment/fulfillment.md)
- [Shipping Method](fulfillment/shipping-method.md)

## Pricing
- [Pricing](pricing/pricing.md)

## Promotion
- [Promotion](promotion/promotion.md)
- [Coupon Instance](promotion/coupon-instance.md)

## Inventory
- [Inventory](inventory/inventory.md)

## Identity
- [Customer](identity/customer.md)

## Campaign
- Campaign *(coming soon)*

### Utility functions
- [Address](utilities/address.md)
- Channel *(coming soon)*
- Contact *(coming soon)*
- Identifier *(coming soon)*
- [Language](utilities/language.md)
- [Media](utilities/media.md)
- [Money](utilities/money.md)
- Store *(coming soon)*
