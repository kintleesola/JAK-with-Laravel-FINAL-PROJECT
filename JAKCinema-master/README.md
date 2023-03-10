# JAKcinema

A movie management application using a REST API built with Laravel. Display with movie Choices and seats in a Cinema to select from in order to purchase tickets

![Screenshot TMM](extra/media/ticket.png)
![Screenshot TMM](extra/media/tmm.png)
![Screenshot TMM](extra/media/tmm-browse.png)
![Screenshot TMM](extra/media/tmm-add.png)
![Screenshot TMM](extra/media/sticket.png)
![Screenshot TMM](extra/media/socticket.png)
![Screenshot TMM](extra/media/twticket.png)

## Dependencies

* [docker](https://docs.docker.com/engine/installation/)
* [docker-compose](https://docs.docker.com/compose/install/)

## Installation

For development, nginx expects the domain `tmm.8ed.local`, add that to `/etc/hosts/`:

```
sudo echo "127.0.0.1 tmm.8ed.local" >> /etc/hosts
```

An `.env` file is also required to set up environment variables, laravel should automatically copy the `.env.example` file to `.env` if `.env` is not found.

Generate oauth keys and install vendor packages:

```
composer install
php artisan passport:install
```

Optionally, you can register an API key with [Guidebox](https://api.guidebox.com/apidocs) for additional data about your movies.

## Usage

The stack runs in docker, which can be started with:

```
docker-compose up
```

This setups a database, and an nginx + php5-fpm container to serve the Laravel project located in `src`. 

Visit [http://jakc.8ed.local](http://jakc.8ed.local) in your web browser and create a new user.

Default login is [test@test.com / test123](https://github.com/kintleesola/JAK-Cinema-Tickets)

## Deployment

Create a `docker-compose.prod.yml` file based on `docker-compose.override.yml` and edit your `.env` to match production.

Bring it up with:

```
docker-compose -f docker-compose.yml -f docker-compose.prod.yml up
```

### Automated (optional)

Take a look at the `extra/git/hooks/post-receive` hook to setup automated deployments when you push to a special remote.

## Developer Notes

```bash
# dockerized composer
alias composer='docker run -it --rm --net=host -v $HOME:$HOME -e COMPOSER_HOME="$HOME/.composer" -u $UID -w `pwd` composer/composer:master-php5-alpine'
```

The `src` base was generated with composer:

```bash
cd src
composer create-project --prefer-dist laravel/laravel .
```

Permissions on directories:

```
chown -R $USER:$USER .
chmod -R o+w bootstrap/cache
chmod -R o+w storage
```

If you have any issues starting up, try the following:

```
# clear cache and compiled classes
php artisan cache:clear
php artisan clear-compiled

# regen the autoload file
composer dump-autoload
```

## License

Copyright (c) 2023 JAK Cinema kintleesola and JoshuaDelvalle14.

If you discover a security vulnerability within Laravel, please send an e-mail to Kint Lee Sola via [kintlee.sola@unc.edu.ph]. All security vulnerabilities will be promptly addressed.
