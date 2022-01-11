FROM rrrelax/python-redis
WORKDIR /root
RUN curl -O https://dlcdn.apache.org/kafka/3.0.0/kafka_2.13-3.0.0.tgz \
    && tar -zxvf kafka_2.13-3.0.0.tgz \
    && chmod +x /root/kafka_2.13-3.0.0/bin/*.sh
ENV PATH=$PATH:/root/kafka_2.13-3.0.0/bin
CMD /bin/bash