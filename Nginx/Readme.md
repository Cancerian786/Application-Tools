<p align="center">
  <img src="https://github.com/Cancerian786/Favicon/blob/main/nginx.png" alt="DevOpsGuru Banner">
</p>

# 🎉 Welcome to DevOpsGuru

# 📦 PROCESS TO INSTALL NGINX

# 📄 If you are Using Latest Version of RHEL Distribution of Linux, You Can follow below Steps.

# 🔄 Step 1: Update Your System

<update>

sudo yum -y update

</update>

📦 Step 2: Install the Extra Packages for Enterprise Linux (EPEL) Repository

Nginx is not included in the standard CentOS repositories, so you need to install the EPEL repository. EPEL is a free resource that offers a wide range of open-source packages for installation using Yum.

# To install EPEL, use the following command:

sudo yum install -y epel-release

🚀 Step 3: Install and Configure Nginx

After installing the EPEL repository, you can install Nginx on your server. Use the following commands:

# Install Nginx

sudo yum -y install nginx

# Start Nginx and enable it to start on boot

sudo systemctl start nginx
sudo systemctl enable nginx

🔐 Step 4: Configure Firewall for HTTP/HTTPS Traffic

# To allow web traffic, configure your firewall with these commands:

firewall-cmd --zone=public --permanent --add-service=http
firewall-cmd --zone=public --permanent --add-service=https

# Reload the Firewall, After applying the Changes:

firewall-cmd --reload

# Enable Nginx in Config-Manager (Not Compulsory):

yum-config-manager --enable nginx

## 📄 If you are Using Older Version of RHEL Distribution of Linux which is EOL(End Of Life) Support, You Can follow below Steps.

# ⚙️ Change the Repository/Mirror URL link:

<>
vi /etc/yum.repos.d/CentOS-Base.repo

Replace the entire data present in <CentOS-Base.repo>, with the below Given data
</>

<>

# /etc/yum.repos.d/CentOS-Base.repo

[base]
name=CentOS-$releasever - Base
baseurl=http://vault.centos.org/7.9.2009/os/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

[updates]
name=CentOS-$releasever - Updates
baseurl=http://vault.centos.org/7.9.2009/updates/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

[extras]
name=CentOS-$releasever - Extras
baseurl=http://vault.centos.org/7.9.2009/extras/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

[centosplus]
name=CentOS-$releasever - Plus
baseurl=http://vault.centos.org/7.9.2009/centosplus/$basearch/
gpgcheck=1
enabled=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

[contrib]
name=CentOS-$releasever - Contrib
baseurl=http://vault.centos.org/7.9.2009/contrib/$basearch/
gpgcheck=1
enabled=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

</>

# 🔄 Step 1: Update Your System

sudo yum -y update

# 📦 Step 2: Install EPEL Repository, use the following command:

<>
sudo yum install -y epel-release
</>

# 🚀 Step 3: Install and Configure Nginx

<>
sudo yum -y install nginx
</>

# 🛠️ Step 4: Start Nginx and enable it to start on boot

<>
sudo systemctl start nginx
sudo systemctl enable nginx
</>

🔐 Step 5: Configure Firewall for HTTP/HTTPS Traffic

# To allow web traffic, configure your firewall with these commands:

<>
firewall-cmd --zone=public --permanent --add-service=http
firewall-cmd --zone=public --permanent --add-service=https
</>

# Reload the Firewall, After applying the Changes:

<>
firewall-cmd --reload
</>
