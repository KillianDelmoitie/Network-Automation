# Network-Automation

##Make your OS ready for Ansible
In this example I used Redhat
The commands below install all needed programs:
```
sudo yum update
&& sudo yum install python3
&& sudo yum install epel-release
&& sudo yum install git
&& sudo yum install make
&& sudo yum install perl-CPAN
```
We also have to install PIP to get all requirements.
```
wget https://bootstrap.pypa.io/get-pip.py
python3 ./get-pip.py
```

When using old Cisco hardware, which was my case, I had to install an old version of openssl to support and send my Ansible scripts to these network devices:
```
wget https://www.openssl.org/source/openssl-1.0.2u.tar.gz 
tar -xzvf openssl-1.0.2u.tar.gz
cd openssl-1.0.2u
sudo ./config
sudo make install 
sudo ln -sf /usr/local/ssl/bin/openssl `which openssl`
openssl version -v (should be OpenSSL1.0.2u)
```
Now we can start by cloning the git repo. When using old hardware it is important to move the config file to your .ssh file, and maybe adapt this file to your needs and configurations:
```
git clone https://github.com/KillianDelmoitie/Network-Automation.git
cd Network-Automation/
mv config ../.ssh/config
```
Then we are ready to install all requirements with PIP, which includes Ansible:
```
pip install -r requirements.txt 
```

Now that Ansible is downloaded we use ansible-galaxy to add the required collections to your Ansible project:
```
ansible-galaxy collection install cisco.ios
ansible-galaxy collection install ansible.netcommon
```
