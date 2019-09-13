FROM python:latest

LABEL author="Bohdan Hvozd"
LABEL version=1

WORKDIR /usr/share/src
COPY src /usr/share/src

RUN chmod +x /usr/share/src/app.py
EXPOSE 8080/tcp

RUN pip install flask

ENTRYPOINT ["python", "./app.py"]
