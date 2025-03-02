# Week-4-day-7-assignment-a
answers.sql

Solution for 1NF (First Normal Form)

Steps to achieve 1NF:

Remove multiple values in a single column (Products).

Create a separate row for each product associated with an OrderID.


SQL Query to Transform into 1NF:

CREATE TABLE ProductDetail_1NF (
    OrderID INT,
    CustomerName VARCHAR(255),
    Product VARCHAR(255)
);

INSERT INTO ProductDetail_1NF (OrderID, CustomerName, Product)
VALUES 
(101, 'John Doe', 'Laptop'),
(101, 'John Doe', 'Mouse'),
(102, 'Jane Smith', 'Tablet'),
(102, 'Jane Smith', 'Keyboard'),
(102, 'Jane Smith', 'Mouse'),
(103, 'Emily Clark', 'Phone');


---

Solution for 2NF (Second Normal Form)

Steps to achieve 2NF:

Identify partial dependency: CustomerName depends only on OrderID, not on Product.

Normalize by splitting into two tables:

Orders table: Stores OrderID and CustomerName (removing dependency on Product).

OrderDetails table: Stores OrderID, Product, and Quantity.



SQL Query to Transform into 2NF:

-- Create Orders table
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerName VARCHAR(255)
);

-- Insert data into Orders table
INSERT INTO Orders (OrderID, CustomerName)
VALUES 
(101, 'John Doe'),
(102, 'Jane Smith'),
(103, 'Emily Clark');

-- Create OrderDetails table
CREATE TABLE OrderDetails_2NF (
    OrderID INT,
    Product VARCHAR(255),
    Quantity INT,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);

-- Insert data into OrderDetails table
INSERT INTO OrderDetails_2NF (OrderID, Product, Quantity)
VALUES 
(101, 'Laptop', 2),
(101, 'Mouse', 1),
(102, 'Tablet', 3),
(102, 'Keyboard', 1),
(102, 'Mouse', 2),
(103, 'Phone', 1);

