# Full Database Schema 

```sql
CREATE DATABASE IF NOT EXISTS mabiUpdateNew;
USE mabiUpdateNew;

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

CREATE TABLE master_user (
    intId INT PRIMARY KEY AUTO_INCREMENT,
    strEnrollId VARCHAR(255) NOT NULL,
    strSupervisorId VARCHAR(255) NOT NULL,
    strName VARCHAR(255) NOT NULL,
    strDesignation VARCHAR(255) NOT NULL,
    strEmail VARCHAR(255) NOT NULL,
    strContactNo VARCHAR(255) NOT NULL,
    strUserType VARCHAR(255) NOT NULL,
    isActive  TINYINT(1) NOT NULL,
    status  TINYINT(1) NOT NULL,
    strCreatedBy VARCHAR(255) NOT NULL,
    dteCreatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    strUpdatedBy VARCHAR(255) NULL,
    dteUpdatedAt DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
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
    updated_by INT NOT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

CREATE TABLE outlet_mapping (
    id INT PRIMARY KEY AUTO_INCREMENT,
    outlet_id INT NOT NULL,
    route_id INT NOT NULL,
    status TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

CREATE TABLE tour_plan (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    line_id INT NOT NULL,
    region_id INT NOT NULL,
    area_id INT NOT NULL,
    territory_id INT NOT NULL,
    point_id INT NOT NULL,
    route_id INT NOT NULL,
    tour_date DATETIME NOT NULL,
    tour_status ENUM('active', 'inactive') DEFAULT 'active',
    status  TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

CREATE TABLE requested_tour_plan (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    tour_plan_id INT NOT NULL,
    status ENUM('approved', 'declined') DEFAULT 'approved',
    approved_by VARCHAR(255) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

CREATE TABLE auditor_path (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    line_id INT NOT NULL,
    region_id INT NOT NULL,
    area_id INT NOT NULL,
    territory_id INT NOT NULL,
    point_id INT NOT NULL,
    route_id INT NOT NULL,
    status  TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

CREATE TABLE master_roles (
    id INT PRIMARY KEY AUTO_INCREMENT,
    role_name VARCHAR(255) NOT NULL,
    status  TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

CREATE TABLE role_permission (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    role_id INT NOT NULL,
    status  TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

CREATE TABLE master_questions (
    id INT PRIMARY KEY AUTO_INCREMENT,
    ques_type VARCHAR(255) NOT NULL,   
    ques_category VARCHAR(255) NOT NULL,   
    text_ques VARCHAR(255) NOT NULL,   
    ques_options VARCHAR(255) NOT NULL,      
    status TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NOT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

CREATE TABLE master_questions_answers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    ques_id INT NOT NULL,
    answer VARCHAR(255) NOT NULL,         
    status TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NOT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

CREATE TABLE master_menu (
    id INT PRIMARY KEY AUTO_INCREMENT,
    parent_id INT NOT NULL,
    submenu_name VARCHAR(255) NOT NULL,         
    url VARCHAR(255) NOT NULL,         
    status TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NOT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

ALTER TABLE master_product ADD CONSTRAINT fk_product_product_pack_size_type FOREIGN KEY (product_pack_size_id) REFERENCES master_product_pack_size_type (id);
ALTER TABLE outlet_mapping ADD CONSTRAINT fk_outlet_mapping_master_outlet FOREIGN KEY (outlet_id) REFERENCES master_outlet (id);
ALTER TABLE outlet_mapping ADD CONSTRAINT fk_outlet_mapping_route FOREIGN KEY (route_id) REFERENCES route (id);
ALTER TABLE master_product_ND_survey ADD CONSTRAINT fk_product_ND_survey_outlet FOREIGN KEY (outlet_id) REFERENCES master_outlet (id);
ALTER TABLE master_product_ND_survey ADD CONSTRAINT fk_product_ND_product FOREIGN KEY (product_id) REFERENCES master_product (id);
ALTER TABLE region ADD CONSTRAINT fk_region_line FOREIGN KEY (line_id) REFERENCES line (id);
ALTER TABLE area ADD CONSTRAINT fk_area_line FOREIGN KEY (line_id) REFERENCES line (id);
ALTER TABLE area ADD CONSTRAINT fk_area_region FOREIGN KEY (region_id) REFERENCES region (id);
ALTER TABLE territory ADD CONSTRAINT fk_territory_line FOREIGN KEY (line_id) REFERENCES line (id);
ALTER TABLE territory ADD CONSTRAINT fk_territory_region FOREIGN KEY (region_id) REFERENCES region (id);
ALTER TABLE territory ADD CONSTRAINT fk_territory_area FOREIGN KEY (area_id) REFERENCES area (id);
ALTER TABLE point ADD CONSTRAINT fk_point_line FOREIGN KEY (line_id) REFERENCES line (id);
ALTER TABLE point ADD CONSTRAINT fk_point_region FOREIGN KEY (region_id) REFERENCES region (id);
ALTER TABLE point ADD CONSTRAINT fk_point_area FOREIGN KEY (area_id) REFERENCES area (id);
ALTER TABLE point ADD CONSTRAINT fk_point_territory FOREIGN KEY (territory_id) REFERENCES territory (id);
ALTER TABLE section ADD CONSTRAINT fk_section_line FOREIGN KEY (line_id) REFERENCES line (id);
ALTER TABLE section ADD CONSTRAINT fk_section_region FOREIGN KEY (region_id) REFERENCES region (id);
ALTER TABLE section ADD CONSTRAINT fk_section_area FOREIGN KEY (area_id) REFERENCES area (id);
ALTER TABLE section ADD CONSTRAINT fk_section_territory FOREIGN KEY (territory_id) REFERENCES territory (id);
ALTER TABLE section ADD CONSTRAINT fk_section_point FOREIGN KEY (point_id) REFERENCES point (id);
ALTER TABLE route ADD CONSTRAINT fk_route_line FOREIGN KEY (line_id) REFERENCES line (id);
ALTER TABLE route ADD CONSTRAINT fk_route_region FOREIGN KEY (region_id) REFERENCES region (id);
ALTER TABLE route ADD CONSTRAINT fk_route_area FOREIGN KEY (area_id) REFERENCES area (id);
ALTER TABLE route ADD CONSTRAINT fk_route_territory FOREIGN KEY (territory_id) REFERENCES territory (id);
ALTER TABLE route ADD CONSTRAINT fk_route_point FOREIGN KEY (point_id) REFERENCES point (id);
ALTER TABLE route ADD CONSTRAINT fk_route_section FOREIGN KEY (section_id) REFERENCES section (id);
ALTER TABLE tour_plan ADD CONSTRAINT fk_tour_plan_user FOREIGN KEY (user_id) REFERENCES master_user (id);
ALTER TABLE tour_plan ADD CONSTRAINT fk_tour_plan_line FOREIGN KEY (line_id) REFERENCES line (id);
ALTER TABLE tour_plan ADD CONSTRAINT fk_tour_plan_region FOREIGN KEY (region_id) REFERENCES region (id);
ALTER TABLE tour_plan ADD CONSTRAINT fk_tour_plan_area FOREIGN KEY (area_id) REFERENCES area (id);
ALTER TABLE tour_plan ADD CONSTRAINT fk_tour_plan_territory FOREIGN KEY (territory_id) REFERENCES territory (id);
ALTER TABLE tour_plan ADD CONSTRAINT fk_tour_plan_point FOREIGN KEY (point_id) REFERENCES point (id);
ALTER TABLE tour_plan ADD CONSTRAINT fk_tour_plan_route FOREIGN KEY (route_id) REFERENCES route (id);
ALTER TABLE requested_tour_plan ADD CONSTRAINT fk_requested_tour_plan_user FOREIGN KEY (user_id) REFERENCES master_user (id);
ALTER TABLE requested_tour_plan ADD CONSTRAINT fk_requested_tour_plan_tour_plan FOREIGN KEY (tour_plan_id) REFERENCES tour_plan (id);
ALTER TABLE auditor_path ADD CONSTRAINT fk_auditor_path_user FOREIGN KEY (user_id) REFERENCES master_user (id);
ALTER TABLE auditor_path ADD CONSTRAINT fk_auditor_path_line FOREIGN KEY (line_id) REFERENCES line (id);
ALTER TABLE auditor_path ADD CONSTRAINT fk_auditor_path_region FOREIGN KEY (region_id) REFERENCES region (id);
ALTER TABLE auditor_path ADD CONSTRAINT fk_auditor_path_area FOREIGN KEY (area_id) REFERENCES area (id);
ALTER TABLE auditor_path ADD CONSTRAINT fk_auditor_path_territory FOREIGN KEY (territory_id) REFERENCES territory (id);
ALTER TABLE auditor_path ADD CONSTRAINT fk_auditor_path_point FOREIGN KEY (point_id) REFERENCES point (id);
ALTER TABLE auditor_path ADD CONSTRAINT fk_auditor_path_route FOREIGN KEY (route_id) REFERENCES route (id);
ALTER TABLE role_permission ADD CONSTRAINT fk_role_permission_user FOREIGN KEY (user_id) REFERENCES master_user (id);
ALTER TABLE role_permission ADD CONSTRAINT fk_role_permission_master_roles FOREIGN KEY (role_id) REFERENCES master_roles (id);
ALTER TABLE master_questions_answers ADD CONSTRAINT fk_master_questions_answers_master_questions FOREIGN KEY (ques_id) REFERENCES master_questions (id);
```


# Seperate Query based on Table

## 1. master_product_pack_size_type

### Table Creation 

```sql
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
```

## 2. master_product

### Table Creation 

```sql
CREATE TABLE master_product (
    id INT PRIMARY KEY AUTO_INCREMENT,
    product_name VARCHAR(255) NOT NULL,
    category VARCHAR(255) NOT NULL,
    SKU VARCHAR(255) NOT NULL,
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
```
### Table Constraints - Foreign Key

```sql
ALTER TABLE master_product ADD CONSTRAINT fk_product_product_pack_size_type FOREIGN KEY (product_pack_size_id) REFERENCES master_product_pack_size_type (id);
```

## 3. master_outlet

### Table Creation

```sql
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
```

## 4. master_product_ND_survey

### Table Creation

```sql
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

```

### Table Constraints - Foreign Key

```sql
ALTER TABLE master_product_ND_survey ADD CONSTRAINT fk_product_ND_survey_outlet FOREIGN KEY (outlet_id) REFERENCES master_outlet (id);
ALTER TABLE master_product_ND_survey ADD CONSTRAINT fk_product_ND_product FOREIGN KEY (product_id) REFERENCES master_product (id);
```

## 5. master_user

### Table Creation

```sql
CREATE TABLE master_user (
    intId INT PRIMARY KEY AUTO_INCREMENT,
    strEnrollId VARCHAR(255) NOT NULL,
    strSupervisorId VARCHAR(255) NOT NULL,
    strName VARCHAR(255) NOT NULL,
    strDesignation VARCHAR(255) NOT NULL,
    strEmail VARCHAR(255) NOT NULL,
    strContactNo VARCHAR(255) NOT NULL,
    strUserType VARCHAR(255) NOT NULL,
    isActive  TINYINT(1) NOT NULL,
    status  TINYINT(1) NOT NULL,
    strCreatedBy VARCHAR(255) NOT NULL,
    dteCreatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    strUpdatedBy VARCHAR(255) NULL,
    dteUpdatedAt DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

## 6. line

### Table Creation

```sql
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
```

## 7. region

### Table Creation

```sql
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
```
### Table Constraints - Foreign Key

```sql
ALTER TABLE region ADD CONSTRAINT fk_region_line FOREIGN KEY (line_id) REFERENCES line (id);
```

## 8. area

### Table Creation

```sql
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
```
### Table Constraints - Foreign Key

```sql
ALTER TABLE area ADD CONSTRAINT fk_area_line FOREIGN KEY (line_id) REFERENCES line (id);
ALTER TABLE area ADD CONSTRAINT fk_area_region FOREIGN KEY (region_id) REFERENCES region (id);
```

## 9. territory

### Table Creation

```sql
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
```

### Table Constraints - Foreign Key

```sql
ALTER TABLE territory ADD CONSTRAINT fk_territory_line FOREIGN KEY (line_id) REFERENCES line (id);
ALTER TABLE territory ADD CONSTRAINT fk_territory_region FOREIGN KEY (region_id) REFERENCES region (id);
ALTER TABLE territory ADD CONSTRAINT fk_territory_area FOREIGN KEY (area_id) REFERENCES area (id);
```

## 10. point

### Table Creation

```sql
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
```

### Table Constraints - Foreign Key

```sql
ALTER TABLE point ADD CONSTRAINT fk_point_line FOREIGN KEY (line_id) REFERENCES line (id);
ALTER TABLE point ADD CONSTRAINT fk_point_region FOREIGN KEY (region_id) REFERENCES region (id);
ALTER TABLE point ADD CONSTRAINT fk_point_area FOREIGN KEY (area_id) REFERENCES area (id);
ALTER TABLE point ADD CONSTRAINT fk_point_territory FOREIGN KEY (territory_id) REFERENCES territory (id);
```

## 11. section

### Table Creation

```sql
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
```

### Table Constraints - Foreign Key

```sql
ALTER TABLE section ADD CONSTRAINT fk_section_line FOREIGN KEY (line_id) REFERENCES line (id);
ALTER TABLE section ADD CONSTRAINT fk_section_region FOREIGN KEY (region_id) REFERENCES region (id);
ALTER TABLE section ADD CONSTRAINT fk_section_area FOREIGN KEY (area_id) REFERENCES area (id);
ALTER TABLE section ADD CONSTRAINT fk_section_territory FOREIGN KEY (territory_id) REFERENCES territory (id);
ALTER TABLE section ADD CONSTRAINT fk_section_point FOREIGN KEY (point_id) REFERENCES point (id);
```

## 12. route

### Table Creation

```sql
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
    updated_by INT NOT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

### Table Constraints - Foreign Key

```sql
ALTER TABLE route ADD CONSTRAINT fk_route_line FOREIGN KEY (line_id) REFERENCES line (id);
ALTER TABLE route ADD CONSTRAINT fk_route_region FOREIGN KEY (region_id) REFERENCES region (id);
ALTER TABLE route ADD CONSTRAINT fk_route_area FOREIGN KEY (area_id) REFERENCES area (id);
ALTER TABLE route ADD CONSTRAINT fk_route_territory FOREIGN KEY (territory_id) REFERENCES territory (id);
ALTER TABLE route ADD CONSTRAINT fk_route_point FOREIGN KEY (point_id) REFERENCES point (id);
ALTER TABLE route ADD CONSTRAINT fk_route_section FOREIGN KEY (section_id) REFERENCES section (id);
```

## 13. outlet_mapping

### Table Creation

```sql
CREATE TABLE outlet_mapping (
    id INT PRIMARY KEY AUTO_INCREMENT,
    outlet_id INT NOT NULL,
    route_id INT NOT NULL,
    status TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

### Table Constraints - Foreign Key

```sql
ALTER TABLE outlet_mapping ADD CONSTRAINT fk_outlet_mapping_master_outlet FOREIGN KEY (outlet_id) REFERENCES master_outlet (id);
ALTER TABLE outlet_mapping ADD CONSTRAINT fk_outlet_mapping_route FOREIGN KEY (route_id) REFERENCES route (id);
```

## 14. tour_plan

### Table Creation

```sql
CREATE TABLE tour_plan (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    line_id INT NOT NULL,
    region_id INT NOT NULL,
    area_id INT NOT NULL,
    territory_id INT NOT NULL,
    point_id INT NOT NULL,
    route_id INT NOT NULL,
    tour_date DATETIME NOT NULL,
    tour_status ENUM('active', 'inactive') DEFAULT 'active',
    status  TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

### Table Constraints - Foreign Key

```sql
ALTER TABLE tour_plan ADD CONSTRAINT fk_tour_plan_user FOREIGN KEY (user_id) REFERENCES master_user (id);
ALTER TABLE tour_plan ADD CONSTRAINT fk_tour_plan_line FOREIGN KEY (line_id) REFERENCES line (id);
ALTER TABLE tour_plan ADD CONSTRAINT fk_tour_plan_region FOREIGN KEY (region_id) REFERENCES region (id);
ALTER TABLE tour_plan ADD CONSTRAINT fk_tour_plan_area FOREIGN KEY (area_id) REFERENCES area (id);
ALTER TABLE tour_plan ADD CONSTRAINT fk_tour_plan_territory FOREIGN KEY (territory_id) REFERENCES territory (id);
ALTER TABLE tour_plan ADD CONSTRAINT fk_tour_plan_point FOREIGN KEY (point_id) REFERENCES point (id);
ALTER TABLE tour_plan ADD CONSTRAINT fk_tour_plan_route FOREIGN KEY (route_id) REFERENCES route (id);
```

## 15. requested_tour_plan

### Table Creation

```sql
CREATE TABLE requested_tour_plan (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    tour_plan_id INT NOT NULL,
    status ENUM('approved', 'declined') DEFAULT 'approved',
    approved_by VARCHAR(255) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

### Table Constraints - Foreign Key

```sql
ALTER TABLE requested_tour_plan ADD CONSTRAINT fk_requested_tour_plan_user FOREIGN KEY (user_id) REFERENCES master_user (id);
ALTER TABLE requested_tour_plan ADD CONSTRAINT fk_requested_tour_plan_tour_plan FOREIGN KEY (tour_plan_id) REFERENCES tour_plan (id);
```

## 16. auditor_path

### Table Creation

```sql
CREATE TABLE auditor_path (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    line_id INT NOT NULL,
    region_id INT NOT NULL,
    area_id INT NOT NULL,
    territory_id INT NOT NULL,
    point_id INT NOT NULL,
    route_id INT NOT NULL,
    status  TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

### Table Constraints - Foreign Key

```sql
ALTER TABLE auditor_path ADD CONSTRAINT fk_auditor_path_user FOREIGN KEY (user_id) REFERENCES master_user (id);
ALTER TABLE auditor_path ADD CONSTRAINT fk_auditor_path_line FOREIGN KEY (line_id) REFERENCES line (id);
ALTER TABLE auditor_path ADD CONSTRAINT fk_auditor_path_region FOREIGN KEY (region_id) REFERENCES region (id);
ALTER TABLE auditor_path ADD CONSTRAINT fk_auditor_path_area FOREIGN KEY (area_id) REFERENCES area (id);
ALTER TABLE auditor_path ADD CONSTRAINT fk_auditor_path_territory FOREIGN KEY (territory_id) REFERENCES territory (id);
ALTER TABLE auditor_path ADD CONSTRAINT fk_auditor_path_point FOREIGN KEY (point_id) REFERENCES point (id);
ALTER TABLE auditor_path ADD CONSTRAINT fk_auditor_path_route FOREIGN KEY (route_id) REFERENCES route (id);
```

## 17. master_roles

### Table Creation

```sql
CREATE TABLE master_roles (
    id INT PRIMARY KEY AUTO_INCREMENT,
    role_name VARCHAR(255) NOT NULL,
    status  TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

## 18. role_permission

### Table Creation

```sql
CREATE TABLE role_permission (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    role_id INT NOT NULL,
    status  TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

### Table Constraints - Foreign Key

```sql
ALTER TABLE role_permission ADD CONSTRAINT fk_role_permission_user FOREIGN KEY (user_id) REFERENCES master_user (id);
ALTER TABLE role_permission ADD CONSTRAINT fk_role_permission_master_roles FOREIGN KEY (role_id) REFERENCES master_roles (id);
```

## 19. master_questions

### Table Creation

```sql
CREATE TABLE master_questions (
    id INT PRIMARY KEY AUTO_INCREMENT,
    ques_type VARCHAR(255) NOT NULL,   
    ques_category VARCHAR(255) NOT NULL,   
    text_ques VARCHAR(255) NOT NULL,   
    ques_options VARCHAR(255) NOT NULL,      
    status TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NOT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

## 20. master_questions_answers

### Table Creation

```sql
CREATE TABLE master_questions_answers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    ques_id INT NOT NULL,
    answer VARCHAR(255) NOT NULL,         
    status TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NOT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

### Table Constraints - Foreign Key

```sql
ALTER TABLE master_questions_answers ADD CONSTRAINT fk_master_questions_answers_master_questions FOREIGN KEY (ques_id) REFERENCES master_questions (id);
```

## 21. master_menu

### Table Creation

```sql
CREATE TABLE master_menu (
    id INT PRIMARY KEY AUTO_INCREMENT,
    parent_id INT NOT NULL,
    submenu_name VARCHAR(255) NOT NULL,         
    url VARCHAR(255) NOT NULL,         
    status TINYINT(1) NOT NULL,
    created_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by INT NOT NULL,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```