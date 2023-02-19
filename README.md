# elk-docker-nodocker-sample

![badge4](https://img.shields.io/badge/docker-3.3.1-blue)
![Stars](https://img.shields.io/github/stars/tquangdo/elk-docker-nodocker-sample?color=f05340)
![Issues](https://img.shields.io/github/issues/tquangdo/elk-docker-nodocker-sample?color=f05340)
![Forks](https://img.shields.io/github/forks/tquangdo/elk-docker-nodocker-sample?color=f05340)
[![Report an issue](https://img.shields.io/badge/Support-Issues-green)](https://github.com/tquangdo/elk-docker-nodocker-sample/issues/new)

## reference
- a/docker: [viblo](https://viblo.asia/p/elasticsearch-kibana-logstash-tong-quan-cai-dat-va-su-dung-RQqKLRn6l7z)
- b/nodocker: [viblo](https://viblo.asia/p/quan-ly-log-ung-dung-voi-elk-stack-elasticsearch-logstash-va-kibana-Qbq5QJzmKD8)

## docker
just do with Elasticsearch & Kibana on `docker-compose.yml` (not yet with Logstash)

## nodocker
- just test with Elasticsearch & Kibana: `curl localhost:9200<5601>`. Can NOT access localhost on browser like `docker`
- need to edit these out-date command:
1. ### ubuntu
    ```shell
    sudo docker run --name elk_stack --net=host -it ubuntu:14.04 /bin/bash
    ->
    docker run --name elk_stack --net=host -it ubuntu /bin/bash
    ```

1. ### java
    ```shell
    add-apt-repository -y ppa:webupd8team/java
    apt-get -y install oracle-java8-installer
    ->
    apt-get install default-jdk
    ```

1. ### elasticsearch
    1. #### add key
        ```shell
        wget -qO - https://packages.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
        ->
        wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | apt-key add -
        ```

    1. #### install
        ```shell
        echo "deb http://packages.elastic.co/elasticsearch/2.x/debian stable main" | sudo tee -a /etc/apt/sources.list.d/elasticsearch-2.x.list
        ->
        echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | tee /etc/apt/sources.list.d/elastic-7.x.list
        ```

    1. #### service
        ```shell
        service elasticsearch start
        ->
        /etc/init.d/elasticsearch start
        /etc/init.d/elasticsearch status
        # * elasticsearch is running
        ```

1. ### kibana
    ```shell
    echo "deb http://packages.elastic.co/kibana/4.4/debian stable main" | sudo tee -a /etc/apt/sources.list.d/kibana-4.4.x.list
    ->
    echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | tee /etc/apt/sources.list.d/kibana-7.x.list
    ```

1. ### logstash
    1. #### install
        ```shell
        echo 'deb http://packages.elastic.co/logstash/2.2/debian stable main' | sudo tee /etc/apt/sources.list.d/logstash-2.2.x.list
        ->
        echo 'deb https://artifacts.elastic.co/packages/7.x/apt stable main' | tee /etc/apt/sources.list.d/logstash-7.x.list
        ```

    1. #### service
        ```shell
        service logstash start
        ->
        /usr/share/logstash/bin/logstash -f /etc/logstash/conf.d/myconfig.conf
        ~~~~~~~~~~~~~~~~
        [INFO ] 2023-02-19 03:21:34.906 [main] runner - Starting Logstash {"logstash.version"=>"7.17.9", "jruby.version"=>"jruby 9.2.20.1 (2.5.8) 2021-11-30 2a2962fbd1 OpenJDK 64-Bit Server VM 11.0.18+10 on 11.0.18+10 +indy +jit [linux-aarch64]"}
        [INFO ] 2023-02-19 03:21:34.937 [main] runner - JVM bootstrap flags: [-Xms1g, -Xmx1g, -XX:+UseConcMarkSweepGC, -XX:CMSInitiatingOccupancyFraction=75, -XX:+UseCMSInitiatingOccupancyOnly, -Djava.awt.headless=true, -Dfile.encoding=UTF-8, -Djdk.io.File.enableADS=true, -Djruby.compile.invokedynamic=true, -Djruby.jit.threshold=0, -Djruby.regexp.interruptible=true, -XX:+HeapDumpOnOutOfMemoryError, -Djava.security.egd=file:/dev/urandom, -Dlog4j2.isThreadContextMapInheritable=true]
        [WARN ] 2023-02-19 03:21:35.360 [LogStash::Runner] multilocal - Ignoring the 'pipelines.yml' file because modules or command line options are specified
        [INFO ] 2023-02-19 03:21:36.581 [Agent thread] configpathloader - No config files found in path {:path=>"/etc/logstash/conf.d/myconfig.conf"}
        [ERROR] 2023-02-19 03:21:36.595 [Agent thread] sourceloader - No configuration found in the configured sources.
        [INFO ] 2023-02-19 03:21:36.631 [Api Webserver] agent - Successfully started Logstash API endpoint {:port=>9600, :ssl_enabled=>false}
        [INFO ] 2023-02-19 03:21:41.948 [LogStash::Runner] runner - Logstash shut down.
        ```







