# Full Database Schema 

```sql
CREATE DATABASE mabi;
USE mabi;

CREATE TABLE master_product_pack_size_type (
    id INT PRIMARY KEY AUTO_INCREMENT,
    pack_size VARCHAR(255) NOT NULL,
    pack_type VARCHAR(255) NOT NULL,
    status  TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

CREATE TABLE master_product (
    id INT PRIMARY KEY AUTO_INCREMENT,
    product_name VARCHAR(255) NOT NULL,
    category VARCHAR(255) NOT NULL,
    SKU VARCHAR(255) NOT NULL,
    -- FOREIGN KEY (product_pack_size_id) REFERENCES master_product_pack_size_type(id),
    product_pack_size_id INT NOT NULL,
    product_company VARCHAR(255) NOT NULL,
    company_type ENUM('own', 'others') DEFAULT 'own',
    dp_price DOUBLE NOT NULL,
    tp_price DOUBLE NOT NULL,
    MRP DOUBLE NOT NULL,
    brand VARCHAR(255) NOT NULL,
    brand_id INT NOT NULL,
    image_url VARCHAR(255) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

ALTER TABLE master_product ADD CONSTRAINT fk_product_product_pack_size_type FOREIGN KEY (product_pack_size_id) REFERENCES master_product_pack_size_type (id);

CREATE TABLE master_outlet (
    id INT PRIMARY KEY AUTO_INCREMENT,
    owner_name VARCHAR(255) NOT NULL,
    contact_no VARCHAR(255) NOT NULL,
    address VARCHAR(255) NOT NULL,
    latitude VARCHAR(255) NOT NULL,
    longitude VARCHAR(255) NOT NULL,
    outlet_code VARCHAR(255) NOT NULL,
    cooler_outlet TINYINT(1) NOT NULL,
    outlet_category VARCHAR(255) NOT NULL,
    image_url VARCHAR(255) NOT NULL,
    status  TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

CREATE TABLE master_product_ND_survey (
    id INT PRIMARY KEY AUTO_INCREMENT,
    outlet_code VARCHAR(255) NOT NULL,
    outlet_id INT NOT NULL,
    product_id INT NOT NULL,
    product_isPresent TINYINT(1) NOT NULL,
    product_isDisplayed TINYINT(1) NOT NULL,
    status  TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

ALTER TABLE master_product_ND_survey ADD CONSTRAINT fk_product_ND_survey_outlet FOREIGN KEY (outlet_id) REFERENCES master_outlet (id);
ALTER TABLE master_product_ND_survey ADD CONSTRAINT fk_product_ND_product FOREIGN KEY (product_id) REFERENCES master_product (id);

CREATE TABLE master_user (
    id INT PRIMARY KEY AUTO_INCREMENT,
    enroll_id VARCHAR(255) NOT NULL,
    supervisor_id VARCHAR(255) NOT NULL,
    name VARCHAR(255) NOT NULL,
    designation VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL,
    contact_no VARCHAR(255) NOT NULL,
    user_type VARCHAR(255) NOT NULL,
    status  TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

CREATE TABLE line (
    id INT PRIMARY KEY AUTO_INCREMENT,
    display_name VARCHAR(255) NOT NULL,
    slug VARCHAR(255) NOT NULL,
    status  TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

CREATE TABLE region (
    id INT PRIMARY KEY AUTO_INCREMENT,
    display_name VARCHAR(255) NOT NULL,
    slug VARCHAR(255) NOT NULL,
    line_id INT NOT NULL,
    status  TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

ALTER TABLE region ADD CONSTRAINT fk_region_line FOREIGN KEY (line_id) REFERENCES line (id);

CREATE TABLE area (
    id INT PRIMARY KEY AUTO_INCREMENT,
    display_name VARCHAR(255) NOT NULL,
    slug VARCHAR(255) NOT NULL,
    line_id INT NOT NULL,
    region_id INT NOT NULL,
    status  TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

ALTER TABLE area ADD CONSTRAINT fk_area_line FOREIGN KEY (line_id) REFERENCES line (id);
ALTER TABLE area ADD CONSTRAINT fk_area_region FOREIGN KEY (region_id) REFERENCES region (id);

CREATE TABLE territory (
    id INT PRIMARY KEY AUTO_INCREMENT,
    display_name VARCHAR(255) NOT NULL,
    slug VARCHAR(255) NOT NULL,
    line_id INT NOT NULL,
    region_id INT NOT NULL,
    area_id INT NOT NULL,
    status  TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

ALTER TABLE territory ADD CONSTRAINT fk_territory_line FOREIGN KEY (line_id) REFERENCES line (id);
ALTER TABLE territory ADD CONSTRAINT fk_territory_region FOREIGN KEY (region_id) REFERENCES region (id);
ALTER TABLE territory ADD CONSTRAINT fk_territory_area FOREIGN KEY (area_id) REFERENCES area (id);

CREATE TABLE point (
    id INT PRIMARY KEY AUTO_INCREMENT,
    display_name VARCHAR(255) NOT NULL,
    slug VARCHAR(255) NOT NULL,
    line_id INT NOT NULL,
    region_id INT NOT NULL,
    area_id INT NOT NULL,
    territory_id INT NOT NULL,
    status  TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

ALTER TABLE point ADD CONSTRAINT fk_point_line FOREIGN KEY (line_id) REFERENCES line (id);
ALTER TABLE point ADD CONSTRAINT fk_point_region FOREIGN KEY (region_id) REFERENCES region (id);
ALTER TABLE point ADD CONSTRAINT fk_point_area FOREIGN KEY (area_id) REFERENCES area (id);
ALTER TABLE point ADD CONSTRAINT fk_point_territory FOREIGN KEY (territory_id) REFERENCES territory (id);

CREATE TABLE section (
    id INT PRIMARY KEY AUTO_INCREMENT,
    display_name VARCHAR(255) NOT NULL,
    slug VARCHAR(255) NOT NULL,
    line_id INT NOT NULL,
    region_id INT NOT NULL,
    area_id INT NOT NULL,
    territory_id INT NOT NULL,
    point_id INT NOT NULL,
    status  TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

ALTER TABLE section ADD CONSTRAINT fk_section_line FOREIGN KEY (line_id) REFERENCES line (id);
ALTER TABLE section ADD CONSTRAINT fk_section_region FOREIGN KEY (region_id) REFERENCES region (id);
ALTER TABLE section ADD CONSTRAINT fk_section_area FOREIGN KEY (area_id) REFERENCES area (id);
ALTER TABLE section ADD CONSTRAINT fk_section_territory FOREIGN KEY (territory_id) REFERENCES territory (id);
ALTER TABLE section ADD CONSTRAINT fk_section_point FOREIGN KEY (point_id) REFERENCES point (id);

CREATE TABLE route (
    id INT PRIMARY KEY AUTO_INCREMENT,
    display_name VARCHAR(255) NOT NULL,
    slug VARCHAR(255) NOT NULL,
    line_id INT NOT NULL,
    region_id INT NOT NULL,
    area_id INT NOT NULL,
    territory_id INT NOT NULL,
    point_id INT NOT NULL,
    section_id INT NOT NULL,
    status  TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

ALTER TABLE route ADD CONSTRAINT fk_route_line FOREIGN KEY (line_id) REFERENCES line (id);
ALTER TABLE route ADD CONSTRAINT fk_route_region FOREIGN KEY (region_id) REFERENCES region (id);
ALTER TABLE route ADD CONSTRAINT fk_route_area FOREIGN KEY (area_id) REFERENCES area (id);
ALTER TABLE route ADD CONSTRAINT fk_route_territory FOREIGN KEY (territory_id) REFERENCES territory (id);
ALTER TABLE route ADD CONSTRAINT fk_route_point FOREIGN KEY (point_id) REFERENCES point (id);
ALTER TABLE route ADD CONSTRAINT fk_route_section FOREIGN KEY (section_id) REFERENCES section (id);



```


# Seperate Query based on Table

## 1. master_product

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
    id INT PRIMARY KEY AUTO_INCREMENT,
    pack_size VARCHAR(255) NOT NULL,
    pack_type VARCHAR(255) NOT NULL,
    status  TINYINT(1),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
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
