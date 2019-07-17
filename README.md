# PHPproject
My Mini Project
This is a website which can efficiently manage database of students applying for scholarship.
The code is simple but it is efficient to manage a large number of students.


PHP Snippets of the code:
<?php
	session_start();

	if( isset($_SESSION['admin_id1']) ){
		header("Location: /SMS/admindashboard.php");
	}

	require 'database.php';
	if(isset($_POST['admin_submit'])){
	if(!empty($_POST['admin_id']) && !empty($_POST['password2'])):
	$records = $conn->prepare('SELECT * FROM admin WHERE admin_id = :admin_id1');
	$records->bindParam(':admin_id1', $_POST['admin_id']);
	$records->execute();
	$results = $records->fetch(PDO::FETCH_ASSOC);
	$message = '';

	if(count($results) > 0 && ($_POST['password2']==$results['admin_pass'])){
		$_SESSION['admin_id1'] = $results['admin_id'];
		$_SESSION['admin_email1'] = $results['admin_email'];
		$message = 'Welcome Admin!';
		header("Location: /SMS/admindashboard.php");
		echo $message;
	} else {
		$message = 'Sorry, those credentials do not match';
		echo $message;
	}
	endif;
	}
?>






