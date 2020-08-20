# FoodDelivery
Summary of the purpose of the project:

Managing a food-delivery services ,such as , adding new customers , food menu items , making an order , and eventually providing some statistics

Methods of the project:

The class named Delivery represents the delivery company.

In order to access the service, a subscription must be activated using the method newCustomer(), which accepts as parameters: the name of the customer, his address, telephone number and email; the method returns the unique CUSTOMER ID, that is, an integer number starting from 1 and then progressively increased. If the same email is already associated to another customer, the methods throw an exception DeliveryException.

Given a CUSTOMER ID it is possible to retrieve his information using the method customerInfo(), which returns a string formatted as "NAME, ADDRESS, TEL, EMAIL", e.g., "Rossi Giovanni, C.so Duca degli Abruzzi 25, 011 555666, greds@torino.it".

The list of all customers is returned by the method listCustomers(), which yields, for each customer, a string in the same format; strings are sorted alphabetically by name.

The menu of available food can be defined, one entry at a time, using the method newMenuItem(), which gets as parameters the description, the price, the category, and the time required to prepare it (preparation time).

Existing items in the menu may be found using the method findItem(), which gets a pattern as a string, and returns all menu items whose description includes the pattern (case insensitive), e.g., the pattern "pizza" would match "Chinese noodles". The empty pattern ("") is included in all menu items. Individual menu items are represented by a string in the format "[CATEGORY] DESCRIPTION : PRICE", e.g., "[MAIN COURSE] Chinese noodles : 8.50". The result of the search is sorted alphabetically by category, then by description.

To create a new order the user calls the method newOrder(), which gets a CUSTOMER ID and returns a unique ORDER ID, that is, an integer number starting at 1 for the first order and then progressively incremented.

It is possible to add new items to an order by selecting a menu item via the method addItem(), which gets as parameters the ORDER ID, a search pattern, and the quantity. The method adds the menu item to the order with the specified quantity. The search pattern must identify exactly one menu item and the ORDER ID must be valid, otherwise the method throws the exception DeliveryException. If the order already contains the specified item, the quantity is added to the current one. The method returns the final quantity of the specified item in the order.

The method showOrder() allows to check the content of an order. It gets the ORDER ID as an argument, and returns the list of items, each one in the format "DESCRIPTION, QUANTITY". If the ORDER ID is not valid, the method throws the exception DeliveryException.

The method totalOrder() gets an ORDER ID parameter and returns the total for that order. That is, the sum of item's quantity multiplied by item's price. If the ORDER ID is not valid, the method throws the exception DeliveryException.

Preparation and delivery each order goes through different states, that can be checked via the method getStatus(), which gets as parameter the ORDER ID and returns the status as an enum of type OrderStatus. An order is initially in the state NEW.

An order can be confirmed via the method confirm() that changes the order's status to CONFIRMED and returns an estimate of the delivery time in minutes. The delivery time is calculated as a sum of (a) a fixed initial delay of 5 minutes, (b) the maximum among the preparation times, and (c) 15 minutes fixed transport time. If the ORDER ID is not valid, or the order is not in the state NEW, the method throws the exception DeliveryException.

Then, the state of an order may be changed to PREPARATION by the method start(), which returns the estimate delivery time, as the sum of (b) and (c) of the previous point. If the ORDER ID is not valid, or the order is not in the state CONFIRMED, the method throws the exception DeliveryException. After preparation, the status of an order may be changed to ON_DELIVERY by the method deliver(), which returns the estimate delivery time, that is, (c) of the previous point. If the ORDER ID is not valid, or the order is not in the state PREPARATION, the method throws the exception DeliveryException.

Eventually, the delivery is recorded by calling the method complete(), which changes the status to DELIVERED. If the ORDER ID is not valid, or the order is not in the state ON_DELIVERY, the method throws the exception DeliveryException.

All the reports are computed including only orders that have been previously confirmed. The method totalCustomer() gets a CUSTOMER ID as parameter and returns the total of his orders.

The method bestCustomers() ranks customers according to their orders. It returns a map with the total of the orders as key, and the list of the customers that ordered such a total value. Customers are represented with strings in the format specified in Delivery Class. the map is sorted by decreasing total.
