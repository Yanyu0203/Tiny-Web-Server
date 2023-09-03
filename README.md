# Tiny-Web-Server

A high concurrency web server for users to sign up, log in, request for images and videos with thread pool, socket, epoll(ET, LT) and Proactor.

Utilized FSM based method to parse HTTP requests, including GET and POST. Used sub function to get a line and parsed the line in main function.

Improved the efficiency of connection requests to MySQL through designing a connection pool.

Applied singleton pattern and block queue to build a synchronous/asynchronous log system to record server status.

Used Webbench for stress testing. Achieved more than 48962 QPS with log closed + LT + ET + Proactor

![image](https://github.com/Yanyu0203/Tiny-Web-Server/assets/132418583/d08d0ff8-1a00-4130-ac9a-67644fe65fed)

If you want to test this web server, please follow instructions below:

1. Please make sure you have ubuntu and build-essential.

2. Install MySQL:

```shell
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install mysql-server
systemctl status mysql.service  //check status
```

3. Build the database:

```sql
create database yourdb;
USE yourdb;
CREATE TABLE user(
	username char(50) NULL,
	passwd char(50) NULL
)ENGINE=InnoDB;
INSERT INTO user(username, passwd) VALUES('name', 'passwd');
```

4. Edit database info in main.cpp

![image](https://github.com/Yanyu0203/Tiny-Web-Server/assets/132418583/4208b5ba-bbbb-406a-99ca-694d00802928)

5. Build and run the server

```shell
sudo ./build.sh
sudo ./server
```

6. Test Pressure

```shell
cd ./test_pressure/webbench-1.5
make clean
make
sudo make install
webbench -c 10500 -t 5 http://localhost:9006/
```

[Sources and Referrence](https://github.com/qinguoyi/TinyWebServer/tree/master)
