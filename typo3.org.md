# latin1 problem

docker exec -it terdockerminimal_ter-db_1 bash
docker exec -it terdockerminimal_t3o-db_1 bash

mysql -u root -p
uf5c92eCULghtfdEdqH0hsfvnPSuEY7cnPKk5MAz
ALTER DATABASE t3o CHARACTER SET utf8 COLLATE utf8_general_ci;
drop database t3o;
create database t3o CHARACTER SET utf8 COLLATE utf8_general_ci;