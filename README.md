# JmeterDocker

docker network create forJmeter

docker run -dit --name master50 --network=forJmeter -e Xms=256m -e Xmx=512m -e MaxMetaspaceSize=512m -e DATA_FILE=/opt/Sharedvolume/slm1 -v /opt/Sharedvolume:/opt/Sharedvolume smahaboob/master /bin/bash



docker run -dit --name slave51 --network=forJmeter -e Xms=256m -e Xmx=512m -e MaxMetaspaceSize=512m -e DATA_FILE=/opt/Sharedvolume/slm1 -v /opt/Sharedvolume:/opt/Sharedvolume smahaboob/slave /bin/bash



docker run -dit --name slave52 --network=forJmeter -e Xms=256m -e Xmx=512m -e MaxMetaspaceSize=512m -e DATA_FILE=/opt/Sharedvolume/slm1 -v /opt/Sharedvolume:/opt/Sharedvolume smahaboob/slave /bin/bash


docker exec -ti master50 bash

cd /opt/apache-jmeter-5.1.1/bin/


./jmeter -n -t /opt/Sharedvolume/slm1/Login_TEST3.jmx -Dserver.rmi.ssl.disable=true -Dserver.rmi.ssl.keystore.file=rmi_keystore.jks -R slave51,slave52 -l /opt/Sharedvolume/slm1/logfile.jtl
