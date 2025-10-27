```shell
# Root
mjolnir123

# Print to screen
echo Hi

# List files & folders
ls

# Change directory
cd my_dir1

# Present working directory
pwd

# Make directory
mkdir new_directory

# Multiple commands
cd directory; mkdir new_directory; pwd

# Make directory hierarchy
mkdir -p /tmp/asia/india/bangalore

# Remove directory
rm -r /tmp/my_dir1

# Copy directory
cp -r my_dir1 /tmp/my_dir1

# Create a new file with no content
touch new_file.txt

# Add contents to file
cat > new_file.txt # CTRL + d to finish

# View the content of the file
cat new_file.txt

# Copy a file
cp new_file.txt copy_file.txt

# Move / Rename file
mv new_file.txt sample_file.txt

# Remove a file
rm new_file.txt

# Identify the current user
whoami

# Identify the user's different IDs
id

# Switch user
su username

# Connect to another host through SSH
ssh username@ip-address

# Execute a command as admin
sudo command

# Download file
curl url-site -O
# Alternative
wget url-site -O filename.ext

# Check the OS version
ls /etc/*release*
cat /etc/*release*
```
### Package manager
```shell
# Check for packages
apt list package

# Remove a package
apt remove package

# Check for duplicated packages
apt ---showduplicates list package
```
### Services
```shell
# Start a service
service <service_name> start
# Alternative
systemctl start <service_name>

# Stop a service
systemctl stop <service_name>

# Check a service status
systemctl status <service_name>

# To start a service at startup
systemctl enable <service_name>

# To not start a service at startup
systemctl disable <service_name>
```

Example of a unit config file, using an http server made with Python.
It'll be placed in: `etc/systemd/system/<app_name>.service`
```shell
[Unit]
Description=Mypython web application

[Service]
ExecStart=/usr/bin/python3 /opt/code/my_app.py
ExecStartPre=/opt/code/configure_db.sh
ExecPost=/pot/code/email_status.sh
Restart=always

[Install]
WantedBy=multi-user.target
```

