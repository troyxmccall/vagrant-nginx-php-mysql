#Vagrant Box Setup
#Requires Base Box "Lucid32"
##xcode is required on osx in order to chef-install

	git clone https://github.com/troyxmccall/vagrant-nginx-php-mysql.git vagrantnginx

	cd vagrantnginx

	gem install librarian

	librarian-chef install

	vagrant up

	#you can now visit http://33.33.33.33

	vagrant shh

	sudo apt-get install vim

	sudo vim /etc/nginx/sites-available/default

#example config here
https://gist.github.com/3913295



