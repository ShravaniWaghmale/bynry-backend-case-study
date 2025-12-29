// Part 3: Low-Stock Alerts API

// Assumptions
- Recent sales are within the last 30 days
- Low-stock threshold is stored per product
- Products may have multiple suppliers

// API Logic (Node.js-style Pseudocode)

```js
async function getLowStockAlerts(companyId) {
  alerts = [];

  inventories = fetchInventoriesByCompany(companyId);

  for (inventory of inventories) {
    if (
      inventory.quantity < inventory.product.lowStockThreshold &&
      inventory.product.hasRecentSales
    ) {
      daysLeft = calculateDaysUntilStockout(inventory);

      alerts.push({
        product_id: inventory.product.id,
        product_name: inventory.product.name,
        sku: inventory.product.sku,
        warehouse_id: inventory.warehouse.id,
        warehouse_name: inventory.warehouse.name,
        current_stock: inventory.quantity,
        threshold: inventory.product.lowStockThreshold,
        days_until_stockout: daysLeft,
        supplier: inventory.product.suppliers[0] || null
      });
    }
  }

  return {
    alerts,
    total_alerts: alerts.length
  };
}
