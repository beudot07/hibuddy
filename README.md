# HiBuddy, say hi to your friends !

HiBuddy provides you a simple way to make bidirectional
videoconferences with your friends.

## Goals

  - Provides a small web application.
  - Easy to install, easy to launch, easy to use.
  - Doesn't keep any user data.
  - Free as in freedom.

## Getting Started

### Requirements

  - Firefox 25 (or later) not tested but supposed to work with Opera or Chrome since 2012
  - `node 0.8.x` note that this version needs a trick for installation on Ubuntu 2012 LTS
  - `npm 1.1.x`

### Install the project

    $ git clone https://github.com/tOkeshu/hibuddy.git
    $ cd hibuddy
    $ npm install

These commands should clone and pull the necessary dependencies.

### Configure Nginx

Here is a sample configuration for nginx:

    # /etc/nginx/sites-available/hibuddy.example.com
    server {
        listen   80;

        root /path/to/hibuddy/public;
        index index.html index.htm;

        server_name hibuddy.example.com;
        server_name_in_redirect off;

        proxy_buffering off;

        location / {
               proxy_pass http://127.0.0.1:7665;
        }
    }
    
Enable your site:

    # ln -s /etc/nginx/sites-available/hibuddy.example.com /etc/nginx/sites-enabled/hibuddy.example.com
    # /etc/init.d/nginx reload  
    
Here is a sample configuration for apache2:

VirtualHost *:80>
        ServerName hibuddy.example.com

        ProxyPass / http://localhost:7665/
        ProxyPassReverse / http://localhost:7665/
        ProxyPreserveHost On
</VirtualHost>

Enable your site :
    # a2ensite hibuddy.example.com
    # service apache2 reload

### Start the server

    $ cd hibuddy
    $ npm start # starts the server on port 7665

Then open a browser to http://hibuddy.example.com (where `hibuddy.example.com` is your domain).

If you just want to test the application on you machine, just edit your
`/etc/hosts`:

    # /etc/hosts
    127.0.1.1	hibuddy.example.com

### Production

For a more concrete deployment, we recommand you to use `forever`:

    # npm install -g forever # install forever system wide
    $ cd hibuddy
    $ forever -o logs/stdout.log -e logs/stderr.log start bin/hibuddy
    $ forever stop bin/hibuddy

See the [forever documentation](https://github.com/nodejitsu/forever)
for more information.

## License

HiBuddy is released under the terms of the
[GNU Affero General Public License v3](http://www.gnu.org/licenses/agpl-3.0.html)
or later.

