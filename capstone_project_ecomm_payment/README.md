# Ecommerce payment method analysis
Notebook: https://github.com/piyalidas28/ML_AI_UCB/blob/main/capstone_project_ecomm_payment/ecomm.ipynb

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
* Merged all the datasets into one
  * There seemed to be a 1-1 relationship between the primary keys of each dataset with the other
* Dropped the test dataset already provided because 3 columns were missing compared to training dataset: 'order_status', 'order_estimated_delivery_date', 'order_delivered_timestamp'
* Dropped the following columns as they seemed unnecessary
  * order_status // happens after the payment is made
  * order_purchase_timestamp  // converted into 3 more columns
  * order_approved_at
  * order_delivered_timestamp
  * order_estimated_delivery_date
  * order_id, customer_id, product_id  // not necessary after the merge
  * length, bredth, width  // not necessary after coverting to volume_category
  * payment_sequential, payment_installments  // these are highly correlated to payment_type
  * customer_city, customer_state  // highly correlated to the pin code prefix
### Feature engineering
I added the following features:
* order_purchase_hour, order_purchase_day, order_purchase_month
  * Derived these features from order_purchase_timestamp
* vol_category
  * product volumee is computed from the length, breadth and width of the package
  * Created 3 new categories: small: 1 (less than 25 percentile), medium: 2 (between 25 and 75 percentile) and large: 3 (more than 75th percentile)
* weight_category
  * Similar to vol_category, created 3 new categories from product_weight_g column 
## Exploratory Data Analysis
**Payment types**: Majority of payment is done by credit cards.
![image](https://github.com/user-attachments/assets/7ffa0d26-39ee-4202-ad6d-9d021c6de643)

**Timeseries of number of orders**: We can see mild weekly cycle and overall there's a gradual increase in number of orders
![image](https://github.com/user-attachments/assets/087c8bfe-013b-43a1-8845-a2a8a93e5e79)

**Price histogram**
![image](https://github.com/user-attachments/assets/1bebf31a-d246-4835-8483-237c9484d400)


**Product category**: Toys comprise of majority of the product categories bought on the ecommerce website.
![image](https://github.com/user-attachments/assets/6c466e86-4e51-4f8e-b5d8-547f077e697d)

**Bivariet analysis**
![image](https://github.com/user-attachments/assets/493673da-3631-4562-828e-81f9443a52fb)

### Final dataset
* Created train/test datasets by splitting 80/20
* Used OrdinalEncoder to convert categorical columns into numerical ![image](https://github.com/user-attachments/assets/ae523dc3-03e4-4836-9dfd-98f4643d8e5b)

## Modeling
This is a multi-class classification problem. The target feature (payment_type) has 4 values (4 classes).
### Model performance
![image](https://github.com/user-attachments/assets/0399b1f7-b969-405b-8049-ff49a4420907)
#### Confusion Matrices
![image](https://github.com/user-attachments/assets/d8e22da0-c52c-4c0d-95b1-7200ed091983) | ![image](https://github.com/user-attachments/assets/f5eda1fe-dc10-466b-b2f3-950a881a9d40) ![image](https://github.com/user-attachments/assets/5f06fd46-f864-4ec2-9e66-a9c7e93cecc4) ![image](https://github.com/user-attachments/assets/dfd98503-3c46-4ab6-a437-4fb038c09ae1) ![image](https://github.com/user-attachments/assets/7665bab5-c042-4912-b6d5-1605dd4559a6) ![image](https://github.com/user-attachments/assets/6e46d6d3-4563-44e7-8332-09bec3b1d56c)

#### Comparison by individual matrices
![image](https://github.com/user-attachments/assets/1f4aa0e7-7573-476b-9bb8-98b6b07b4bef)
![image](https://github.com/user-attachments/assets/c3d16bc2-c74e-4a8d-b953-b2efceff1279)
![image](https://github.com/user-attachments/assets/77e175f6-3a90-4bda-9123-e9aa78f4f216)
![image](https://github.com/user-attachments/assets/19a43fc3-7583-4a12-be55-9e1f894910c8)
![image](https://github.com/user-attachments/assets/6c7298f2-613d-4041-8272-26c4e84426be)

### Feature importance
Feature importance analysis shows that payment related fields are the most important, followed by product category, seller, location and then other features.
![image](https://github.com/user-attachments/assets/29f363d1-5730-49f7-9f3b-37e45bd9ee5a)

## Next steps
I propose to
* further iterate over this dataset by adding new features and also removing strongly correlated features (de-duplicating payment related features)
* try the other approach to drop the columns missing in test dataset from training dataset and use both the sets of datasets in your analysis
* try to fetch data in the test dataset as well
* explore neural network to see if it improves the performance of the model
* Improve efficiency of the models, specifically Logistic regression and Gradient boosting
* Deploy the model for realtime prediction in one of the use cases discussed above
* Setup a feedback loop to continuously improve the model






