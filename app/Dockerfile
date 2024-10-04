FROM amd64/ubuntu

# Install Basics
RUN apt-get update
RUN apt-get install -y curl
RUN apt-get install -y gnupg2
RUN apt-get install -y wget
RUN apt-get install -y supervisor

RUN curl -fsSL https://deb.nodesource.com/setup_22.x -o nodesource_setup.sh
RUN bash nodesource_setup.sh
RUN apt-get install -y nodejs

# Install Alloy
RUN mkdir -p /etc/apt/keyrings/
RUN wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | tee /etc/apt/keyrings/grafana.gpg > /dev/null
RUN echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | tee /etc/apt/sources.list.d/grafana.list
RUN apt-get update
RUN apt-get install -y alloy
RUN apt-get clean
RUN rm -i /etc/apt/sources.list.d/grafana.list

# Install Beyla
RUN curl -L -o beyla.tar.gz https://github.com/grafana/beyla/releases/download/v1.8.4/beyla-linux-amd64-v1.8.4.tar.gz 
RUN tar -xzf beyla.tar.gz 
RUN mv beyla /usr/local/bin/ 
RUN rm beyla.tar.gz

# Run Node
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
RUN mkdir -p /etc/alloy
RUN mkdir -p /etc/beyla
COPY config.alloy /etc/alloy/config.alloy
COPY config.yaml /etc/beyla/config.yaml
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Execute
EXPOSE 8000
EXPOSE 8001
CMD ["supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
