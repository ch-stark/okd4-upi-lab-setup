```
curl -o /tmp/keycloak.tgz https://downloads.jboss.org/keycloak/9.0.2/keycloak-9.0.2.tar.gz

cd /usr/local
tar -xzv /tmp/keycloak.tgz
ln -s keycloak-9.0.2 keycloak
group add keycloak
useradd -g keycloak keycloak
chown -R keycloak:keycloak keycloak-9.0.2

sudo cat > /etc/systemd/system/keycloak.service <<EOF

[Unit]
Description=KeyCloak IAM Server
After=network.target

[Service]
Type=idle
User=keycloak
Group=keycloak
ExecStart=/usr/local/keycloak/bin/standalone.sh -b 0.0.0.0
TimeoutStartSec=600
TimeoutStopSec=600

[Install]
WantedBy=multi-user.target
EOF

firewall-cmd --add-port=8080/tcp --permanent
firewall-cmd --reload

systemctl enable keycloak

```