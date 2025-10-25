[Comandos utilizados en Lab Modulo 4.txt](https://github.com/user-attachments/files/23138471/Comandos.utilizados.en.Lab.Modulo.4.txt)
Practica 1 Instalar un servidor HTTP apache2
sudo apt update
sudo apt install apache2 -y
sudo systemctl status apache2
sudo mkdir -p /var/www/holamundo
echo "<h1>Hola Mundo</h1>" | sudo tee /var/www/holamundo/index.html
sudo chown -R www-data:www-data /var/www/holamundo
sudo chmod -R 755 /var/www/holamundo
sudo nano /etc/apache2/sites-available/holamundo.conf
<VirtualHost *:80>
    ServerAdmin admin@localhost
    ServerName holamundo.local
    DocumentRoot /var/www/holamundo
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
sudo a2ensite holamundo.conf
sudo systemctl reload apache2
sudo a2dissite 000-default.conf
sudo systemctl reload apache2
sudo mkdir -p /var/www/juanesteban
echo "<h1>Juan Esteban - 20221760 - Administracion de Servidores Linux</h1>" | sudo tee /var/www/juanesteban/index.html
sudo nano /etc/apache2/sites-available/juanesteban.conf
<VirtualHost *:8080>
    ServerAdmin admin@localhost
    ServerName juanesteban.local
    DocumentRoot /var/www/juanesteban
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
sudo nano /etc/apache2/ports.conf
Listen 8080
sudo a2ensite juanesteban.conf
sudo systemctl reload apache2
curl http://localhost
curl http://localhost:8080
================================================================================

=================================================================================
Practica 3 Instalar un servidor de Impresion
sudo apt update
sudo apt install cups -y
sudo systemctl status cups
sudo nano /etc/cups/cupsd.conf
Busca estas líneas (pueden estar comentadas) y modifícalas así 👇🏽:

conf
Port 631
Listen /var/run/cups/cups.sock
ServerAdmin admin@localhost
WebInterface Yes

<Location />
  Order allow,deny
  Allow all
</Location>

<Location /admin>
  Order allow,deny
  Allow all
</Location>
sudo usermod -aG lpadmin $USER
sudo systemctl restart cups
http://<IP_DEL_SERVIDOR>:631
http://192.168.1.10:631
sudo apt install printer-driver-cups-pdf -y
/var/spool/cups-pdf/<usuario>/
mkdir -p ~/ImpresionesPDF
sudo ln -s /var/spool/cups-pdf/$USER ~/ImpresionesPDF
sudo apt install cups-client -y
ping <IP_DEL_SERVIDOR>
ping 192.168.1.10
lpstat -a

sudo nano /etc/cups/client.conf

php-template

ServerName <IP_DEL_SERVIDOR>

sudo systemctl restart cups

lpstat -a

libreoffice --headless --pt PDF prueba.docx

echo "Hola soy Juan Esteban - 20221760" | lp -d PDF

/var/spool/cups-pdf/<usuario>/
