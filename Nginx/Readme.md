<p align="center">
  <img src="https://github.com/Cancerian786/Favicon/blob/main/nginx.png" alt="DevOpsGuru Banner">
</p>
# 🎉 Welcome to DevOpsGuru

# 🔄 Step 1: Update Your System

sudo yum -y update

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

# Apply the changes

firewall-cmd --reload

# Enable Nginx in Config-Manager

yum-config-manager --enable nginx
