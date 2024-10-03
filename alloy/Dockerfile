FROM node:22

RUN apt-get update

RUN apt-get install -y gnupg2

RUN apt-get install -y wget

RUN apt-get install -y supervisor

RUN mkdir -p /etc/apt/keyrings/

RUN wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | tee /etc/apt/keyrings/grafana.gpg > /dev/null

RUN echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | tee /etc/apt/sources.list.d/grafana.list

RUN apt-get update

RUN apt-get install -y alloy

RUN alloy --version

RUN apt-get clean

RUN rm -i /etc/apt/sources.list.d/grafana.list

COPY config.alloy /etc/alloy/config.alloy

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 12345

CMD ["supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
