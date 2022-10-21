---
title: Install php-Mongo driver on Windows XAMPP
date: 2018-12-15 21:05:17
tags: ['tutorial', 'windows', 'php', 'mongo']
cover: 
    src: https://zdnet3.cbsistatic.com/hub/i/r/2018/02/16/8abdb3e1-47bc-446e-9871-c4e11a46f680/resize/370xauto/8a68280fd20eebfa7789cdaa6fb5eff1/mongo-db-logo.png
---

Honestly im Linux/unix user, but in this case , i’ll make my MAC turn into jendela or fvcking windows

I will configure MongoDB with PHP xampp. It is very easy to do. Oke let’s install latest XAMPP, 

cause i am using XAMPP ,

here we go !!
1 Installing MongoDB

2 Download MongoDB [here](https://s3.amazonaws.com/drivers.mongodb.org/php/)

3 Extract the archive , you will see all version of mongo.dll (read step 6)

4. Check your Php version by going to http://localhost/phpinfo.php , if u dont have .. (create a file phpinfo on ur htdocs)
You’ll see , version of php and “PHP Extension Build” on this pic
my php version is 5.6.8 , and “PHP Extension Build” = vc11
![image](https://alfathdirk.files.wordpress.com/2015/05/php.jpg)

5 Extract files mongo which downloaded before

6. copy php_mongo-1.6.8-5.6-vc11.dll to directory C:\\xampp\php\ext "5.6-vc11.dk => my php version and build extension" , make sure you’re copy the file with same version and build extension (re-read step 4)


7. open xampp control panel,Click “Config”->”PHP (PHP.ini)”->(notepad opened) and then add “extension=php_mongo-1.6.8-5.6-vc11.dll” on line 989 or up2you .. save

8. restart apache 😀

9. refresh browser phpinfo ,localhost/phpinfo.php , and find mongo extensions has been active on your xampp

![mongodb](https://alfathdirk.files.wordpress.com/2015/05/mongo.jpg)

oke Thanks
