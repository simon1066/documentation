---
title: Orders
description: Zen Cart Orders Admin Page 
category: admin_pages
weight: 20
---

The Orders page allows you to view your orders. 

It shows your orders in paginated list, with one line per order.  The most recently received order is shown first.  

<img src="/images/orders_list.png" alt="Zen Cart Orders Screen" />
<br><br>

The columns in the list are: 

- Order ID  
- Payment and Shipping - the payment module and shipping module names are shown in stacked format.  
- Customer's name (with company name, if applicable, shown below) 
- Total value of the order
- Date purchased 
- [Order Status](/user/localization/orders_status/)
- Customer comments on the order are indicated by a yellow square.  

To the left of the order id, a red dot indicates that the order's shipping address is different from the billing address. Such orders are a greater fraud risk, which is why they are flagged in this way. 

Clicking an order selects it and opens a preview on the right hand side of the page.  From there, the order may be opened or deleted.  The invoice or packingslip for an order may also be opened from the preview. 

Opening an order displays the order details screen, which shows the customer information, order contents, and order history.  The order status may be updated from this screen.  Updating the order status permits you to optionally send an email to the customer with the updated status and a brief note.

<img src="/images/order_update.png" alt="Zen Cart Orders Updating " />
<br><br>

In this order, the first history entry is from when the order was placed, the second was done by an administrator and resulted in an email to the customer, and the third was done by an administrator and will only be visible in the admin, and not to the customer.


For more information, see the [customer and order FAQs](/user/orders/). 