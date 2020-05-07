# JmeterDocker

docker network create forJmeter

docker run -dit --name master50 --network=forJmeter -e Xms=256m -e Xmx=512m -e MaxMetaspaceSize=512m -e DATA_FILE=/opt/Sharedvolume/slm1 -v /opt/Sharedvolume:/opt/Sharedvolume smahaboob/master /bin/bash



docker run -dit --name slave51 --network=forJmeter -e Xms=256m -e Xmx=512m -e MaxMetaspaceSize=512m -e DATA_FILE=/opt/Sharedvolume/slm1 -v /opt/Sharedvolume:/opt/Sharedvolume smahaboob/slave /bin/bash



docker run -dit --name slave52 --network=forJmeter -e Xms=256m -e Xmx=512m -e MaxMetaspaceSize=512m -e DATA_FILE=/opt/Sharedvolume/slm1 -v /opt/Sharedvolume:/opt/Sharedvolume smahaboob/slave /bin/bash


docker exec -ti master50 bash

cd /opt/apache-jmeter-5.1.1/bin/


./jmeter -n -t /opt/Sharedvolume/slm1/Login_TEST3.jmx -Dserver.rmi.ssl.disable=true -Dserver.rmi.ssl.keystore.file=rmi_keystore.jks -R slave51,slave52 -l /opt/Sharedvolume/slm1/logfile.jtl


========================

docker network create forJmeter

docker run -dit --name master50 --network=forJmeter -e Xms=256m -e Xmx=512m -e MaxMetaspaceSize=512m -eDATA_FILE=/opt/Sharedvolume/slm1 -v /opt/Sharedvolume:/opt/Sharedvolume smahaboob/master /bin/bash

docker run -dit --name slave51 --network=forJmeter -e Xms=256m -e Xmx=512m -e MaxMetaspaceSize=512m -e DATA_FILE=/opt/Sharedvolume/slm1 -v /opt/Sharedvolume:/opt/Sharedvolume smahaboob/slave /bin/bash

docker run -dit --name slave52 --network=forJmeter -e Xms=256m -e Xmx=512m -e MaxMetaspaceSize=512m -e DATA_FILE=/opt/Sharedvolume/slm1 -v /opt/Sharedvolume:/opt/Sharedvolume smahaboob/slave /bin/bash

docker exec -ti master50 bash

cd /opt/apache-jmeter-5.1.1/bin/

./jmeter -n -t /opt/Sharedvolume/slm1/Login_TEST3.jmx -Dserver.rmi.ssl.disable=true -Dserver.rmi.ssl.keystore.file=rmi_keystore.jks -R slave51,slave52 -l /opt/Sharedvolume/slm1/logfile.jtl

sudo docker run --rm  -t --name slm16master --network=slm16 -e Xms=256m -e Xmx=512m -e MaxMetaspaceSize=512m -e DATA_FILE=/opt/Sharedvolume/slm16 -v /opt/Sharedvolume:/opt/Sharedvolume smahaboob/master /opt/apache-jmeter-5.1.1/bin/jmeter -n -t /opt/Sharedvolume/JmeterScripts/Login_TEST3.jmx -Dserver.rmi.ssl.disable=true -Dserver.rmi.ssl.keystore.file=rmi_keystore.jks  -l /opt/Sharedvolume/slm16/logfile.jtl -e -o /opt/Sharedvolume/HTML_Reports/SLM16/HTML

echo "Deleting all master and slave containers after test execution"
echo "============================================="
sudo docker rm -f slm16master slm16slave1 slm16slave2
echo "Deleting network after test execution"
echo "============================================="
sudo docker network rm slm16
sudo cp /opt/Sharedvolume/slm16/logfile.jtl /opt/Sharedvolume/slm16/logfile_$(date +%F-%H:%M).jtl
sudo mv /opt/Sharedvolume/HTML_Reports/SLM16/HTML /opt/Sharedvolume/HTML_Reports/SLM16/HTML_$(date +%F-%H:%M)
sudo mkdir /opt/Sharedvolume/HTML_Reports/SLM16/HTML



sudo docker network create slm1

sudo docker run -dit --name slm1 --network=slm1 -e Xms=256m -e Xmx=512m -e MaxMetaspaceSize=512m -e DATA_FILE=/Users/sshareef/SLM1 -e ENV_VAR=SLM1 -v /Users/sshareef/SLM1:/opt/ octoperf/jmeter-standard /bin/bash

sudo docker run -dit --name slm18slave2 --network=slm18 -e Xms=256m -e Xmx=512m -e MaxMetaspaceSize=512m -e DATA_FILE=/opt/Sharedvolume/slm18 -e ENV_VAR=SLM18 -v /opt/Sharedvolume:/opt/Sharedvolume smahaboob/slave /bin/bash

sudo docker run --rm  -t --name slm18master --network=slm18 -e Xms=256m -e Xmx=512m -e MaxMetaspaceSize=512m -e DATA_FILE=/opt/Sharedvolume/slm18 -e ENV_VAR=SLM18 -v /opt/Sharedvolume:/opt/Sharedvolume smahaboob/master /opt/apache-jmeter-5.1.1/bin/jmeter -n -t /opt/Sharedvolume/JmeterScripts/Login_TEST3.jmx -Dserver.rmi.ssl.disable=true -Dserver.rmi.ssl.keystore.file=rmi_keystore.jks -R slm18slave1,slm18slave2 -l /opt/Sharedvolume/slm18/logfile.jtl




