FROM node:22

RUN apt-get update
RUN apt-get install -y gnupg2
RUN apt-get install -y wget
RUN mkdir -p /etc/apt/keyrings/
RUN wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | tee /etc/apt/keyrings/grafana.gpg > /dev/null
RUN echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | tee /etc/apt/sources.list.d/grafana.list
RUN apt-get update
RUN apt-get install -y alloy
RUN apt-get clean
RUN rm -i /etc/apt/sources.list.d/grafana.list

WORKDIR /usr/src/app

RUN mkdir -p /etc/alloy
COPY config.alloy /etc/alloy/config.alloy
RUN cat /etc/alloy/config.alloy
COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 8000

CMD ["node", "index.js"]
