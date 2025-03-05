# roots-bedrock-sage-docker
A Dockerized WordPress setup using Roots Bedrock &amp; Sage form modern development.

Step 1: Install Bedrock:
Use Composer to install Bedrock. This command will create a new Bedrock project in the current directory.

```
composer create-project roots/bedrock bedrock-demo
```
Step 2: Install Sage:
Navigate to the themes directory and install Sage.

```
cd web/app/themes
composer create-project roots/sage sage-demo
cd sage-demo
```
Step 3: Install Required Packages for Sage:
Run the following commands to install necessary dependencies for Sage.

```
npm install
npm run build
```
Step 4: Copy files from the repository to your root directory, then run following command

```
docker-compose build
docker-compose up -d
```
Step 5: Access Your WordPress Site & Finalize WordPress Installation:
Open a web browser and navigate to http://localhost (or the appropriate URL based on your Docker setup).

Step 6: 
Complete WordPress Installation:
Follow the standard WordPress installation process by accessing your site in the browser and completing the setup wizard.

Step 7: Activate Sage Theme:
Once WordPress is installed, log in to the admin dashboard and activate the Sage theme.

Step 8: Troubleshooting
Common Issues:

Ensure that Docker and Docker Compose are installed and running correctly.

Check for port conflicts if you encounter issues accessing your site.

Verify that your .env file is correctly configured.

This guide should help you set up a Dockerized WordPress environment with Roots Bedrock and Sage. Make sure to adjust the configuration files according to your specific needs.
