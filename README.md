#Vagrant Box Setup
#Requires Base Box "Lucid32"
#xcode is required on osx in order to chef-install

git clone https://github.com/troyxmccall/vagrant-nginx-php-mysql.git vagrantnginx

cd vagrantnignx

gem install librarian

librarian-chef install

vagrant up

http://33.33.33.33

