Kibana Web Admin for Logstash
=============================

Installation notes for Kibana logstash frontend.


Tutorial
--------
[Link](https://www.digitalocean.com/community/tutorials/how-to-install-elasticsearch-logstash-and-kibana-4-on-ubuntu-14-04)


Chef cookbooks
------------
Expect that we use librarian to manage chef cookbooks

*--> Add to *Cheffile* the following:*
    
    cookbook 'java'
    cookbook 'logstash', '~> 0.11.4'
    cookbook 'elasticsearch', '~> 0.3.13'

*--> Download all cookbooks with*
    
    librarian-chef install --verbose
    
*--> Create a role and setup the default attributes:*
        
        "java": {
            "install_flavor": "openjdk",
            "jdk_version": "7"
        },
        "elasticsearch": {
            "version": "1.5.2",
            "cluster": {"name": "logs"},
            "deb_url": "https://download.elastic.co/elasticsearch/elasticsearch/elasticsearch-1.5.2.deb",
            "deb_sha": "2595e14de7133fa23db90f83c83c84c0ea08468a"
        },
        "logstash": {
            "instance_default": {
                "elasticsearch_ip": "localhost",
                "elasticsearch_port": 9200,
                "elasticsearch_embedded": false,
                "ipv4_only": true,
                "init_method": "native",
                "web": {
                    "enabled": true,
                    "address": "0.0.0.0",
                    "port": 9292
                },
                "xmx": "500M"
            }
        },

**NOTE:** See more attributes in the cookbooks attributes 

*--> Upload all and make a provision*

*--> Install Kibana manually from the [link](https://www.digitalocean.com/community/tutorials/how-to-install-elasticsearch-logstash-and-kibana-4-on-ubuntu-14-04)*