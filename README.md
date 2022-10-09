# workspace
Dockerfile modified from laradock
Main Feature 
 - workspace (include nodejs and container with username : arn)
 - nginx
 - php-fpm
 - mysql
 - phpmyadmin
 - traefix
 - volume database to folder VOLUME-DATA (set in ENV for change)
 
 # ***************************************************** #
 
 - Easy switch between PHP versions: 8.1, 8.0, 7.4, 7.3, 7.2, 7.1, 5.6
 - Easy to customize any container, with simple edits to the Dockerfile.
 - All Images extend from an official base Image. (Trusted base Images).
 - Pre-configured NGINX to host any code at your root directory.
 - Can use Laradock per project, or single Laradock for all projects.
 - Everything is visible and editable.
 - Fast Images Builds.

# ***************************************************** #
Getting Started
Requirements
 - Git
 - Docker [ >= 17.12 ]

Setup for Single Project
   1. Already have a PHP project:
      Your folder structure should look like this:
      * project-a
      *   workspace-a
      * project-b
      *   workspace-b
      * cp .env.example .env

   2. Don’t have a PHP project yet:
      * workspace
      * project-z
        - cp .env.example .env
        - At the top, change the APP_CODE_PATH_HOST variable to your project path.
             - APP_CODE_PATH_HOST=../project-z/ (Make sure to replace project-z with your project folder name.)

Setup for Multiple Projects:
   Your folder structure should look like this:
   * workspace
   * project-1
   * project-2

    - Make sure the APP_CODE_PATH_HOST variable points to parent directory.
       APP_CODE_PATH_HOST=../
    - Go to your web server and create config files to point to different project directory when visiting different domains:
       For Nginx go to nginx/sites, for Apache2 apache2/sites.
       workspace by default includes some sample files for you to copy app.conf.example, laravel.conf.example and symfony.conf.example.
    - change the default names *.conf:
       You can rename the config files, project folders and domains as you like, just make sure the root in the config files, is pointing to the correct project folder name.
    - Add the domains to the hosts files.
       127.0.0.1  project-1.test
       127.0.0.1  project-2.test    ...
       If you use Chrome 63 or above for development, don’t use .dev. Why?. Instead use .localhost, .invalid, .test, or .example.
       
Run        
- docker-compose up -d nginx mysql phpmyadmin workspace

- docker-compose exec workspace bash 

        (Enter the Workspace container, to execute commands like (Artisan, Composer)
        Note: You can add --user=arn to have files created as your host’s user. Example:
        docker-compose exec --user=arn workspace bash

- Update your project configuration to use the database host
  Open your PHP project’s .env file or whichever configuration file you are reading from, and set the database host DB_HOST to mysql:
  DB_HOST=mysql
  
