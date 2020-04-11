# WordPressOnlineStore
Disploy a onlinestore in Google cloud using a WordPress
Step One:
  
  # create a project
  # create an vm in google cloud
  # Allow http and https traffic

Step two:
  # make ip address static through Network Setting
  # create a DNS zone
  # add A zone record pointing to the static ip address
  # add a CNAME record 
  # point the domain name "Name Server" to the gcloud name server
 
Step three:
  # Connect to the server though gcloud command or SSH
  
Step Four:
  # install lamb-server (Or apache2 php,myssql)
  # make the website site folder in /var/www/ name yourdomain.com
  # cp /etc/apache2/site-availables/000.conf to /etc/apache2/site-availables/yourdomain.com.conf
  # config yourdomain.com.conf including SeverName
  # a2ensite yourdomain.com
  # systemctl reload apache2
  # systemctl restart apache2.service
  
Step Four:
  # create database and config
  
Step Five:
  # in /var/www/youdomain.com install wordpress
  # wget https://wordpress.org/latest.tar.gz
  # tar -xvf latest.tar.gz
  # config wp-config.php
  
Step Six:
  # imput yourdomain.com in the brownser;
  # save the password
  # install plugin or theme
  # chown -R www-data /var/www/yourdomain.com if the website ask for ftp authority
  # edit /etc/apache2/apache2.conf (/ /var/www/ Allow ALL)
  
 Step 7 ssl:
  # buy ssl
  # activate the ssl
  # use http DSV: cp certificate.txt /var/www/youdomain.com/.well-known/pki-validation/
  # vist http://yourdomain.com/.well-known/pki-validation/certificate.txt
  # ssl issued
  # install ssl in the server
  # download crt and private key and bundle key ,copy to /etc/ssl/
  # cp yourdomain.com.conf yourdomain.com-ssl.conf
  # config yourdomain.com-ssl.conf( SSLCertificateFile /etc/ssl/certs/, SSLCertificatePrivateKey /etc/ssl/private/, SSLCertificateBundle /etc/ssl/bundle)
  # apachectl -t
  # apachectl restart if Syntax OK
  # Google blocked by default port 443,so run the command: sudo a2enmod ssl
  # make the website http redirect to the https automatically: edit .htacess and add the following:
  RewriteEngine On
RewriteCond %{HTTPS} !=on
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301,NE] 
  
  
