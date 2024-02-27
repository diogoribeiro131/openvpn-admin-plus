FROM debian:bullseye

WORKDIR /opt
EXPOSE 8080

RUN apt-get update && apt-get install -y easy-rsa

# Define a variável de ambiente TERM
ENV TERM xterm

# Cria o diretório /etc/openvpn/easy-rsa/ e copia o arquivo vars
RUN mkdir -p /etc/openvpn/easy-rsa/
COPY easy-rsa/vars /etc/openvpn/easy-rsa/vars

# Torna os arquivos easy-rsa executáveis
RUN chmod 755 /usr/share/easy-rsa/*

# Adiciona os scripts e arquivos de configuração
ADD assets/start.sh /opt/start.sh
ADD assets/generate_ca_and_server_certs.sh /opt/scripts/generate_ca_and_server_certs.sh
ADD assets/vars.template /opt/scripts/
ADD pivpn-tap-web-ui.tar.gz /opt/openvpn-gui-tap/
RUN rm -f /opt/openvpn-gui-tap/data.db
ADD assets/app.conf /opt/openvpn-gui-tap/conf/app.conf

# Define o comando padrão
CMD ["/bin/bash", "/opt/start.sh"]
