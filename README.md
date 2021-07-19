# vagrant-dockware-platform
Setup a Shopware 6 dev environment with [vagrant](https://www.vagrantup.com) and [dockware](https://dockware.io)

## Setup instructions:
- Set preferred version of Shopware 6 in [`ansible/vars/all.yml`](/ansible/vars/all.yml)
- Start vagrant box and dockware setup: `vagrant up`
- Log in to vagrant box from your host: `vagrant ssh`
- Log in to docker container from vagrant box: `docker exec -it shopware /bin/bash`
- Run setup script to prepare your dev environment: `cd /var/www && ./setup.sh`
- Edit nameserver in docker container `sudo vi /etc/resolv.conf` set nameserver to `8.8.8.8`
- Access your dev setup in your browser by navigating to http://192.168.35.10/

## Issues:
- chmod error when trying to activate adyen-shopware6 plugin in Shopware admin: edit `vendor/league/flysystem/src/Adapter/Local.php` and comment out line containing `chmod()` call.
