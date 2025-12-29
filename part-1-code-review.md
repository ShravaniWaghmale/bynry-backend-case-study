//Part 1: Code Review & Debugging

// Issues Identified
- No input validation for request data
- SKU uniqueness is not enforced
- No transaction handling, leading to partial data saves
- Price precision issues (float instead of decimal)
- No error handling
- Assumes product belongs to only one warehouse

// Impact in Production
- Duplicate SKUs can exist
- Product may be created without inventory
- Incorrect pricing calculations
- API instability during failures

// Corrected Logic (Node.js-style Pseudocode)

```
async function createProduct(data) {

  if (!data.name || !data.sku || !data.warehouseId) {
    return error("Invalid input");
  }

  if (SKU already exists in database) {
    return error("Duplicate SKU");
  }

  startTransaction();

  try {
    create Product (name, sku, price as DECIMAL);
    create Inventory (productId, warehouseId, quantity default 0);
    commitTransaction();
    return success;
  } catch (error) {
    rollbackTransaction();
    return failure;
  }
}
