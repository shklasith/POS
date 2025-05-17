# POS System - Java Web Application

![POS System Screenshot](https://github.com/user-attachments/assets/b31f4abb-a970-451e-9959-11728143650c)

A complete Point of Sale system with inventory management, sales processing, and reporting capabilities.

## 🗄 Database Schema

```sql
CREATE DATABASE IF NOT EXISTS pos_system 
  CHARACTER SET utf8mb4 
  COLLATE utf8mb4_unicode_ci;

USE pos_system;

-- Products table
CREATE TABLE products (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    price DECIMAL(10,2) NOT NULL CHECK (price > 0),
    quantity INT NOT NULL DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    INDEX idx_name (name)
) ENGINE=InnoDB;

-- Sales transactions
CREATE TABLE sales (
    id INT AUTO_INCREMENT PRIMARY KEY,
    sale_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    total_amount DECIMAL(10,2) NOT NULL,
    INDEX idx_sale_date (sale_date)
) ENGINE=InnoDB;

-- Individual sale items
CREATE TABLE sale_items (
    id INT AUTO_INCREMENT PRIMARY KEY,
    sale_id INT NOT NULL,
    product_id INT NOT NULL,
    quantity INT NOT NULL CHECK (quantity > 0),
    subtotal DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (sale_id) REFERENCES sales(id) ON DELETE CASCADE,
    FOREIGN KEY (product_id) REFERENCES products(id),
    INDEX idx_sale (sale_id)
) ENGINE=InnoDB;

-- User accounts
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    INDEX idx_username (username)
) ENGINE=InnoDB;

## 🏗 Project Structure

```text
pos-system/
├── nb-configuration.xml
├── pom.xml
├── src/
│   └── main/
│       ├── java/
│       │   ├── com/mycompany/possystem/
│       │   │   ├── dao/
│       │   │   │   ├── ProductDAO.java       # Product data access
│       │   │   │   └── SalesDAO.java        # Sales data access
│       │   │   ├── model/
│       │   │   │   ├── Product.java         # Product entity
│       │   │   │   ├── SaleItem.java        # Sale item entity
│       │   │   │   ├── Sale.java            # Sale entity
│       │   │   │   └── User.java            # User entity
│       │   │   ├── service/
│       │   │   │   ├── ProductService.java  # Product business logic
│       │   │   │   └── SalesService.java   # Sales business logic
│       │   │   ├── servlet/
│       │   │   │   ├── ProductServlet.java  # Product controller
│       │   │   │   ├── ReportServlet.java   # Report controller
│       │   │   │   └── SalesServlet.java   # Sales controller
│       │   │   └── util/
│       │   │       ├── DateUtil.java        # Date utilities
│       │   │       └── NumberFormatter.java # Formatting utilities
│       │   └── DBUtil.java                 # Database utilities
│       ├── resources/
│       │   └── META-INF/
│       │       └── persistence.xml          # JPA configuration
│       └── webapp/
│           ├── add_sale.jsp                # Add sale page
│           ├── index.jsp                   # Home page
│           ├── META-INF/
│           │   └── context.xml             # Data source config
│           ├── product_form.jsp            # Product form
│           ├── products.jsp                # Products listing
│           ├── receipt.jsp                 # Receipt template
│           ├── report.jsp                  # Reports page
│           ├── style.css                   # Main stylesheet
│           └── WEB-INF/
│               ├── beans.xml               # CDI configuration
│               └── web.xml                 # Deployment descriptor
└── target/                                 # Build output
    ├── classes/                           # Compiled classes
    └── POSSystem.war                      # Deployable WAR

