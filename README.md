# OdooProject
	Before You begin you need to set up ubuntu envirement by checking Python and Wklhm..  version	and set up the enviroment and stuff thisz can take you sometime	and dont forget to set up the Reginx
	PS: the directory f the folder should be /opt/odoo13

								Install Odoo 13 on Ubuntu 16.04




** MT Software **

sudo apt update && sudo apt upgrade
	
sudo apt install git python3-pip build-essential wget python3-dev python3-venv python3-wheel libxslt-dev libzip-dev libldap2-dev libsasl2-dev python3-setuptools node-less


**Create Odoo user **

sudo useradd -m -d /opt/odoo13 -U -r -s /bin/bash odoo13

*Install PostgreSQL **

sudo apt install postgresql

sudo su - postgres -c "createuser -s odoo13"

** Install Wkhtmltopdf **

wget https://builds.wkhtmltopdf.org/0.12.1.3/wkhtmltox_0.12.1.3-1~bionic_amd64.deb

sudo apt install ./wkhtmltox_0.12.1.3-1~bionic_amd64.deb


** Install Odoo **

sudo su - odoo13

git clone https://www.github.com/odoo/odoo --depth 1 --branch 13.0 /opt/odoo13/odoo

cd /opt/odoo13
python3 -m venv odoo-venv

source odoo-venv/bin/activate

pip3 install wheel
pip3 install -r odoo/requirements.txt

deactivate

mkdir /opt/odoo13/odoo-extra-addons

exit

sudo cp /opt/odoo13/odoo/debian/odoo.conf /etc/odoo13.conf

sudo nano /etc/odoo13.conf

----------------------------------------------------------

[options]
; This is the password that allows database operations:
admin_passwd = admin_passwd
db_host = False
db_port = False
db_user = odoo13
db_password = False
addons_path = /opt/odoo13/odoo/addons,/opt/odoo13/odoo-extra-addons

----------------------------------

** Service Odoo ** 

sudo nano /etc/systemd/system/odoo13.service

-----------------------------

[Unit]
Description=Odoo13
Requires=postgresql.service
After=network.target postgresql.service

[Service]
Type=simple
SyslogIdentifier=odoo13
PermissionsStartOnly=true
User=odoo13
Group=odoo13
ExecStart=/opt/odoo13/odoo-venv/bin/python3 /opt/odoo13/odoo/odoo-bin -c /etc/odoo13.conf
StandardOutput=journal+console

[Install]
WantedBy=multi-user.target


-----------------------------------------------

sudo systemctl daemon-reload
sudo systemctl start odoo13
sudo systemctl status odoo13
sudo systemctl enable odoo13



Run Browser 
 ==> http://<domain_or_IP_address>:8069




 




