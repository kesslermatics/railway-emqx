FROM docker.io/library/emqx:5

# Generate self-signed certificate for TLS on port 8883
RUN mkdir -p /opt/emqx/etc/certs && \
    openssl req -x509 -nodes -days 3650 -newkey rsa:2048 \
    -keyout /opt/emqx/etc/certs/key.pem \
    -out /opt/emqx/etc/certs/cert.pem \
    -subj "/C=DE/ST=Bavaria/L=Markt-Nordheim/O=Aquaware/CN=*.railway.app" && \
    cp /opt/emqx/etc/certs/cert.pem /opt/emqx/etc/certs/cacert.pem && \
    chmod 644 /opt/emqx/etc/certs/*.pem && \
    chown -R emqx:emqx /opt/emqx/etc/certs

COPY docker-entrypoint.sh /usr/bin/
COPY docker-healthcheck /usr/local/bin/

HEALTHCHECK CMD ["docker-healthcheck"]

ENTRYPOINT ["/usr/bin/docker-entrypoint.sh"]
CMD ["/opt/emqx/bin/emqx", "foreground"]