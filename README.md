# WordPressOnlineStore
Disploy a onlinestore in Google cloud using a WordPress
Step One:
  
  1. create a project
  2. create an vm in google cloud
  3. Allow http and https traffic

Step two:
  4. make ip address static through Network Setting
  5. create a DNS zone
  6. add A zone record pointing to the static ip address
  7. add a CNAME record 
  8. point the domain name "Name Server" to the gcloud name server
 
Step three:
  1. Connect to the server though gcloud command or SSH
  
Step Four:
  2. install lamb-server (Or apache2 php,myssql)
  3. make the website site folder in /var/www/ name yourdomain.com
  4. cp /etc/apache2/site-availables/000.conf to /etc/apache2/site-availables/yourdomain.com.conf
  5. config yourdomain.com.conf including SeverName
  6. a2ensite yourdomain.com
  7. systemctl reload apache2
  8. systemctl restart apache2.service
  
Step Four:
  1. create database and config
  
Step Five:
  1. in /var/www/youdomain.com install wordpress
  2. wget https://wordpress.org/latest.tar.gz
  3. tar -xvf latest.tar.gz
  4. config wp-config.php
  
Step Six:
  5. imput yourdomain.com in the brownser;
  6. save the password
  7. install plugin or theme
  8. chown -R www-data /var/www/yourdomain.com if the website ask for ftp authority
  9. edit /etc/apache2/apache2.conf (/ /var/www/ Allow ALL)
  
 Step 7 ssl:
  1. buy ssl
  2. activate the ssl
  3. use http DSV: cp certificate.txt /var/www/youdomain.com/.well-known/pki-validation/
  4. vist http://yourdomain.com/.well-known/pki-validation/certificate.txt
  5. ssl issued
  6. install ssl in the server
  7. download crt and private key and bundle key ,copy to /etc/ssl/
  8. cp yourdomain.com.conf yourdomain.com-ssl.conf
  9. config yourdomain.com-ssl.conf( SSLCertificateFile /etc/ssl/certs/, SSLCertificatePrivateKey /etc/ssl/private/, SSLCertificateBundle /etc/ssl/bundle)
  1. apachectl -t
  2. apachectl restart if Syntax OK
  3. Google blocked by default port 443,so run the command: sudo a2enmod ssl
  4. make the website http redirect to the https automatically: edit .htacess and add the following:
  RewriteEngine On
RewriteCond %{HTTPS} !=on
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301,NE] 
  
  
