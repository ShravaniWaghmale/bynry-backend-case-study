## part-2-database-design.md

```md

// Core Tables
- Company(id, name)
- Warehouse(id, companyId)
- Product(id, sku UNIQUE, name, price, lowStockThreshold)
- Inventory(id, productId, warehouseId, quantity)
- InventoryLog(id, inventoryId, changeQuantity, timestamp)
- Supplier(id, name, contactEmail)
- ProductSupplier(productId, supplierId)

// Missing Requirements / Questions
- How is "recent sales" defined?
- Can a product have multiple suppliers?
- Is low-stock threshold product-level or warehouse-level?

// Design Decisions
- Inventory is tracked per warehouse
- Unique SKU ensures consistency
- InventoryLog supports audit and history tracking
- Many-to-many relationship for suppliers
