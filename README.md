# spark-instance

### check if docker is installed

```
docker version
systemctl status docker
```

### installing docker
```

sudo apt-get update                                

sudo apt-get install \                             
    apt-transport-https \                          
    ca-certificates \                                 
    curl \
    gnupg \
    lsb-release



curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg



echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null



sudo apt-get update

 sudo apt-get install docker-ce docker-ce-cli containerd.io
```

### creating a base container for spark then we'll commit image of it and use that image to install spark container

```
docker run --it --name spark_base ubuntu bash
```
### installing packages that support spark

```
apt update
apt install git scala wget default-jdk vim python3 net-tools -y
```

### checking versions

```
java -version ; javac -version ; scala -version ; git --version

```

### downloading spark
```
wget  https://downloads.apache.org/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2.tgz
```

### extracting

```
tar xvzf spark-3.1.2-bin-hadoop3.2.tgz
```

### remove setup and moving it
```
rm  spark-3.1.2-bin-hadoop3.2.tgz 
   mv  spark-3.1.2-bin-hadoop3.2/  /opt/spark
  ```
  
### setting path in /root/.bashrc in last

```
export SPARK_HOME=/opt/spark
export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin
export PYSPARK_PYTHON=/usr/bin/python3
```

### commiting image using root user
```
docker commit -m "spark base image" spark_base spark:v1
```
### pushing it on docker hub you guys can pull it

```
docker pull xpron/spark:v1
```

### creating our first container using this image

```
docker run -itd --name spark_master --hostname SparkM --network myhadoop_br --ip 192.168.200.230 --restart always xpron/spark:v1
```

