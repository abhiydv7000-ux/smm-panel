
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

