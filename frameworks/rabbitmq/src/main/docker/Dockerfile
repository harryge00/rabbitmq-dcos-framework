FROM rabbitmq:3.7.17-management

RUN apt-get update; \
	apt-get install --yes iputils-ping; \
	rm -rf /var/lib/apt/lists/*;
COPY docker-entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-entrypoint.sh