FROM ubuntu
RUN apt update \
    && apt install mysql-router -y \
    && echo "[routing:basic_failover]" >> /etc/mysqlrouter.conf \
    && echo "bind_address=0.0.0.0" >> /etc/mysqlrouter.conf \
    && echo "mode=read-write" >> /etc/mysqlrouter.conf \
    && echo "destinations=appstack.mysql.rds.aliyuncs.com:3306" >> /etc/mysqlrouter.conf \
    && echo "[keepalive]" >> /etc/mysqlrouter.conf \
    && echo "interval=60" >> /etc/mysqlrouter.conf
