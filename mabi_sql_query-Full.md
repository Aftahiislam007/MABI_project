# Full Database Schema 

```sql
CREATE DATABASE mabi;
USE mabi;

CREATE TABLE master_product (
    id INT PRIMARY KEY AUTO_INCREMENT,
    product_name VARCHAR(255) NOT NULL,
    category VARCHAR(255) NOT NULL,
    SKU VARCHAR(255) NOT NULL,
    FOREIGN KEY (product_pack_size_id) REFERENCES master_product_pack_size_type(id),
    product_company VARCHAR(255) NOT NULL,
    company_type ENUM('own', 'others') DEFAULT 'own',
    dp_price DOUBLE NOT NULL,
    tp_price DOUBLE NOT NULL,
    MRP DOUBLE NOT NULL,
    brand VARCHAR(255) NOT NULL,
    brand_id INT NOT NULL,
    image_url VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```


# Seperate Query based on Table

## 1. master_product_pack_size_type

### Table Creation 

```sql
CREATE TABLE master_product (
    id INT PRIMARY KEY AUTO_INCREMENT,
    product_name VARCHAR(255) NOT NULL,
    category VARCHAR(255) NOT NULL,
    SKU VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

## 2. master_product_pack_size_type

### Table Creation 

```sql
CREATE TABLE master_product_pack_size_type (
 id int(11) PRIMARY KEY AUTO_INCREMENT,
    pack_size varchar(50) NULL,
    pack_type varchar(50) NULL,
    status boolean,
    createdAt DateTime,
    updatedAt DateTime,
    createdBy varchar(50),
    updatedBy varchar(50)
);
```

# 3. master_product

### Table Constraints - Foreign Key

```sql
ALTER TABLE master_product
ADD CONSTRAINT FK_Product_pack_size_type
FOREIGN KEY (product_pack_size_id) REFERENCES master_product_pack_size_type(id);
```

# 4. master_product_ND_survey

### Table Creation

```sql
CREATE TABLE master_product_ND_survey ( 
    id int(11) PRIMARY KEY AUTO_INCREMENT, 
    outlet_code varchar(50) NULL, 
    outlet_id int(11) NULL, 
    product_id int(11) NULL, 
    product_isPresent boolean NULL, 
    product_isDisplayed boolean NULL, 
    status boolean NULL, 
    createdAt DateTime NULL, 
    updatedAt DateTime NULL, 
    createdBy varchar(50) NULL, 
    updatedBy varchar(50) NULL 
);
```

# 4. master_outlet

### Table Creation

```sql

```
