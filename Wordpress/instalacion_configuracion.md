# Script de Automatización LAMP (User Data utilizado)

```bash
#!/bin/bash
dnf update -y
dnf install -y httpd php php-mysqlnd php-gd php-xml php-mbstring mariadb105-server tar wget
systemctl start httpd
systemctl enable httpd
systemctl start mariadb
systemctl enable mariadb

mysql -e "CREATE DATABASE wordpress_db;"
mysql -e "CREATE USER 'wp_user'@'localhost' IDENTIFIED BY 'NovaPass2026*';"
mysql -e "GRANT ALL PRIVILEGES ON wordpress_db.* TO 'wp_user'@'localhost';"
mysql -e "FLUSH PRIVILEGES;"

cd /var/www/html
wget [https://wordpress.org/latest.tar.gz](https://wordpress.org/latest.tar.gz)
tar -xzf latest.tar.gz
cp -r wordpress/* .
rm -rf wordpress latest.tar.gz
chown -R apache:apache /var/www/html
chmod -R 755 /var/www/html