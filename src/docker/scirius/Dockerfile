FROM debian:latest

ENV VERSION 1.1.3
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y wget python-pip python-dev git gcc
ADD stamus-packages.list /etc/apt/sources.list.d/
WORKDIR /tmp/
RUN wget -O stamus.key -q http://packages.stamus-networks.com/packages.stamus-networks.com.gpg.key
RUN apt-key add stamus.key
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y suricata
RUN wget https://github.com/StamusNetworks/scirius/archive/scirius-${VERSION}.tar.gz
RUN mkdir -p /opt/selks/sciriusdata
WORKDIR /opt/selks
RUN tar zxf /tmp/scirius-${VERSION}.tar.gz
RUN ln -sf /opt/selks/scirius-scirius-${VERSION} /opt/selks/scirius
WORKDIR /opt/selks/scirius
RUN pip install -r requirements.txt
RUN ln -s /etc/scirius/local_settings.py /opt/selks/scirius/scirius/
ADD django/scirius.json /opt/selks/scirius/
ADD django/scirius.sh /opt/selks/bin/

ENTRYPOINT ["/opt/selks/bin/scirius.sh"]
