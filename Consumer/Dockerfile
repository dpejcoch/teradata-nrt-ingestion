FROM fedora:34

#Update system
RUN dnf -y install python3-devel findutils libstdc++
RUN dnf -y update python3-setuptools python3-pip

#Install Teradata python package
RUN pip3 install --no-cache-dir \
	teradatasql

#Install Teradata Tools & Utilities
ADD Consumer/TeradataToolsAndUtilitiesBase__linux_*.tar /tmp/
#COPY Consumer/load_sensor_data.tpt /tmp/
COPY Consumer/libkafkaaxsmod.so /opt/teradata/client/17.20/lib64/
RUN cd tmp; find . -name '*.tar.gz' -exec tar zxvf {} --strip=1 \;
RUN /tmp/TeradataToolsAndUtilitiesBase/Linux/x8664/signing/importkey.sh

#Install TPT (manual, not in the above repo)
RUN rpm -ivh /tmp/TeradataToolsAndUtilitiesBase/Linux/x8664/signing/ttupublickey*.rpm
RUN rpm -ivh /tmp/TeradataToolsAndUtilitiesBase/Linux/x8664/tdicu*.rpm
RUN rpm -ivh /tmp/TeradataToolsAndUtilitiesBase/Linux/x8664/cliv2*.rpm
RUN rpm -ivh /tmp/TeradataToolsAndUtilitiesBase/Linux/x8664/tdodbc*.rpm
RUN rpm -ivh /tmp/TeradataToolsAndUtilitiesBase/Linux/x8664/tptbase*.rpm

RUN mkdir /tmp/jobs

#Add entry point - example
ENTRYPOINT ["tail", "-f", "/dev/null"]

