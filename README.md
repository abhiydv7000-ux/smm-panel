smm-panel/
│── index.php
│── login.php
│── register.php
│── dashboard.php
│── order.php
│── payment.php
│── admin/
│   ├── admin.php
│   ├── services.php
│   ├── orders.php
│── config.php
│── database.sql
│── style.css
CREATE DATABASE smm_panel;

USE smm_panel;

CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100),
  email VARCHAR(100),
  password VARCHAR(255),
  balance DECIMAL(10,2) DEFAULT 0,
  role ENUM('user','admin') DEFAULT 'user'
);

CREATE TABLE services (
  id INT AUTO_INCREMENT PRIMARY KEY,
  service_name VARCHAR(255),
  price DECIMAL(10,2),
  description TEXT
);

CREATE TABLE orders (
  id INT AUTO_INCREMENT PRIMARY KEY,
  user_id INT,
  service_id INT,
  link VARCHAR(255),
  quantity INT,
  status VARCHAR(50) DEFAULT 'Pending'
);

CREATE TABLE payments (
  id INT AUTO_INCREMENT PRIMARY KEY,
  user_id INT,
  upi_txn VARCHAR(100),
  screenshot VARCHAR(255),
  status VARCHAR(50) DEFAULT 'Pending'
);
<?php
$conn = mysqli_connect("localhost","root","","smm_panel");
if(!$conn){
  die("Database Error");
}
session_start();
?>
<!DOCTYPE html>
<html>
<head>
<title>SMM Panel</title>
<link rel="stylesheet" href="style.css">
</head>
<body>
<h1>Instagram SMM Panel</h1>
<a href="login.php">Login</a> | <a href="register.php">Register</a>
</body>
</html>
<?php
include 'config.php';
if(isset($_POST['register'])){
  $name=$_POST['name'];
  $email=$_POST['email'];
  $pass=password_hash($_POST['password'], PASSWORD_DEFAULT);

  mysqli_query($conn,"INSERT INTO users(name,email,password) VALUES('$name','$email','$pass')");
  header("Location: login.php");
}
?>
<form method="post">
<input name="name" placeholder="Name"><br>
<input name="email" placeholder="Email"><br>
<input name="password" type="password" placeholder="Password"><br>
<button name="register">Register</button>
</form>
<?php
include 'config.php';
if(isset($_POST['login'])){
  $email=$_POST['email'];
  $pass=$_POST['password'];

  $q=mysqli_query($conn,"SELECT * FROM users WHERE email='$email'");
  $u=mysqli_fetch_assoc($q);

  if(password_verify($pass,$u['password'])){
    $_SESSION['uid']=$u['id'];
    $_SESSION['role']=$u['role'];
    header("Location: dashboard.php");
  }
}
?>
<form method="post">
<input name="email"><br>
<input name="password" type="password"><br>
<button name="login">Login</button>
</form>
<?php
include 'config.php';
if(!isset($_SESSION['uid'])) header("Location: login.php");
?>
<h2>Dashboard</h2>
<a href="order.php">New Order</a><br>
<a href="payment.php">Add Balance</a>
<?php
include 'config.php';
if(isset($_POST['order'])){
  $sid=$_POST['service'];
  $link=$_POST['link'];
  $qty=$_POST['qty'];
  $uid=$_SESSION['uid'];

  mysqli_query($conn,"INSERT INTO orders(user_id,service_id,link,quantity)
  VALUES('$uid','$sid','$link','$qty')");
}
$services=mysqli_query($conn,"SELECT * FROM services");
?>
<form method="post">
<select name="service">
<?php while($s=mysqli_fetch_assoc($services)){ ?>
<option value="<?=$s['id']?>"><?=$s['service_name']?></option>
<?php } ?>
</select><br>
<input name="link" placeholder="Instagram Link"><br>
<input name="qty" placeholder="Quantity"><br>
<button name="order">Submit</button>
</form>
<?php
include 'config.php';
if(isset($_POST['pay'])){
  $txn=$_POST['txn'];
  mysqli_query($conn,"INSERT INTO payments(user_id,upi_txn)
  VALUES('{$_SESSION['uid']}','$txn')");
}
?>
<h3>Pay via UPI</h3>
<p>UPI ID: <b>70618712@ibl</b></p>
<form method="post">
<input name="txn" placeholder="UPI Transaction ID"><br>
<button name="pay">Submit</button>
</form>

