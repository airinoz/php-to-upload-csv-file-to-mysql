<?php
            //database connection details
            $connect = mysql_connect('localhost','XXXXX','XXXXXXX');

            if (!$connect) {
             die('Could not connect to MySQL: ' . mysql_error());
            }

            //your database name
            $cid =mysql_select_db('my_db_name',$connect); 

            //get the csv file 
            $file = $_FILES[csv][tmp_name]; 

            if (($handle = fopen($file, "r")) !== FALSE) {
                fgetcsv($handle);   
                while (($data = fgetcsv($handle, 360, ",")) !== FALSE) {
                        $num = count($data);
                        for ($c=0; $c < $num; $c++) {
                            $col[$c] = $data[$c];
                        }

                        $col1 = $col[0];
                        $col2 = $col[1];
                        $col3 = $col[2];
                        $col4 = $col[3];
                        $col5 = $col[4];
                        $col6 = $col[5];
                        $col7 = $col[6];

                         // SQL Query to insert data into DataBase
                        $query1 = "INSERT INTO transport(type) VALUES('".$col1."')";
                        $query3 = "INSERT INTO ward_tmode(year, value) VALUES('$col2','$col4')";
                        $query4 = "INSERT INTO ward(ward_name, lat, lon) VALUES('$col3','$col5','$col6')";
                
                        $a = mysql_query($query1, $connect);
                        $c = mysql_query($query3, $connect);
                        $d = mysql_query($query4, $connect);

                    }
                    echo "<br>File data successfully imported to database!!<br><br>";
                    echo "<a href='showtable.php'> show table </a>";
                    fclose($handle);
            }

            mysql_close($connect);
        ?>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"> 
<html xmlns="http://www.w3.org/1999/xhtml"> 
<head> 
<meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" /> 
<title>Import a CSV File with PHP & MySQL</title> 
</head> 

<body> 

<?php if (!empty($_GET[success])) { echo "<b>Your file has been imported.</b><br><br>"; } //generic success notice ?> 

<form action="" method="post" enctype="multipart/form-data" name="form1" id="form1"> 
  Choose your file: <br /> 
  <input name="csv" type="file" id="csv" /> 
  <input type="submit" name="Submit" value="Submit" /> 
</form> 

</body> 
</html>
