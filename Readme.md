This is a documentation to complete a development environment of LARAVEL + Docker in Linux(Ubuntu 18.04) + NGINX + MSSQL
SQL Server has been installed in docker

First install wsl in your pc so that you can use linux based dokcer.


If you are using windows 10(home) or lesser version then you can't use docker desktop. you have to use docker toolbox.


Install docker and docker-compose in wsl. You also have to configure your docker so that it can work with docker toolbox.(you can follow the instruction provided here==>https://medium.com/@joaoh82/setting-up-docker-toolbox-for-windows-home-10-and-wsl-to-work-perfectly-2fd34ed41d51)

After completing installation you can check whether docker is working perfectly or not.
Run==> docker--version & docker-compose --version in Ubuntu.
Also run ==> docker run hello-world to check if docker in wsl are working combinedly with docker toolbox.

Then make a directory in your wsl workspace and open that directory in VS code. Maybe you need to install a vscode plugin to work with wsl folder or VScode will automatically detect the plugin and you need to install it.

NOTE: we are going to install the mssql server in docker so you don't need to install sql server in your machine. You can use MSSQL Server management studio to visualize the database.

Now create a docker-compose.yml file in the root of the project directory.
Also create a directory named docker-config in root directory.
Then create 2 directories named php, nginx in docker-config directory.

we will use the official php7.3-fpm image for php environment and will also modify the image a little so that we can run laravel application using that image.
we will also install php driver for sql server in the image so that we can access to mssql database.

For nginx we will use tthe official nginx:alphine image.

create a laravel project in the root project directory.
Change the .env folder in your laravel project folder and put the credential for sqlsrv.

For mssql we will use the microsoft official sqlserver 2017 image.




If you are pulling from github you can start from here==>

give your pc's user name in docker-copose file's app section


if everything is complete you can run " docker-compose up -d " and it will serve the laravel app in 8000 port.

then find the ip where your wsl docker is hosting. To find the ip run "docker-machine env". then run that_ip:8000( For example 192.168.99.100:8000) in your browser
 
if you see that sql server image can't run in your docker machine then you need to increase your docker memory. Initially it is set to 2GB so you need to increase it to 4GB.
***for increasing docker memory run the following command in docker quickstart terminal
-->docker-machine rm default
-->docker-machine create -d virtualbox --virtualbox-cpu-count=2 --virtualbox-memory=4096 --virtualbox-disk-size=50000 default
-->docker-machine stop
-->exit



open sql server management studio and connect to the container where sql server is installed using the server address(the ip where your wsl docker is hosting) for the server address you can run run "docker-machine env" in docker quickstart terminal. The default user is ==> sa and the password will be set by you.
Using sql server management studio create a database named testdb.

you can also use artisan command in docker-compose(For example: docker-compose exec app php artisan serve)





