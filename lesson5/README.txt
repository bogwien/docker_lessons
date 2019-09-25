Build image locally:
docker build -t extsoft/allure-docker-example .

Docker run:
1. docker run -t -i -p 80:80 extsoft/allure-docker-example
2. Open Allure report on your host machine: http://localhost/#/



docker build -t jat:h5 .
docker run -it -p 8080:80 jat:h5
