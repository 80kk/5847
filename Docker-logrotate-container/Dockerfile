FROM alpine:3.8

ENV CRON_SCHEDULE='*/5 * * * *' \
    LOGROTATE_SIZE='10M' \
    LOGROTATE_MODE='copytruncate' \
    LOGROTATE_PATTERN1='/var/log/*.log' \
    LOGROTATE_PATTERN2='/var/log/*/*.log' \
    LOGROTATE_ROTATE='5'

RUN apk --no-cache add logrotate tini gettext libintl \
    && mkdir -p /var/log \
    && chmod 775 /var/log \
    && mkdir -p /etc/logrotate.d

COPY logrotate.tpl.conf /logrotate.tpl.conf
COPY entrypoint.sh /usr/local/bin/entrypoint.sh

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]

CMD ["/usr/sbin/crond", "-f", "-L", "/dev/stdout"]
