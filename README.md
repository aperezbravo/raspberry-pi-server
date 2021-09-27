# raspberry-pi-server

Make your own server using a raspberry pi. You will need a raspberry pi and  a USB of any kind.

Hardware:
- Raspberry Pi 4: 4gb Ram
- Seargate external SSD: 500gb

Software:
- NGINX


Format SSD:
	determine what file format you want your drive in
	choose a suitable fs that allows Raspi OS to read and write.

Mounting SSD:
	Connect  drive check the mounted drives and their partitions.
	```
	lsblk
	```
	mount the available partiotion from your drive to the desired folder
	```
	sudo mount /dev/sda1 /var/www/media/ssd1
	```
Download & SetUp NGINX:
	Download nginx
	```
	sudo apt install nginx
	```
	edit nginx config file
	```
	sudo vim /etc/nginx/sites-enabled/default
	```
	add a location block inside the main server block
	```
	location / {
	}
	```
	location block takes the name of the desired URL
	```
	location /media/ {
	}
	```
	now we need to rote the user to the correct directory by defining the path
	```
	location /media/
		alias /var/www/media/ssd1/;
	}
	```
	in order to  list the files in the specified path we must specify it by adding the fillowing line
	```
	location /media/ {
		alias /var/www/media/ssd1/;
		autoindex on;
	}
	```
Auto mount ssd on startup:
	check for the UUID, careful to make sure it is the correct one
	```
	blkid
	```
