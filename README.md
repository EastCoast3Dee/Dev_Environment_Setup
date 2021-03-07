# Dev_Environment_Setup
Install, Configure, and Maintain your own development environment.

## Description
Install Apache, PHP, and MariaDB to get your development environment up and running.

## Table of Contents
1. Install Apache
2. Install PHP
3. Install MariaDB


## 1. Install Apache

1. Download the latest version of Apache from http://httpd.apache.org/download.cgi.

2. Click on the 'a number of third party vendors' link and choose the Apache Lounge option.

3. For Windows 10 (64 bit), download the .exe file below Apache 2.4.46 Win64.

![Screenshot 2021-03-06 150622](https://user-images.githubusercontent.com/75577872/110230390-ebe28180-7ee6-11eb-9a4c-fb2c260d36f6.png)


4. Move the Apache24 folder to the root of the c drive. (c:/Apache24).





## Run and Test

1. Navigate to c:\Apache24 and open a PowerShell window on the \bin folder. (shift + right click)

![Screenshot 2021-03-06 154905](https://user-images.githubusercontent.com/75577872/110230401-0a487d00-7ee7-11eb-8d2b-b24179dbd92c.png)

2. Enter .\httpd.exe and accept the permissions prompt.

3. There will be a blinking cursor below the coomand prompt if there were no errors.

4. To test the server is properly running, open a browser and go to http://localhost.

5. If properly installed and running, the page will display 'It works!'.

![Screenshot 2021-03-06 155010](https://user-images.githubusercontent.com/75577872/110230647-d3736680-7ee8-11eb-8dfc-d67bedd57d89.png)


6. Go back to the PowerShell window and enter CTRL + C to stop running the command.
 
 
 
 
 
## Register Apache as a Windows Service

1. In the PowerShell window for c:\Apache24\bin, enter .\htpd.exe -k install.

![Screenshot 2021-03-06 155937](https://user-images.githubusercontent.com/75577872/110230412-264c1e80-7ee7-11eb-8062-fc250f4ce953.png)

2. If successful, 'The Apache 2.4 service is successfully installed' will be displayed.

3. This can be confirmed by opening the Services snap-in and searching for Apache24.

4. Now Apache can be started, stopped, or restarted without using the command prompt.

5. Optional - open the c:/Apache/bin folder and double-click on ApacheMonitor.exe to install a
convenient icon to control Apache in the tray.




## Initial Config File for Apache

1. Navigate to c:/Apache24/conf and open the httpd.conf file (with a text editor ex: vscode).

2. Confirm Define SRVROOT is "c:/Apache24". (line 37)

3. Confirm the server is listening on port 80. (line 60) Listen 80

4. Notice the DocumentRoot "${SRVROOT}/htdocs" (line 251). This is where website content will be served from.

5. To ensure virtual hosts can be created, uncomment line 510, to allow configuration files for virtual hosts
to be accessed from conf/extra/httpd-vhosts.conf.

6. Disable directory browsing by changing line 265 to Options FollowSymLinks.

7. Restart Apache to apply the changes made.




## Creating Sites

1.  Create a new project folder for the site in c:/Apache24/htdocs named examplesite.tbd.

2.  Create an index.html file in the site folder.

3.  Add the site name to the hosts file. 127.0.0.1 examplesite.tbd

4.  Open c:/Apache24/config/extra and open httpd-vhosts.conf.

5.  Add the following virtual host configurations for the site:
 
     <VirtualHost *:80>
     
        DocumentRoot "${SRVROOT}/htdocs/examplesite.tbd"
        
        ServerName examplesite.tbd
        
     </VirtualHost>
     
     
     ![Screenshot 2021-03-06 213429](https://user-images.githubusercontent.com/75577872/110230445-6ca17d80-7ee7-11eb-9b61-92796d4ef3b3.png)

       
6.  Create another project folder for a second site in c:/Apache24/htdocs named newproject.tbd.

7.  Create an index.html file in the site folder.

8.  Add the site name to the hosts file. 127.0.0.1 newproject.tbd

9.  Open c:/Apache24/config/extra and open httpd-vhosts.conf.

10. Add the following virtual host configurations for the site:

    <VirtualHost *:80>
    
      DocumentRoot "${SRVROOT}/htdocs/newproject.tbd"
      
      ServerName newproject.tbd
      
    </VirtualHost>
    
    
    ![Screenshot 2021-03-06 232905](https://user-images.githubusercontent.com/75577872/110230495-bee29e80-7ee7-11eb-8a79-ac221400e74a.png)




## 2. Install PHP

1. Download PHP 8.0 from https://windows.php.net/download/.

2. Be sure to get the correct version by checking the information on the left side of the page.

3. For Windows 10 64 bit and the Apache build from Apache Lounge, download the Thread Safe version,
VS16 x64 Thread Safe.

4. Create a directory in the C drive (c:/phpApache) to extract the PHP files to.

5. In the PHP directory, rename the file php.ini-development to php.ini.




## Integrate PHP with Apache

1. Open php.ini in a text editor.

2. Locate extension_dir (line 766) and change the path to "C:/phpApache/ext", the ext folder in the php directory.

3. Open httpd.conf file with a text editor.

4. Locate the Directory Index (line 285) and add index.php.
    <IfModule dir_module>
       DirectoryIndex index.html index.php
    </IfModule>
    
5. At the end of the file, specify the Apache module, php extensions, and php.ini directory to integrate PHP.

    #PHP 8 Config
    
    LoadModule php_module "c:/phpApache/php8apache2_4.dll"
    
    AddType application/x-http-php .php
    
    PHPIniDir "C:/phpApache"
    
    ![Screenshot 2021-03-06 213452](https://user-images.githubusercontent.com/75577872/110230474-9eb2df80-7ee7-11eb-95f6-800e0595e235.png)

6. Restart Apache.
 
 
 
 
## Test PHP

1. In htdocs, open the examplesite.tbd folder and create a PHP file named index.php.

2. Open index.php in a text editor.

3. Add the following php script to the file:
    <?php
    phpinfo();
    
4. Rename index.html to indexold.html to allow index.php to be loaded.

5. Open http://examplesite.tbd in the browser.

6. If PHP has been successfully integrated, the PHP Version information page will be displayed in the browser.

![Screenshot 2021-03-06 232929](https://user-images.githubusercontent.com/75577872/110230628-a1fa9b00-7ee8-11eb-8de9-36719815a1a0.png)





## 3. Install MariaDB as database server

1. Download MariaDB from https://mariadb.org/download/.

2. Run the setup wizard to finish installation.




## Test MariaDB 

1. Open Services.

2. Locate MariaDB and and confirm it is running.

![Screenshot 2021-03-06 214920](https://user-images.githubusercontent.com/75577872/110230490-b2f6dc80-7ee7-11eb-80d0-9897f2cb738a.png)




## License
[MIT](https://choosealicense.com/licenses/mit/)
