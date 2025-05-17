# POS System - Java Web Application

![POS System Screenshot](screen![WhatsApp Image 2025-05-17 at 23 18 41](https://github.com/user-attachments/assets/b31f4abb-a970-451e-9959-11728143650c)
shot.png) 

A Point of Sale (POS) system built with Java EE/Jakarta EE, MySQL, and Maven.

## Features
- Product inventory management
- Sales processing
- Sales history tracking
- MySQL database integration
- RESTful API endpoints (Optional)
- User authentication (Optional)

## Technologies Used
- **Backend**: Java EE/Jakarta EE 8+
- **Frontend**: JSP, JSTL, HTML5, CSS3, JavaScript
- **Database**: MySQL
- **Build Tool**: Maven
- **Application Server**: Tomcat 9+/Payara/Jetty

## Database Schema
The system uses the following MySQL database structure:

```sql
CREATE DATABASE IF NOT EXISTS pos_system;
USE pos_system;

-- Products table
CREATE TABLE products (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    price DECIMAL(10,2) NOT NULL,
    quantity INT NOT NULL
);

-- Sales table
CREATE TABLE sales (
    id INT AUTO_INCREMENT PRIMARY KEY,
    sale_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    total_amount DECIMAL(10,2)
);

-- Sale Items table
CREATE TABLE sale_items (
    id INT AUTO_INCREMENT PRIMARY KEY,
    sale_id INT,
    product_id INT,
    quantity INT,
    subtotal DECIMAL(10,2),
    FOREIGN KEY (sale_id) REFERENCES sales(id),
    FOREIGN KEY (product_id) REFERENCES products(id)
);

-- Users table (optional)
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50),
    password VARCHAR(255)
);
