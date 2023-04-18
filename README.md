# mongodb-config

## install

1. `sudo apt-get install gnupg`

1. `curl -fsSL https://pgp.mongodb.com/server-6.0.asc | \
sudo gpg -o /usr/share/keyrings/mongodb-server-6.0.gpg \
--dearmor`

1. `echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-6.0.gpg ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list`

1. `sudo apt-get update`

1. `sudo apt-get install -y mongodb-org`

1. `sudo systemctl enable mongod`

1. vm.max_map_count [65530] is too low

   ```cmd
   echo "vm.max_map_count=262144" >> /etc/sysctl.conf
   sudo sysctl -p
   ```

1. `sudo systemctl start mongod`

## Authentication

1. admin

   ```cmd
   use admin
   db.createUser(
   {
   user: "admin",
   pwd: "myNewPassword",
   roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
   }
   )
   ```

1. enable authorization in `/etc/mongod.conf`

   ```conf
   security:
   authorization: "enabled"
   ```

1. `sudo service mongodb restart`

1. create new user

   ```cmd
   use demo

   db.createUser(
   {
   user: "justAUser",
   pwd: "pwd",
   roles: [ { role: "readWrite", db: "demo" } ]
   }
   )
   ```
