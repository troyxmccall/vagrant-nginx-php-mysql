##Vagrant Nginx/PHP/MYSQL Box Setup

###Requirements: Vagrant, Oracle VirtualBox, Base Box (Precise64)
*Xcode is required on OSX for librarian-chef install

	git clone https://github.com/troyxmccall/vagrant-nginx-php-mysql.git vagrantnginx

	cd vagrantnginx

	gem install librarian

	librarian-chef install

	vagrant up

	vagrant shh

	sudo apt-get install vim

	sudo vim /etc/nginx/sites-available/default



##example config here
https://gist.github.com/3913295

##restart nginx
	sudo /etc/init.d/nginx restart


##remember to update your machine host file
	vim /private/etc/hosts
		33.33.33.33     precise64.dev
