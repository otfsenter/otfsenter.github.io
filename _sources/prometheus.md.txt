# prometheus

没有看的文章

https://www.cnblogs.com/jiujuan/p/13262380.html

## install

download

https://github.com/prometheus/prometheus/tags

```bash
wget prometheus tar file
tar xvf prometheus-2.14.0.linux-amd64.tar.gz
mv prometheus-2.14.0.linux-amd64 /usr/local/bin/prometheus
```

配置systemd管理

```bash
cat > /usr/lib/systemd/system/prometheus.service << EOF
[Unit]
Description=https://prometheus.io

[Service]
Restart=on-failure
ExecStart=/usr/local/bin/prometheus/prometheus --config.file=/usr/local/bin/prometheus/prometheus.yml

[Install]
WantedBy=multi-user.target
EOF
```

服务管理

```bash
systemctl daemon-reload
systemctl start prometheus
systemctl enable prometheus
```

visit website

http://ip:9090
