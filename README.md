# SQL Practice Questions

A comprehensive collection of SQL practice questions covering various concepts from basic to advanced level.

> **Note:** Please do not use any functions which are not taught in the class. Solve the questions only with the concepts that have been discussed so far.

---

## Table of Contents

1. [Basic SQL Queries](#1-basic-sql-queries)
2. [Aggregate Functions & GROUP BY](#2-aggregate-functions--group-by)
3. [JOIN Based Questions](#3-join-based-questions)
4. [String Manipulation & Complex Queries](#4-string-manipulation--complex-queries)
5. [Subqueries](#5-subqueries)
6. [Window Functions & Advanced Queries](#6-window-functions--advanced-queries)
7. [Rolling Aggregations & Time Series](#7-rolling-aggregations--time-series)
8. [External Practice Problems](#8-external-practice-problems)

---

## 1. Basic SQL Queries

### Q1. Pattern Matching with LIKE
Write a SQL to get all the orders where customer's name has "a" as second character and "d" as fourth character.

**Expected Rows:** 58

<details>
<summary>Solution</summary>

```sql
SELECT * FROM orders WHERE customer_name LIKE '_a_d%';
```
</details>

---

### Q2. Date Range Filtering
Write a SQL to get all the orders placed in the month of December 2020.

**Expected Rows:** 352

<details>
<summary>Solution</summary>

```sql
SELECT * FROM orders WHERE order_date BETWEEN '2020-12-01' AND '2020-12-31';
```
</details>

---

### Q3. NOT IN with Date Condition
Write a query to get all the orders where ship_mode is neither in 'Standard Class' nor in 'First Class' and ship_date is after November 2020.

**Expected Rows:** 944

<details>
<summary>Solution</summary>

```sql
SELECT * FROM orders 
WHERE ship_mode NOT IN ('Standard Class', 'First Class')
AND ship_date > '2020-11-30';
```
</details>

---

### Q4. NOT LIKE Pattern
Write a query to get all the orders where customer name neither starts with "A" nor ends with "n".

**Expected Rows:** 9815

<details>
<summary>Solution</summary>

```sql
SELECT * FROM orders WHERE customer_name NOT LIKE 'A%n';
```
</details>

---

### Q5. Negative Values
Write a query to get all the orders where profit is negative.

**Expected Rows:** 1871

<details>
<summary>Solution</summary>

```sql
SELECT * FROM orders WHERE profit < 0;
```
</details>

---

### Q6. OR Condition
Write a query to get all the orders where either quantity is less than 3 or profit is 0.

**Expected Rows:** 3348

<details>
<summary>Solution</summary>

```sql
SELECT * FROM orders WHERE profit = 0 OR quantity < 3;
```
</details>

---

### Q7. Multiple Conditions
Your manager handles the sales for South region and he wants you to create a report of all the orders in his region where some discount is provided to the customers.

**Expected Rows:** 815

<details>
<summary>Solution</summary>

```sql
SELECT * FROM orders WHERE region = 'South' AND discount > 0;
```
</details>

---

### Q8. TOP N with ORDER BY
Write a query to find top 5 orders with highest sales in furniture category.

<details>
<summary>Solution</summary>

```sql
SELECT TOP 5 * FROM orders WHERE category = 'Furniture' ORDER BY sales DESC;
```
</details>

---

### Q9. Multiple Category Filter with Date
Write a query to find all the records in technology and furniture category for the orders placed in the year 2020 only.

**Expected Rows:** 1021

<details>
<summary>Solution</summary>

```sql
SELECT * FROM orders 
WHERE category IN ('Furniture', 'Technology') 
AND order_date BETWEEN '2020-01-01' AND '2020-12-31';
```
</details>

---

### Q10. Cross Year Orders
Write a query to find all the orders where order date is in year 2020 but ship date is in 2021.

**Expected Rows:** 33

<details>
<summary>Solution</summary>

```sql
SELECT * FROM orders 
WHERE order_date BETWEEN '2020-01-01' AND '2020-12-31' 
AND ship_date BETWEEN '2021-01-01' AND '2021-12-31';
```
</details>

---

## 2. Aggregate Functions & GROUP BY

### Q1. Update Statement
Write an update statement to update city as null for order ids: CA-2020-161389, US-2021-156909

---

### Q2. NULL Check
Write a query to find orders where city is null.

**Expected Rows:** 2

---

### Q3. Aggregate with GROUP BY
Write a query to get total profit, first order date and latest order date for each category.

---

### Q4. HAVING with Subquery Logic
Write a query to find sub-categories where average profit is more than the half of the max profit in that sub-category.

---

### Q5. Self Join for Comparison

**Setup Script:**
```sql
CREATE TABLE exams (
    student_id INT, 
    subject VARCHAR(20), 
    marks INT
);

INSERT INTO exams VALUES 
(1, 'Chemistry', 91), (1, 'Physics', 91), (1, 'Maths', 92),
(2, 'Chemistry', 80), (2, 'Physics', 90),
(3, 'Chemistry', 80), (3, 'Maths', 80),
(4, 'Chemistry', 71), (4, 'Physics', 54),
(5, 'Chemistry', 79);
```

Write a query to find students who have got same marks in Physics and Chemistry.

---

### Q6. COUNT with GROUP BY
Write a query to find total number of products in each category.

---

### Q7. TOP N by Region
Write a query to find top 5 sub categories in west region by total quantity sold.

---

### Q8. Multiple GROUP BY
Write a query to find total sales for each region and ship mode combination for orders in year 2020.

---

## 3. JOIN Based Questions

> **Video Reference:** [Most Asked SQL JOIN based Interview Question](https://www.youtube.com/watch?v=xR87ctOgpAE)

**Setup Script:** Run the following command to add and update dob column in employee table:
```sql
ALTER TABLE employee ADD dob DATE;
UPDATE employee SET dob = DATEADD(YEAR, -1 * emp_age, GETDATE());
```

---

### Q1. Self Join with Date Calculation
Write a query to print emp name, their manager name and difference in their age (in days) for employees whose year of birth is before their manager's year of birth.

---

### Q2. LEFT JOIN with NULL Check
Write a query to find subcategories who never had any return orders in the month of November (irrespective of years).

---

### Q3. Single Product Orders
Orders table can have multiple rows for a particular order_id when customers buy more than 1 product in an order. Write a query to find order ids where there is only 1 product bought by the customer.

---

### Q4. STRING_AGG / GROUP_CONCAT
Write a query to print manager names along with the comma separated list (order by emp salary) of all employees directly reporting to him.

---

### Q5. Business Days Calculation
Write a query to get number of business days between order_date and ship_date (exclude weekends). Assume that all order date and ship date are on weekdays only.

---

### Q6. Return Orders Analysis
Write a query to print 3 columns: category, total_sales and total sales of returned orders.

---

### Q7. Pivot by Year
Write a query to print below 3 columns:
- category
- total_sales_2019 (sales in year 2019)
- total_sales_2020 (sales in year 2020)

---

### Q8. Average Days by City
Write a query to print top 5 cities in west region by average number of days between order date and ship date.

---

### Q9. Multi-Level Hierarchy
Write a query to print emp name, manager name and senior manager name (senior manager is manager's manager).

---

## 4. String Manipulation & Complex Queries

### ICC World Cup Problem

**Setup Script:**
```sql
CREATE TABLE icc_world_cup (
    Team_1 VARCHAR(20),
    Team_2 VARCHAR(20),
    Winner VARCHAR(20)
);

INSERT INTO icc_world_cup VALUES 
('India', 'SL', 'India'),
('SL', 'Aus', 'Aus'),
('SA', 'Eng', 'Eng'),
('Eng', 'NZ', 'NZ'),
('Aus', 'India', 'India');
```

### Q1. Match Statistics
Write a query to produce below output from icc_world_cup table:
- team_name
- no_of_matches_played
- no_of_wins
- no_of_losses

---

### Q2. Split Customer Name
Write a query to print first name and last name of a customer using orders table (everything after first space can be considered as last name).

**Output columns:** customer_name, first_name, last_name

---

### Drivers Problem

**Setup Script:**
```sql
CREATE TABLE drivers (
    id VARCHAR(10), 
    start_time TIME, 
    end_time TIME, 
    start_loc VARCHAR(10), 
    end_loc VARCHAR(10)
);

INSERT INTO drivers VALUES 
('dri_1', '09:00', '09:30', 'a', 'b'),
('dri_1', '09:30', '10:30', 'b', 'c'),
('dri_1', '11:00', '11:30', 'd', 'e'),
('dri_1', '12:00', '12:30', 'f', 'g'),
('dri_1', '13:30', '14:30', 'c', 'h'),
('dri_2', '12:15', '12:30', 'f', 'g'),
('dri_2', '13:30', '14:30', 'c', 'h');
```

### Q3. Profit Rides Analysis
Write a query to print below output using drivers table. Profit rides are the number of rides where end location of a ride is same as start location of immediate next ride for a driver.

**Expected Output:**
| id | total_rides | profit_rides |
|----|-------------|--------------|
| dri_1 | 5 | 1 |
| dri_2 | 2 | 0 |

---

### Q4. Character Count
Write a query to print customer name and number of occurrence of character 'n' in the customer name.

**Output columns:** customer_name, count_of_occurence_of_n

---

### Q5. Hierarchy Sales Report
Write a query to print below output from orders data:

| hierarchy_type | hierarchy_name | total_sales_in_west_region | total_sales_in_east_region |
|----------------|----------------|----------------------------|----------------------------|
| category | Technology | ... | ... |
| category | Furniture | ... | ... |
| category | Office Supplies | ... | ... |
| sub_category | Art | ... | ... |
| sub_category | Furnishings | ... | ... |

Include all category, subcategory and ship_mode hierarchies.

---

### Q6. Orders by Country
The first 2 characters of order_id represents the country of order placed. Write a query to print total number of orders placed in each country.

> Note: An order can have 2 rows in the data when more than 1 item was purchased in the order but it should be considered as 1 order.

---

## 5. Subqueries

### Q1. Premium Customers
Write a query to find premium customers from orders data. Premium customers are those who have done more orders than average number of orders per customer.

---

### Q2. Above Department Average Salary
Write a query to find employees whose salary is more than average salary of employees in their department.

---

### Q3. Above Average Age
Write a query to find employees whose age is more than average age of all the employees.

---

### Q4. Highest Salary per Department
Write a query to print emp name, salary and dep id of highest salaried employee in each department.

---

### Q5. Overall Highest Salary
Write a query to print emp name, salary and dep id of highest salaried overall.

---

### Q6. Highest Selling Products
Write a query to print product id and total sales of highest selling products (by number of units sold) in each category.

---

## 6. Window Functions & Advanced Queries

### Q1. Nth Highest Salary
Write a query to print 3rd highest salaried employee details for each department (give preference to younger employee in case of a tie). In case a department has less than 3 employees then print the details of highest salaried employee in that department.

---

### Q2. Top & Bottom Products
Write a query to find top 3 and bottom 3 products by sales in each region.

---

### Q3. Month Over Month Growth
Among all the sub categories, which sub category had highest month over month growth by sales in Jan 2020?

---

### Q4. Year Over Year Growth
Write a query to print top 3 products in each category by year over year sales growth in year 2020.

---

### Q5. Call Duration Analysis

**Setup Script:**
```sql
CREATE TABLE call_start_logs (
    phone_number VARCHAR(10),
    start_time DATETIME
);

INSERT INTO call_start_logs VALUES
('PN1', '2022-01-01 10:20:00'),
('PN1', '2022-01-01 16:25:00'),
('PN2', '2022-01-01 12:30:00'),
('PN3', '2022-01-02 10:00:00'),
('PN3', '2022-01-02 12:30:00'),
('PN3', '2022-01-03 09:20:00');

CREATE TABLE call_end_logs (
    phone_number VARCHAR(10),
    end_time DATETIME
);

INSERT INTO call_end_logs VALUES
('PN1', '2022-01-01 10:45:00'),
('PN1', '2022-01-01 17:05:00'),
('PN2', '2022-01-01 12:55:00'),
('PN3', '2022-01-02 10:20:00'),
('PN3', '2022-01-02 12:50:00'),
('PN3', '2022-01-03 09:40:00');
```

Write a query to get start time and end time of each call from above 2 tables. Also create a column of call duration in minutes.

> Note: There will be multiple calls from one phone number and each entry in start table has a corresponding entry in end table.

---

## 7. Rolling Aggregations & Time Series

### Q1. Rolling 3 Month Sales
Write a SQL to find top 3 products in each category by highest rolling 3 months total sales for Jan 2020.

---

### Q2. Never Declining Sales
Write a query to find products for which month over month sales has never declined.

---

### Q3. Sales vs Previous 2 Months
Write a query to find month wise sales for each category for months where sales is more than the combined sales of previous 2 months for that category.

---

## 8. External Practice Problems

Practice these problems on [NamasteSQL](https://www.namastesql.com):

### Intermediate Level
| # | Problem | Link |
|---|---------|------|
| 1 | Product Reviews | [Problem #38](https://www.namastesql.com/coding-problem/38-product-reviews) |
| 2 | Category Sales Part 1 | [Problem #61](https://www.namastesql.com/coding-problem/61-category-sales-part-1) |
| 3 | Category Sales Part 2 | [Problem #62](https://www.namastesql.com/coding-problem/62-category-sales-part-2) |
| 4 | Department Average Salary | [Problem #71](https://www.namastesql.com/coding-problem/71-department-average-salary) |
| 5 | Product Sales | [Problem #72](https://www.namastesql.com/coding-problem/72-product-sales) |
| 6 | Category Product Count | [Problem #73](https://www.namastesql.com/coding-problem/73-category-product-count) |
| 7 | Employee Mentor | [Problem #103](https://www.namastesql.com/coding-problem/103-employee-mentor) |

### Advanced Level
| # | Problem | Link |
|---|---------|------|
| 1 | Library Borrowing Habits | [Problem #8](https://www.namastesql.com/coding-problem/8-library-borrowing-habits) |
| 2 | Loan Repayment | [Problem #52](https://www.namastesql.com/coding-problem/52-loan-repayment) |
| 3 | Lowest Price | [Problem #55](https://www.namastesql.com/coding-problem/55-lowest-price) |
| 4 | Penultimate Order | [Problem #64](https://www.namastesql.com/coding-problem/64-penultimate-order) |
| 5 | Dynamic Pricing | [Problem #26](https://www.namastesql.com/coding-problem/26-dynamic-pricing) |
| 6 | Amazon Notifications | [Problem #76](https://www.namastesql.com/coding-problem/76-amazon-notifications) |

---

## Dataset Information

This practice set uses the following tables:
- **orders** - Contains order details with customer info, dates, products, sales, profit, etc.
- **returns** - Contains return order information
- **employee** - Contains employee details with manager relationships

---

## Tips for Practice

1. **Start with basic queries** before moving to complex ones
2. **Understand the data** - Run SELECT queries first to understand the table structure
3. **Break down complex problems** into smaller parts
4. **Test with expected row counts** where provided
5. **Practice writing clean, readable SQL** with proper formatting

---

*Good luck with your SQL practice!* 🚀
