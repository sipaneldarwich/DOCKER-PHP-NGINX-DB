# Containers
> 👍 info
>
> change docker-compose.yml name to your project name

  * php + nginx + adminer + mysql
  * nginx: localhost:80
    * nginx is looking for **../app/public/index.php**
  * adminer: localhost:8080
  * mysql: localhost:3306
    * root:root
    * user:devpass
  * commands
    * up
      * `docker composer up -d`
      * `docker-compose -f ./docker/docker-compose.yml up -d`
    * bash
      * php
        * `docker compose exec php bash`
      * nginx
        * `docker compose exec nginx bash`
---
# Symfony
## install Symfony
  * run this commands or add them to docker-compose.yml
    ```bash
    # Install Symfony
    RUN curl -sS https://get.symfony.com/cli/installer | bash
    # Make "Symfony" command available globally
    RUN mv /root/.symfony5/bin/symfony /usr/local/bin/symfony
    ```
## create a new Symfony project
  * go inside php container
    * `docker compose exec php bash`
  * configure Git
    ```bash
    git config --global --add safe.directory /var/www
    git config --global user.email "you@example.com"
    git config --global user.name "Your Name"
    ```
  * create Symfony Project
    * in same folder
      * `symfony new . --webapp`
    * in new folder
      * `symfony new projectName --webapp`

## Connect Symfony to React
* install npm
  * `apt install npm`
* install encore , will add assets & webpack.config.js
  * `composer require encore`
* uncomment this line in webpack.config.js
  * `.enableReactPreset()`
* overwrite symfony main page
  * create controller and name it `indexController`
    * `bin/console make:controller`
    * open templates base.html.twig
      * include this for css in Header
        ```twig
                {% block stylesheets %}
                    {{ encore_entry_link_tags('app') }}
                {% endblock %}
          ```
      * include this for js in Header
        ```twig
            {% block javascripts %}
                {{ encore_entry_script_tags('app') }}
            {% endblock %}
          ```
* start npm
  * `npm install`
  * `npm run watch`
  * if npm run dev fails : https://stackoverflow.com/questions/77684268/bootstrap-cannot-find-symfony-stimulus-bundle
