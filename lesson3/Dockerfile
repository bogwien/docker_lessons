FROM python:3.6

LABEL author="Bohdan Hvozd"
LABEL version=1

WORKDIR /usr/share/src
VOLUME /usr/share/src

EXPOSE 8080/tcp

COPY entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh

ENTRYPOINT ["entrypoint.sh"]
