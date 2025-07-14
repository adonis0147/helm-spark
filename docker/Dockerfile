FROM alpine:latest AS builder

WORKDIR /tmp

COPY spark-*.tgz .
RUN tar -zxvf spark-*.tgz -C /

COPY jdk-* .
RUN tar -zxvf jdk-*.tar.gz -C /

FROM ubuntu:latest

RUN mkdir -p /home/spark

WORKDIR /home/spark

COPY --from=builder spark-* /home/spark/spark-current
COPY --from=builder /jdk-* /opt/java
COPY ./*.jar /home/spark/spark-current/jars/

ENV PATH="/opt/java/bin:/home/spark/spark-current/bin:${PATH}"
ENV JAVA_HOME='/opt/java'
ENV SPARK_HOME='/home/spark/spark-current'
ENV SPARK_LOG_DIR='/home/spark/cluster-data/spark/logs'
ENV SPARK_PID_DIR='/home/spark/cluster-data/spark/pids'

CMD ["/usr/bin/bash"]
