Check you image:
- run commands:
-- `docker network create --driver=bridge lesson3`
-- `docker run -itd -v "$(pwd)/redis":/data -p 6379:6379 --name redis --rm --net=lesson3 redis redis-server --appendonly yes`
-- `docker build -t bogwien/hits:h3 .`
-- `docker run -it -p 8080:5000 --rm --net=lesson3 --mount type=bind,source="$(pwd)/src",target="/usr/share/src" bogwien/hits:h3`
-- ctrl+c to exit

- tests: run container and then run tests:
-- `docker build -t bogwien/hits_tests:h3 -f DockerfileTests .`
-- `docker run --rm --net=host bogwien/hits_tests:h3 --url http://localhost:8080`

- open 'http://localhost:8080' in your browser

