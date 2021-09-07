# PHP FAX[DEV]
PHP application to send faxes.

## Content

 - service.php : a PHP script that reads an IMAP mailbox and combine all PDF(x) and send them back combined.
 - service : a BASH script that executes service.php in a loop.
 - init : a SHELL script to be placed in /etc/init.d/ to launch the service script in the background.
 - settings.json : A JSON file that stores all scripts settings

## Install
### To Install

#### Install Requirements

```BASH
sudo apt-get install -y apache2 php php-common php-imap php-imagick ghostscript imagemagick imagemagick-common
sudo nano /etc/ImageMagick-6/policy.xml
```

Replace `<policy domain="coder" rights="none" pattern="PDF" />` to `<!-- <policy domain="coder" rights="none" pattern="PDF" /> -->`

#### Setup Service
```BASH
cd /opt/
sudo git clone https://github.com/LouisOuellet/php-pdf.git
sudo ln -s /opt/php-pdf/init /etc/init.d/php-pdf
sudo systemctl daemon-reload
sudo systemctl enable php-pdf
sudo systemctl start php-pdf
```

## service.php
### Requirements

 - Linux
 - Apache2
 - php
 - php-common
 - php-imap
 - php-imagick
 - ghostscript
 - imagegick
 - imagegick-common

### Execute

```BASH
php service.php
```

## service
### Execute

```BASH
./service
```

## init
### Configure service

```BASH
sudo ln -s /opt/php-pdf/init /etc/init.d/php-pdf
sudo systemctl daemon-reload
sudo systemctl enable php-pdf
sudo systemctl start php-pdf
```

## settings.json
### Create settings
To create the file simply use your favorite editor and copy/paste the example.

```BASH
nano settings.json
```

 - smtp[MANDATORY]: contains the SMTP configurations
 - imap[MANDATORY]: contains the IMAP configurations
 - destination: contains a static destination email for the service
 - pdf: contains the PDF configurations, currently only support compression settings

### Example
```JSON
{
    "destination": "default@domain.com",
    "smtp":{
        "host": "smtp.domain.com",
        "port": "465",
        "encryption": "SSL",
        "username": "username@domain.com",
        "password": "password"
    },
    "imap":{
        "host": "imap.domain.com",
        "port": "993",
        "encryption": "SSL",
        "isSelfSigned": true,
        "username": "username@domain.com",
        "password": "password"
    },
    "pdf":{
        "scale": 80,
        "maxFileSize": 10000000,
        "compression": false
    }
}
```
