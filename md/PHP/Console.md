
##Console

###DNS Lookup Script Example
This program just parse file like:
```php
 Apr 09 08:27:17 43.254.0.31
 Apr 09 08:30:17 64.207.183.49
 Apr 09 08:30:17 65.307.383.49
 Apr 09 08:45:17 33.111.54.31
 ```
and replace the ip address to domainame if it's found

```php
 <?php
 if (count($argv) == 1) {
         echo "Usage: ip2dn.php <filename>\n";
         return;
 }
 $lines = file($argv[1]);
 foreach ($lines as $num=>$line) {
         list($mon,$day,$time,$ip) = split(" ",$line);
         echo $mon." ".$day." ".$time." ".gethostbyaddr(trim($ip))."\n";
 }
 ?>
 ```




