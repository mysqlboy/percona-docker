FROM ubuntu:latest

EXPOSE 3000 8000 9001 9090

RUN apt-get -y update && apt-get install -y curl apt-transport-https mysql-server python

# Get grafana and install
RUN echo "deb https://packagecloud.io/grafana/stable/debian/ wheezy main" > /etc/apt/sources.list.d/grafana.list \
	&& curl https://packagecloud.io/gpg.key | apt-key add - \
	&& apt-get -yq update \
	&& apt-get -yq install grafana

RUN mkdir /prometheus && curl https://github.com/prometheus/prometheus/releases/download/0.16.2/prometheus-0.16.2.linux-amd64.tar.gz \
	| tar -xJC /prometheus

# Bind mount config
	# -v ${PWD}/config/grafana.ini:/etc/grafana/grafana.ini
# COPY grafana.ini /etc/grafana/grafana.ini

# Bind mount dashboards
	# -v ${PWD}/grafana-dashboards:/var/lib/grafana/dashboards/
# COPY grafana-dashboards/* /var/lib/grafana/dashboards/
COPY prometheus-datasource.json start.sh /

ENTRYPOINT ["/start.sh"]

CMD ["/start.sh"]
