##OpenerpAcademy.com
###Episode 5 - Installing OpenERP V8 from Source on Ubuntu

(watch the full episode at openerpacademy.com)[http://wp.me/p4Bowk-1f]

#####Commands used in this episode

```
# Install Vagrant vbguest plugin
vagrant plugin install vagrant-vbguest
 
# Inititalize the Vagrant box
vagrant init hashicorp/precise32
vagrant ssh

# Update the server
sudo apt-get update
yes | sudo apt-get dist-upgrade
exit

# Reload box
vagrant reload
vagrant ssh

# Update the locales
export LANGUAGE=en_US.UTF-8
export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8
sudo dpkg-reconfigure locales

# 2.  Install Postgresql and GIT
yes | sudo apt-get install python-software-properties 
sudo add-apt-repository ppa:pitti/postgresql 
sudo apt-get update
yes | sudo apt-get install postgresql-9.2 git-core

# 3.  Create Database user for OpenERP and set appropriate permissions
sudo -u postgres createuser --createdb --no-createrole --no-superuser --pwprompt openerp

# 4.  Create OpenERP user and group
sudo adduser --system --home=/opt/openerp --group openerp

# 5.  Install Python Libraries: Dependencies for OpenERP
yes | sudo apt-get install python-dateutil python-docutils python-feedparser python-jinja2 python-ldap python-libxslt1 python-lxml python-mako python-mock python-openid python-psycopg2 python-psutil python-pybabel python-pychart python-pydot python-pyparsing python-reportlab python-simplejson python-tz python-unittest2 python-vatnumber python-vobject python-webdav python-werkzeug python-xlwt python-yaml python-zsi poppler-utils python-pip

# 6.  Install GData
cd /opt/openerp
sudo wget http://gdata-python-client.googlecode.com/files/gdata-2.0.17.tar.gz
sudo tar zxvf gdata-2.0.17.tar.gz
sudo chown -R openerp: gdata-2.0.17
sudo -s
cd gdata-2.0.17/
python setup.py install
cd ..
exit

# 7.  Get lastest OpenERP (Odoo) source from github
sudo git clone https://github.com/odoo/odoo.git
sudo chown -R openerp: odoo

# 8.  Create folder for custom and test addons
sudo mkdir custom-addons test-addons
sudo chown -R openerp: custom-addons
sudo chown -R openerp: test-addons

# 9.  Setup OpenERP Log file
sudo mkdir /var/log/openerp
sudo chown -R openerp:root /var/log/openerp

# 10.  Create OpenERP configuration file
sudo cp /vagrant/openerp-server.conf /etc/openerp-server.conf
sudo chown openerp: /etc/openerp-server.conf

# 11.  Create OpenERP service file -- /etc/init.d/openerp-server
sudo cp /vagrant/openerp-server /etc/init.d/openerp-server
sudo chmod 755 /etc/init.d/openerp-server
sudo chown root: /etc/init.d/openerp-server
sudo update-rc.d openerp-server defaults

# 12.  Start OpenERP and verify log file for startup 
sudo service openerp-server start
```