# Ecommerce payment method analysis

## Description
Payment instrument is a crucial part of shopping online and can provide crucial insights for multiple purposes:
1. Personalized Customer Experience:
  a. Tailored payment options: Offer payment methods that align with customer preferences and demographics, improving user satisfaction and conversion rates.
  b. Reduced friction: Avoid presenting irrelevant payment options, streamlining the checkout process and minimizing abandoned carts.
2. Fraud Prevention:
  a. Risk assessment: Identify high-risk transactions based on payment method and customer behavior patterns, helping to detect and prevent fraudulent activity.
  b. Anomaly detection: Flag unusual payment choices that deviate from customer norms, alerting merchants to potential fraud attempts.
3. Marketing and Promotions:
  a. Targeted campaigns: Design marketing campaigns that resonate with specific payment method segments, increasing the effectiveness of promotions.
  b. Offer optimization: Tailor promotional offers to the preferred payment methods of customers, maximizing their appeal and redemption rates.
4. Inventory Management:
  a. Demand forecasting: Predict payment method usage to anticipate product demand and optimize inventory levels accordingly.
  b. Supply chain management: Ensure adequate supply of products to meet demand, avoiding stockouts or excess inventory.
5. Payment Infrastructure Optimization:
  a. Cost management: Evaluate the profitability of different payment methods to allocate resources effectively and minimize processing costs.
  b. Gateway selection: Select payment gateways that align with customer preferences and business objectives, ensuring a smooth and efficient checkout experience.

## Business Objective
**Predict the payment method for an order**

Identify the features influencing the payment method of a customer for a particular order and develop a method to predict the payment method.

## Dataset
Source: https://www.kaggle.com/datasets/bytadit/ecommerce-order-dataset
The E-commerce Order Dataset provides comprehensive information related to orders, items within orders, customers, payments, and products for an e-commerce platform for a sample of about 89K orders on an ecommerce platform. This dataset is structured with multiple tables, each containing specific information about various aspects of the e-commerce operations.

### Orders Table:
* order_id: Unique identifier for an order, acting as the primary key.
* customer_id: Unique identifier for a customer. This table may not be unique at this level.
* order_status: Indicates the status of an order (e.g., delivered, cancelled, processing, etc.).
* order_purchase_timestamp: Timestamp when the order was made by the customer.
* order_approved_at: Timestamp when the order was approved from the seller's side.
* order_delivered_timestamp: Timestamp when the order was delivered at the customer's location.
* order_estimated_delivery_date: Estimated date of delivery shared with the customer while placing the order.

### Order Items Table
* order_id: Unique identifier for an order.
* order_item_id: Item number in each order, acting as part of the primary key along with the order_id.
* product_id: Unique identifier for a product.
* seller_id: Unique identifier for the seller.
* price: Selling price of the product.
* shipping_charges: Charges associated with the shipping of the product.

### Customers Table
* customer_id: Unique identifier for a customer, acting as the primary key.
* customer_zip_code_prefix: Customer's Zip code.
* customer_city: Customer's city.
* customer_state: Customer's state.

### Payments Table
* order_id: Unique identifier for an order.
* payment_sequential: Provides information about the sequence of payments for the given order.
* payment_type: Type of payment (e.g., credit_card, debit_card, etc.).
* payment_installments: Payment installment number in case of credit cards.
* payment_value: Transaction value.

### Products Table
* product_id: Unique identifier for each product, acting as the primary key.
* product_category_name: Name of the category the product belongs to.
* product_weight_g: Product weight in grams.
* product_length_cm: Product length in centimeters.
* product_height_cm: Product height in centimeters.
* product_width_cm: Product width in centimeters.

## Data inspection and preparation
## Exploratory Data Analysis
![image](https://github.com/user-attachments/assets/4a7faede-14ae-45f5-bc9c-dc6b38cda6ee)
* Payment types: Majority of payment is done by credit cards.
* Product category: Toys comprise of majority of the product categories bought on the ecommerce website.
* Location: Locations close to the major city of Brazil (Sao Paolo) is where there are a lot of data points.

