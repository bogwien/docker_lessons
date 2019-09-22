FROM python:3.6

LABEL author="Bohdan Hvozd"
LABEL version=1

WORKDIR /usr/share/src
COPY src /usr/share/src

VOLUME /usr/share/src/logs

EXPOSE 5000

COPY entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh

ENTRYPOINT ["entrypoint.sh"]
