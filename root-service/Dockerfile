FROM ubuntu:latest
RUN apt update && apt install tor python3 supervisor python3-pip -y && pip3 install flask requests pysocks && echo "HiddenServiceDir /var/lib/tor/" >> /etc/tor/torrc \
    && echo "HiddenServicePort 8000 127.0.0.1:8000" >> /etc/tor/torrc && service tor restart

ADD server.py /root/server.py
ADD keys/* /var/lib/tor/
RUN chown -R debian-tor:debian-tor /var/lib/tor/ && chmod 600 /var/lib/tor/* 
ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf

ENTRYPOINT ["/usr/bin/supervisord"]
