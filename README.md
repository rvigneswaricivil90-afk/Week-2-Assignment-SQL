CREATE DATABASE salesDB;
USE SalesDB;
CREATE TABLE Customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100),
    city VARCHAR(50),
    country VARCHAR(50)
);
INSERT INTO Customers VALUES
(1, 'Arun Kumar', 'Chennai', 'India'),
(2, 'Priya Sharma', 'Bangalore', 'India'),
(3, 'John Smith', 'New York', 'USA'),
(4, 'Sneha Reddy', 'Hyderabad', 'India'),
(5, 'David Lee', 'London', 'UK');
CREATE TABLE Products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    category VARCHAR(50),
    unit_price DECIMAL(10,2)
);
INSERT INTO Products VALUES
(101, 'Laptop', 'Electronics', 75000),
(102, 'Mouse', 'Electronics', 500),
(103, 'Keyboard', 'Electronics', 1200),
(104, 'Office Chair', 'Furniture', 8500),
(105, 'Desk', 'Furniture', 12000);
CREATE TABLE Sales (
    sales_id INT PRIMARY KEY,
    customer_id INT,
    product_id INT,
    quantity INT,
    sales_date DATE,
    total_price DECIMAL(10,2),
    
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id),
    FOREIGN KEY (product_id) REFERENCES Products(product_id)
);
INSERT INTO Sales VALUES
(1, 1, 101, 1, '2025-01-10', 75000),
(2, 2, 102, 2, '2025-01-11', 1000),
(3, 3, 103, 1, '2025-01-12', 1200),
(4, 4, 104, 1, '2025-01-13', 8500),
(5, 5, 105, 1, '2025-01-14', 12000),
(6, 1, 102, 3, '2025-01-15', 1500),
(7, 2, 103, 2, '2025-01-16', 2400),
(8, 3, 101, 1, '2025-01-17', 75000);

select * from sales;

select * from products;

select sum(total_price) from sales;


select avg(total_price) from sales;

select min(total_price) as minimum_sales,
max(total_price) as maximum_sales
from sales;

select customers.customer_name,
sales.total_price
from sales
inner join customers
on sales.customer_id=customers.customer_id
order by sales.total_price desc
limit 5;

select customers.customer_name,
sum(sales.total_price) as total_purchase
from sales
inner join customers
on sales.customer_id=customers.customer_id
group by customers.customer_name
order by total_purchase desc
limit 1;
