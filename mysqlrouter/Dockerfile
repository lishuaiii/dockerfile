FROM ubuntu
RUN apt update \
    && apt install mysql-router -y \
    && mkdir /etc/mysqlrouter \
    && echo "[routing:basic_failover]" >> /etc/mysqlrouter/mysqlrouter.conf \
    && echo "bind_address=0.0.0.0" >> /etc/mysqlrouter/mysqlrouter.conf \
    && echo "bind_port=3306" >> /etc/mysqlrouter/mysqlrouter.conf \
    && echo "mode=read-write" >> /etc/mysqlrouter/mysqlrouter.conf \
    && echo "" >> /etc/mysqlrouter/mysqlrouter.conf \
    && echo "destinations=appstack.mysql.rds.aliyuncs.com:3306" >> /etc/mysqlrouter/mysqlrouter.conf \
    && echo "[keepalive]" >> /etc/mysqlrouter/mysqlrouter.conf \
    && echo "interval=60" >> /etc/mysqlrouter/mysqlrouter.conf
