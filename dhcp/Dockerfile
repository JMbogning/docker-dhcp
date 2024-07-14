# Utilisez l'image de base officielle Ubuntu
FROM debian:bullseye

# Installez ISC DHCP Server
RUN apt-get update && \
    apt-get install -y isc-dhcp-server iproute2 iputils-ping && \
    rm -rf /var/lib/apt/lists/*

# Créer le fichier de baux manquant pour éviter l'erreur au démarrage
RUN mkdir -p /var/lib/dhcp && \
    touch /var/lib/dhcp/dhcpd.leases

# Copiez les configurations DHCP dans le conteneur
COPY configs/ /etc/dhcp/

# Exposez le port DHCP standard
EXPOSE 67/udp

# Configurez le point d'entrée pour démarrer le serveur DHCP
ENTRYPOINT ["/usr/sbin/dhcpd"]
CMD ["-d", "-f", "-cf", "/etc/dhcp/dhcpd.conf", "-lf", "/var/lib/dhcp/dhcpd.leases"]
