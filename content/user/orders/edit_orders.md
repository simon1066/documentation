---
title: Edit Orders
description: Modifying an order after it has been placed 
category: email
weight: 10
---

[Edit Orders](https://www.zen-cart.com/downloads.php?do=file&id=1513) is a plugin which allows you to modify orders after they have been placed. This can be useful in a number of situations: 

- Refunds or cancelled orders 
- Customer changed their mind or made a mistake 
- Product no longer available

Viewing an order in Edit Orders looks the same as viewing it in the Order Details screen, except that all fields are presented in an editable form.  In addition, products may be added to or removed from the order.

![Edit Orders](/images/edit_orders.jpg)

Note that using Edit Orders to increase the value of an order means you will have to manually [collect the balance owed](/user/payment/balance_owed/); this is not done automatically.

## Edit Orders Plugins 

- [Edit Orders Detail Record Copy](https://www.zen-cart.com/downloads.php?do=file&id=2292) is a plugin that preserves the contents of the `orders_products` table records for an order being edited.  This is useful for users of plugins which append to the `orders_products` table, such as [Drop Ship Purchase Orders](https://www.zen-cart.com/downloads.php?do=file&id=688).

