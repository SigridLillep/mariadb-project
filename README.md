## Install Ubuntu WSL on windows 11
https://www.youtube.com/watch?v=zZf4YH4WiZo

## Süsteemi uuendamine
```bash
sudo apt update 
sudo apt upgrade -y
```

## MariaDB paigaldamine
sudo apt install mariadb-server -y
mariadb --version
sudo service mariadb start
sudo service mariadb status

## MariaDB turvaseadistus
sudo mqsql_secure_installation

switch to unix_socket authentication - Y
change the root password - n
remove anonymus users - Y
disallow root login remotely - Y
remove test databases and access to it - Y
reload privilege tables now - Y

## Võrguturbe konfiguratsioon
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
bind-address oli juba 127.0.0.1
lisasin juurde:
local-infile = 0
skip-name-resolve
skip-networking = 1

## MariaDB taaskäivitamine ja kontroll
sudo service mariadb restart
sudo ss -tlnp | grep 3306 - ei anna tulemust, sest konfi on lisatud bind-address 127.0.0.1 ja skip-networking = 1, st et mariadb ei kuula TCP/IP võrku ehk port 3360 ei avatagi. Andmebaas on kasutatav ainult lokaalselt Unix socketi kaudu.
