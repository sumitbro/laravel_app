# Laravel application with Nginx, Mysql with Docker Compose.

### Project Setup
```
Firstly I have download the Laravel project from https://github.com/laravel/laravel.git.
Then i have install the application dependencies using following command. 
docker run --rm -v “$(pwd)”:/app composer install
```

### Creating a docker-compose file
Inside the docker-compose.yaml file, I have added three different services to the file to configure my application’s services. Then, with a single command, I can create and start all the services from my configuration.

### Three services are:
```
a. App: It defines the Laravel application and runs a custom Docker image, sumitlab/laravel. It also sets the working_dir in the container to /var/www/html.

b. NGINX webserver: It pulls the nginx:alpine image from Docker and exposes ports 80 and 443.

c. MY SQL: It pulls the mysql:5.7.22 image from Docker and defines a few environmental variables. These include a database called laravel for the application and the root password for the database. This service also maps port 3306 on the host to port 3306 on the container. 

```

### Creating a Dockerfile
```
Dockerfile includes instructions that Docker can use to build custom Docker images. It can also install the software required and configure the necessary settings for my application. They specify the environment inside a container that will host your application code. 

The Dockerfile creates an image on top of the php:7.2-fpm Docker image. This is a Debian-based image that has the PHP FastCGI implementation PHP-FPM installed. The file also installs the prerequisite packages for Laravel: mcrypt, pdo_mysql, mbstring, and imagick with composer.
```
### Configuring Nginx
```
To configure Nginx, I create an app.conf file with the service configuration in the /nginx/conf.d/ folder.
create the app.conf configuration file using command:
 nano /nginx/conf.d/app.conf 
and then added the code to the file to specify my Nginx configuration
```

###  Modifying Environment Settings and Running the Containers
```
Open .env file using nano and edit the environment variable

DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=laraveluser
DB_PASSWORD=admin123

```
### With all of your services defined in  docker-compose file, use the following single command to start all of the containers, create the volumes, and set up and connect the networks:

```
docker-compose up -d
```
### Use the following command to list all of the running containers:
```
docker ps
```

You’ll now use docker-compose exec to set the application key for the Laravel application. The docker-compose exec command allows you to run specific commands in containers.

The following command will generate a key and copy it to your .env file, ensuring that your user sessions and encrypted data remain secure:
```
docker-compose exec app php artisan key:generate
```
### In this way finaly  our laravel application is fully setup using docker-compose, mysql and nginx. Thankyou
