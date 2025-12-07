# 🍴 Food Treasure – Online Food Ordering System

Food Treasure is a full-stack **Java-based online food ordering application** built using **Servlets, JSP, JDBC, DAO pattern, Models, and MySQL**, following the **MVC architecture**.  
Users can browse restaurants, explore menus, add items to cart, place orders, and track them.  
It includes dashboards for **Customers, Restaurant Admins, Super Admins, and Delivery Partners**.

---

## 🚀 Tech Stack

### **Frontend**
- JSP  
- HTML  
- CSS  

### **Backend**
- Java  
- Servlets (Jakarta)  
- Models (POJOs)  
- DAO Implementation  
- JDBC  

### **Database**
- MySQL  

### **Architecture**
- MVC Architecture  
- HttpSession for user + cart handling  

---

## 📌 Key Features

### 👤 User Management
- Login & Registration  
- Secure authentication  
- Multiple user roles:
  - Customer  
  - Restaurant Admin  
  - Super Admin  
  - Delivery Partner  

### 🍽️ Restaurant & Menu Management
- Browse restaurants  
- View menu items  
- Restaurant Admin features:
  - Add/Delete Restaurants  
  - Add/Delete Menu Items  

### 🛒 Cart System
- Add items to cart  
- Update/Delete items  
- Session-based cart  
- Prevents adding from multiple restaurants  

### 📦 Order System
- Place orders with payment mode  
- COD / UPI / Card  
- Order history  
- Automatic order & order item creation  

---

## 🗄️ Database Schema (MySQL)
-- Create Database CREATE DATABASE IF NOT EXISTS foodtreasure; USE foodtreasure;

-- USERS TABLE CREATE TABLE Users ( user_id INT PRIMARY KEY AUTO_INCREMENT, name VARCHAR(100) NOT NULL, username VARCHAR(50) UNIQUE NOT NULL, password VARCHAR(255) NOT NULL, email VARCHAR(100) UNIQUE NOT NULL, phone_number VARCHAR(15), address VARCHAR(255), role VARCHAR(50) NOT NULL, -- admin, customer, restaurant admin, delivery partner created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP, last_login_date TIMESTAMP NULL );

-- RESTAURANTS TABLE CREATE TABLE Restaurants ( restaurant_id INT PRIMARY KEY AUTO_INCREMENT, name VARCHAR(100) NOT NULL, address VARCHAR(255) NOT NULL, phone_number VARCHAR(15), cuisine_type VARCHAR(50), delivery_time VARCHAR(50), admin_user_id INT, rating FLOAT DEFAULT 0.0, is_active BOOLEAN DEFAULT TRUE, image_path VARCHAR(255), FOREIGN KEY (admin_user_id) REFERENCES Users(user_id) );

-- MENU TABLE CREATE TABLE Menu ( menu_id INT PRIMARY KEY AUTO_INCREMENT, restaurant_id INT NOT NULL, item_name VARCHAR(100) NOT NULL, description TEXT, price DECIMAL(10,2) NOT NULL, is_available BOOLEAN DEFAULT TRUE, rating FLOAT DEFAULT 0.0, image_path VARCHAR(255), FOREIGN KEY (restaurant_id) REFERENCES Restaurants(restaurant_id) );

-- CART ITEMS TABLE CREATE TABLE CartItems ( item_id INT PRIMARY KEY AUTO_INCREMENT, menu_id INT NOT NULL, restaurant_id INT NOT NULL, user_id INT NOT NULL, name VARCHAR(100) NOT NULL, quantity INT NOT NULL CHECK (quantity > 0), description TEXT, image_path VARCHAR(255), price DECIMAL(10,2) NOT NULL, FOREIGN KEY (menu_id) REFERENCES Menu(menu_id) ON DELETE CASCADE ON UPDATE CASCADE, FOREIGN KEY (restaurant_id) REFERENCES Restaurants(restaurant_id) ON DELETE CASCADE ON UPDATE CASCADE, FOREIGN KEY (user_id) REFERENCES Users(user_id) );

-- ORDERS TABLE CREATE TABLE Orders ( order_id INT PRIMARY KEY AUTO_INCREMENT, restaurant_id INT NOT NULL, user_id INT NOT NULL, order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP, total_amount DECIMAL(10,2) NOT NULL, status VARCHAR(50) DEFAULT 'PENDING', payment_mode VARCHAR(20), address VARCHAR(255), FOREIGN KEY (restaurant_id) REFERENCES Restaurants(restaurant_id) ON DELETE CASCADE ON UPDATE CASCADE, FOREIGN KEY (user_id) REFERENCES Users(user_id) );

-- ORDER ITEMS TABLE CREATE TABLE OrderItems ( order_item_id INT PRIMARY KEY AUTO_INCREMENT, order_id INT NOT NULL, menu_id INT NOT NULL, quantity INT NOT NULL CHECK (quantity > 0), price DECIMAL(10,2) NOT NULL, total_amount DECIMAL(10,2) NOT NULL, FOREIGN KEY (order_id) REFERENCES Orders(order_id) ON DELETE CASCADE ON UPDATE CASCADE, FOREIGN KEY (menu_id) REFERENCES Menu(menu_id) );

---

▶️ How to Run the Project

1. Clone the Repository
 - git clone https://github.com/yourusername/food-treasure.git
 - cd food-treasure

2. Setup the Database
   
 - Run all SQL tables from the schema above in MySQL.

3. Configure Database

 - Update DB credentials in:

 - com.tap.util.DBConnection

4. Deploy the Application

 - Deploy on Apache Tomcat

 - Or configure via IDE (Eclipse/IntelliJ)

5. Start Server & Access
 - http://localhost:8080/food-treasure

---

📌 Future Enhancements

 - Online payment integration

 - Email/SMS notifications

 - Real-time delivery tracking

 - Restaurant analytics dashboard

