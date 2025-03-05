# roots-bedrock-sage-docker
A Dockerized WordPress setup using Roots Bedrock &amp; Sage form modern development.

Step 1: Install Bedrock and Sage
Create a New Project Directory:

bash
mkdir my-wordpress-project
cd my-wordpress-project
Install Bedrock:
Use Composer to install Bedrock. This command will create a new Bedrock project in the current directory.

bash
composer create-project roots/bedrock .
Install Sage:
Navigate to the themes directory and install Sage.

bash
cd web/app/themes
composer create-project roots/sage my-sage-theme
cd my-sage-theme
Install Required Packages for Sage:
Run the following commands to install necessary dependencies for Sage.

bash
npm install
npm run build
Step 2: Configure Bedrock
Create a .env File:
Copy the .env.example file to .env and configure your database settings.

bash
cp .env.example .env
Edit .env File:
Open the .env file and update the database settings (e.g., DB_NAME, DB_USER, DB_PASSWORD, DB_HOST).

Step 3: Set Up Docker Environment
Create a docker-compose.yml File:
In your project directory, create a file named docker-compose.yml. Here's a basic example of what it might look like:

text
version: '3'
services:
  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: your_root_password
      MYSQL_DATABASE: your_db_name
      MYSQL_USER: your_db_user
      MYSQL_PASSWORD: your_db_password
    volumes:
      - db-data:/var/lib/mysql

  web:
    build: .
    ports:
      - "80:80"
    depends_on:
      - db
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: your_db_user
      WORDPRESS_DB_PASSWORD: your_db_password
      WORDPRESS_DB_NAME: your_db_name

volumes:
  db-data:
Create a Dockerfile:
In the same directory, create a Dockerfile for your web service. Here's a simple example:

text
FROM php:8.1-apache

# Install dependencies
RUN apt-get update && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libpng-dev libzip-dev libzip

# Set working directory to /var/www/html
WORKDIR /var/www/html

# Copy existing site files
COPY . /var/www/html/

# Expose port 80 to the docker host, so we can access it
EXPOSE 80

# Configure environment variables
ENV COMPOSER_HOME app/composer
ENV COMPOSER_CACHE_DIR app/composer/cache

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install dependencies
RUN composer install --no-dev --prefer-dist

# Start Apache when the container launches
CMD ["apache2-foreground"]
Build and Run Docker Containers:
From your project directory, run the following commands:

bash
docker-compose build
docker-compose up -d
Access Your WordPress Site:
Open a web browser and navigate to http://localhost (or the appropriate URL based on your Docker setup).

Step 4: Finalize WordPress Installation
Complete WordPress Installation:
Follow the standard WordPress installation process by accessing your site in the browser and completing the setup wizard.

Activate Sage Theme:
Once WordPress is installed, log in to the admin dashboard and activate the Sage theme.

Step 5: Troubleshooting
Common Issues:

Ensure that Docker and Docker Compose are installed and running correctly.

Check for port conflicts if you encounter issues accessing your site.

Verify that your .env file is correctly configured.

This guide should help you set up a Dockerized WordPress environment with Roots Bedrock and Sage. Make sure to adjust the configuration files according to your specific needs.
