This example shows how separate containers can interact over Docker host native network.

In this case, host and cotnainers are on same network "host" which is actually the network of the host machine.

This doesn't need any port forwarding between host and cotnainers.

# go to these individual dirs and run:

cd redis

docker-compose up --build

# get the ip of the host 

ifconfig

You can choose any of the local networks in general.

Or, even if you use the name of redis container in flask app, it will work.

# put local IP in flask code file app.py

cd ../flask

vi app.py

#put/replace with:

cache = redis.Redis(host='172.21.0.3', port=6379)

or

cache = redis.Redis(host='redis_host', port=6379)

# start flask app container

docker-compose up --build

docker-compose ps

#Here, curl with container port because everything is on same network.

curl http://localhost:5000

It should work.

