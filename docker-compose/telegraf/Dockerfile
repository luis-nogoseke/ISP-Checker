FROM telegraf:1.21.3

ARG ARCH

LABEL project="ISP-Checker"
LABEL component="telegraf"

COPY ./bin/entrypoint.sh /entrypoint.sh

RUN apt-get update && apt-get install -y --no-install-recommends \
    mtr \
    python3-pip && \
    rm -rf /var/lib/apt/lists/* && \
    usermod -G video telegraf

RUN pip3 install speedtest-cli

RUN ln -s /usr/bin/python3 /usr/bin/python
RUN ln -s /usr/local/lib/python3.9/dist-packages/speedtest.py /usr/bin/speedtest-cli
RUN chmod +x /usr/bin/speedtest-cli

EXPOSE 8125/udp 8092/udp 8094

ENTRYPOINT ["/entrypoint.sh"]

CMD ["telegraf"]
