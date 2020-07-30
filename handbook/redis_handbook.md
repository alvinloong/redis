# [Documentation](https://redis.io/documentation)

## [Quick Start](https://redis.io/topics/quickstart)

### Installing Redis

install dependent packages

```
sudo apt install build-essential
sudo apt install pkg-config
sudo apt install tcl
```

install redis

```
mkdir -p ~/soft/redis/
tar -zxvf redis-6.0.6.tar.gz -C ~/soft/redis/
cd ~/soft/redis/redis-6.0.6
#make distclean
make
make test
#make distclean
sudo make install
```

### Starting Redis

```
redis-server
redis-server /etc/redis.conf
```

### Check if Redis is working

```
netstat -tnpl
redis-cli ping
redis-cli
```

```
ping
set mykey somevalue
get mykey
```

### Redis persistence

```
redis-cli save
redis-cli shutdown
```

### Installing Redis more properly

```
sudo mkdir /etc/redis
sudo mkdir /var/redis
cd ~/soft/redis/redis-6.0.6
```

Make sure to modify **REDISPORT** accordingly to the port you are using. Both the pid file path and the configuration file name depend on the port number.

```
sudo cp utils/redis_init_script /etc/init.d/redis_6379
sudo vi /etc/init.d/redis_6379
sudo cp redis.conf /etc/redis/6379.conf
sudo mkdir /var/redis/6379
sudo update-rc.d redis_6379 defaults
sudo /etc/init.d/redis_6379 start
```

```
sudo vi /etc/redis/6379.conf
```

```
daemonize yes
pidfile /var/run/redis_6379.pid
port 6379
loglevel notice
logfile "/var/log/redis_6379.log"
dir /var/redis/6379
```

## Administration

### [Configuration](https://redis.io/topics/config)

### [Replication](https://redis.io/topics/replication)

```
sudo cp utils/redis_init_script /etc/init.d/redis_6389
sudo vi /etc/init.d/redis_6389
sudo cp redis.conf /etc/redis/6389.conf
sudo mkdir /var/redis/6389
sudo update-rc.d redis_6389 defaults
```

```
sudo vi /etc/redis/6389.conf
```

```
daemonize yes
pidfile /var/run/redis_6389.pid
port 6389
loglevel notice
logfile "/var/log/redis_6389.log"
dir /var/redis/6389
replicaof localhost 6379
```

```
sudo /etc/init.d/redis_6389 start
```

```
redis-cli -p 6389
info replication
```

```
slaveof no one
slaveof localhost 6379
```

