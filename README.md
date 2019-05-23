# Tanzanie-Data-Viz

## Subject

You can find the data [HERE](https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/).

Before importing the data in elasticsearch : 
* You have to remove the first line
* You have to add a column after status group. This column contains a numeric value representing the status.

## HELP

Here some usefull command : 

* run elasticsearch, kabana, and logstash with docker : 
```
docker run -d -p 9200:9200 -p 9300:9300 --name elastic \
                --net=host\
                -e "discovery.type=single-node" \
                -e "XPACK_SECURITY_ENABLED=false" \
                -e "XPACK_REPORTING_ENABLED=false" \
                -e "XPACK_MONITORING_ENABLED=false" \
                docker.elastic.co/elasticsearch/elasticsearch:6.7.1

sudo docker run --name kibana -p 5601:5601 -d \
                --net=host \
                -e "ELASTICSEARCH_URL=http://localhost:9200" \
                docker.elastic.co/kibana/kibana:6.7.1

docker run --name logstash \
       --net=host\
        -v $PWD/data:/usr/tmp \
        -v $PWD/logstash_confs/:/usr/share/logstash/pipeline/ \
        -e "ELASTIC_HOST=localhost:9200" \
        -e "XPACK_SECURITY_ENABLED=false" \
        -e "XPACK_REPORTING_ENABLED=false" \
        -e "XPACK_MONITORING_ENABLED=false" \
        docker.elastic.co/logstash/logstash:6.7.1
```

* Run elastic and kibana in my own conf :

```
sudo /etc/init.d/elasticsearch start
sudo /etc/init.d/kibana start
```

* Run logstash in my own conf : 

```
sudo /opt/logstash-6.7.1/bin/logstash -f pipeline/logstash.conf
```