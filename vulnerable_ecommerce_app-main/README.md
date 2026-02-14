Vulnerable_ecommerce_app This vulnerable e-commerce application is built in a Docker environment using Apache, PHP, and MySQL technologies. It is intended solely for educational purposes to practice penetration testing. Do not attempt these techniques on real-world applications without proper consent from the application owners.

Architecture

Follow the below steps to deploy it as docker in your machine.

Tip

We recommend using Kali Linux as your base OS for running these Docker containers, as it comes pre-installed with the essential tools for learning penetration testing!

Steps to Install and enable docker Note

If you don't have docker installted in your machine you can follow this below steps, otherwise skip to Building and running docker containers

Update kali repository #sudo apt-get update

Installing docker #sudo apt-get install -y docker.io

Start and enable docker service #sudo systemctl start docker #sudo systemctl enable docker

Check docker version #docker --version

Steps to run vulnerable ecommerce as docker container After installing docker, now navigate to the cloned directory which is "vulnerable_ecommerce_app" and execute following docker commands to deploy and launch vulnerable ecommerce application

This command build the web container #sudo docker build -t ecommerce_web .

This command build and run the database container #sudo docker run -d --name ecommerce_db -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=vuln_ecommerce mysql:5.7

This command runs the web container and link with database container #sudo docker run -d --name ecommerce_web -p 8090:80 --link ecommerce_db:db -v $(pwd)/app:/var/www/html ecommerce_web

This command initialize the database #sudo docker exec -i ecommerce_db mysql -u root -ppassword vuln_ecommerce < app/db_init.sql

Set auto-restart (Containers automatically restart after poweroff/reboot of kali linux #sudo docker update --restart unless-stopped ecommerce_web #sudo docker update --restart unless-stopped ecommerce_db
