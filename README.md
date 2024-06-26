# module-end-project-mysql
library management system 
REATE DATABASE library;
USE library;

CREATE TABLE Branch(
Branch_no INT PRIMARY KEY,
Manager_Id int UNIQUE KEY,
Branch_address VARCHAR(90),
Contact_no BIGINT);

INSERT INTO Branch(Branch_no,Manager_Id,Branch_address,Contact_no) VALUES
(1, 101, '123 Main St', 9876543210),
(2, 102, '456 Maple Ave', 9846543210),
(3, 103, '789 Oak Dr', 4567891234),
(4, 104, '101 Pine Rd', 3216549870),
(5, 105, '202 Birch Ln',6543210987);


CREATE TABLE Employee(
Emp_id INT PRIMARY KEY,
Emp_name VARCHAR(50),
Position VARCHAR(20),
Salary INT,
Branch_no INT,
FOREIGN KEY(Branch_no)REFERENCES Branch(Branch_no));

INSERT INTO Employee(Emp_id,Emp_name,Position,Salary,Branch_no) VALUES
(201, 'Alice Smith', 'Librarian', 55000.00, 1),
(202, 'Bob Johnson', 'Assistant', 45000.00, 2),
(203, 'Carol White', 'Manager', 65000.00, 1),
(204, 'David Brown', 'Technician', 40000.00, 3),
(205, 'Eve Davis', 'Assistant', 48000.00, 4),
(206, 'Frank Wilson', 'Librarian', 53000.00, 5),
(207, 'Grace Lee', 'Technician', 42000.00, 1),
(208, 'Henry Clark', 'Librarian', 60000.00, 2),
(209, 'Ivy Young', 'Assistant', 47000.00, 3),
(210, 'Jack Harris', 'Technician', 41000.00, 4);


CREATE TABLE Customer(
Customer_Id INT PRIMARY KEY,
Customer_name VARCHAR(30),
Customer_address VARCHAR(30),
Reg_date DATE);

INSERT INTO Customer(Customer_Id,Customer_name,Customer_address,Reg_date) VALUES
(301, 'John Doe', '789 Willow St', '2020-05-20'),
(302, 'Jane Roe', '123 Elm St', '2021-07-15'),
(303, 'Jim Beam', '456 Spruce Ave', '2022-01-10'),
(304, 'Jill Hill', '789 Pine Dr', '2022-12-12'),
(305, 'Jake Snake', '101 Cedar Rd', '2021-03-05'),
(306, 'Julia Louis', '202 Walnut St', '2023-04-18'),
(307, 'Jason Fox', '303 Chestnut Ln', '2019-11-25'),
(308, 'Janet White', '404 Fir St', '2023-02-14'),
(309, 'Jerry Black', '505 Maple Ave', '2020-08-08'),
(310, 'Joy Brown', '606 Oak Dr', '2021-06-21');


CREATE TABLE Books(
ISBN INT PRIMARY KEY,
Book_title varchar(20),
Category VARCHAR(20),
Rental_Price INT,
Status ENUM ('yes','no'),
Author VARCHAR(100),
Publisher VARCHAR(20));

INSERT INTO Books(ISBN,Book_title,Category,Rental_Price,Status,Author,Publisher) VALUES
(978-3-16-148410-0, 'Book A', 'History', 15.00, 'yes', 'Author A', 'Publisher A'),
(978-1-4028-9462-6, 'Book B', 'Science', 20.00, 'yes', 'Author B', 'Publisher B'),
(978-0-545-01022-1, 'Book C', 'Math', 25.00, 'no', 'Author C', 'Publisher C'),
(978-0-7432-7356-0, 'Book D', 'History', 10.00, 'yes', 'Author D', 'Publisher D'),
(978-1-86197-876-9, 'Book E', 'Literature', 18.00, 'no', 'Author E', 'Publisher E'),
(978-0-452-28423-4, 'Book F', 'Science', 22.00, 'yes', 'Author F', 'Publisher F'),
(978-0-14-044913-6, 'Book G', 'History', 30.00, 'yes', 'Author G', 'Publisher G'),
(978-1-56619-909-4, 'Book H', 'Literature', 16.00, 'yes', 'Author H', 'Publisher H'),
(978-0-06-112008-4, 'Book I', 'Science', 12.00, 'yes', 'Author I', 'Publisher I'),
(978-0-7432-7356-1, 'Book J', 'Math', 14.00, 'no', 'Author J', 'Publisher J');

CREATE TABLE IssueStatus(
Issue_id int PRIMARY KEY,
Issued_cust INT,
Issued_book_name VARCHAR(20),
Issue_date DATE,
Isbn_book INT,
FOREIGN KEY(Isbn_book)REFERENCES Books(ISBN),
FOREIGN KEY (Issued_cust) REFERENCES Customer(Customer_Id)
);

INSERT INTO IssueStatus(Issue_id,Issued_cust,Issued_book_name,Issue_date,Isbn_book) VALUES
(401, 301, 'Book A', '2023-06-01', 978-3-16-148410-0),
(402, 302, 'Book C', '2023-06-05', 978-0-545-01022-1),
(403, 303, 'Book E', '2023-06-10', 978-1-86197-876-9),
(404, 304, 'Book H', '2023-06-15', 978-1-56619-909-4),
(405, 305, 'Book J', '2023-06-20', 978-0-7432-7356-1),
(406, 306, 'Book B', '2023-06-25', 978-1-4028-9462-6),
(407, 307, 'Book D', '2023-06-28', 978-0-7432-7356-0),
(408, 308, 'Book F', '2023-06-30', 978-0-452-28423-4),
(409, 309, 'Book G', '2023-06-02', 978-0-14-044913-6),
(410, 310, 'Book I', '2023-06-03', 978-0-06-112008-4);


 CREATE TABLE ReturnStatus (
    Return_Id INT PRIMARY KEY,
    Return_cust INT,
    Return_book_name VARCHAR(255),
    Return_date DATE,
