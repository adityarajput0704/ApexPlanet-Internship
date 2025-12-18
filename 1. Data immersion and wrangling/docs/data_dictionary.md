# **Data Dictionary**

### **Customer Identification**

| Column Name | Data Type | Description                         | Business Relevance                       |
| ----------- | --------- | ----------------------------------- | ---------------------------------------- |
| Customer ID | String    | Unique identifier for each customer | Helps analyze customer purchase behavior |



### **Transactions Details**

| Column Name      | Data Type | Description                            | Business Relevance                        |
| ---------------- | --------- | -------------------------------------- | ----------------------------------------- |
| Transaction ID   | String    | Unique identifier for each transaction | Used to uniquely track sales transactions |
| Transaction Date | Date      | Date when the transaction occurred     | Enables time-based sales analysis         |


### **Product Information**

| Column Name | Data Type   | Description                                   | Business Relevance                        |
| ----------- | ----------- | --------------------------------------------- | ----------------------------------------- |
| Category    | Categorical | Product category (e.g., Grocery, Electronics) | Helps identify high-performing categories |
| Item        | String      | Name of the purchased item                    | Enables item-level sales analysis         |



### **Pricing and Quantity Details**

| Column Name    | Data Type | Description                           | Business Relevance        |
| -------------- | --------- | ------------------------------------- | ------------------------- |
| Price Per Unit | Float     | Price of a single unit of the product | Used to calculate revenue |
| Quantity       | Integer   | Number of units purchased             | Indicates purchase volume |
| Total Spent    | Float     | Total amount spent in the transaction | Primary revenue metric    |



### **Payment and Location Details**

| Column Name    | Data Type   | Description                                     | Business Relevance                         |
| -------------- | ----------- | ----------------------------------------------- | ------------------------------------------ |
| Payment Method | Categorical | Method used for payment (Cash, Card, UPI, etc.) | Helps analyze payment preferences          |
| Location       | Categorical | Store or branch location                        | Enables location-wise performance analysis |



### **Discount Information**

| Column Name      | Data Type            | Description                              | Business Relevance                    |
| ---------------- | -------------------- | ---------------------------------------- | ------------------------------------- |
| Discount Applied | Categorical (Yes/No) | Indicates whether a discount was applied | Helps evaluate discount effectiveness |



