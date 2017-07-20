# michalsindler/php/pdo_sqlsrv

Files for building docker image with working PDO for Microsoft SQL server.

## Installation

1. Pull this sources and go to folder with sources on your disk
2. Install Docker ([https://docs.docker.com/engine/installation/](https://docs.docker.com/engine/installation/))
3. Install Docker Compose ([https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/))
4. Build image `sudo docker-compose build`
5. Run container `sudo docker-compose up`

## Usage

Every run must fill up environment variables for database connection:

DB_DRIVER - pdo driver (default "pdo_sqlsqv")

DB_HOST - hostname or ip address (default "")

DB_PORT - opened database port (default "1433")

DB_NAME - database name (default "")

DB_USER - username (default "")

DB_PASSWORD - password (default "")

### Running web server:

`sudo docker run -d -v $PWD:/myApp:rw -v $PWD:/var/www/html -p 8080:80 -e DB_HOST="<your db host>" -e DB_NAME="<your db name>" -e DB_USER="<your db user>" -e DB_PASSWORD="<your db password>" michalsindler/php/pdosqlsrv:php7.0 /usr/sbin/apache2ctl -D FOREGROUND`

Server is accessible on `http://localhost:8080`

### Check, if PDO SQLSRV is installed:
Run webserver (see above).
Go to URL: `http://localhost:8080/tools/info.php`
Then scroll down to "PDO" section and you should see tables:

**PDO**
|PDO support	                    |enabled |
|-----------------------------------|--------|
|PDO drivers	                    |sqlsrv  |

**pdo_sqlsrv**

|pdo_sqlsrv support                 |enabled |
|-----------------------------------|--------|
|ExtensionVer	                    |4.3.0   |

## Contributing

1. Fork it!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request :D

## History

It' short. Very short. It's like ... now.

## Credits

Lot's of good people of internet.

## License

Live long and dock your projects.