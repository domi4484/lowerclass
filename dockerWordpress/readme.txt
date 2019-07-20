Guardare se docker sta andando:
sudo docker info

Listare i containers:
docker container ls

Restartare un container:
docker container restart [OPTIONS] CONTAINER [CONTAINER...]

Far partire docker:
sudo service docker start

Installare docker-compose eventualmente:
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose

La prima volta per scaricare tutto il plunder e farlo partire:
sudo docker-compose up -d

Backuppare il database fuori da docker: (https://pattonwebz.info/100-days-of-code-challenge-week-2/)
sudo docker exec dockerwordpress_db_1 sh -c 'exec mysqldump -u"$MYSQL_USER" -p"$MYSQL_PASSWORD" "$MYSQL_DATABASE"' > wp_database.sql

Backuppare i files fuori da docker:
sudo docker run --rm --volumes-from dockerwordpress_wordpress_1 -v $(pwd)/backup:/backup/ ubuntu tar -cvf /backup/wp_files.tar /var/www/

Restaurare il database
sudo docker cp ./lowerc3_wordpress.sql dockerwordpress_db_1:/ 
sudo docker exec dockerwordpress_db_1 /bin/sh -c 'mysql -u "$MYSQL_USER" -p"$MYSQL_PASSWORD" "$MYSQL_DATABASE" </lowerc3_wordpress.sql'
