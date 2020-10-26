# ELK 7.9.3

*Dernière version fonctionnelle : 26/10/20*

## Description

Fichiers de configurations pour des conteneurs dockers pour une pile ELK 7.9.3.
Les fichiers comprennent aussi des configurations de logstash pour collecter des logs `ssh` `apache2` `nginx`

## Prérequis

### Installation de docker et docker-compose

```
$ sudo apt-get update

$ sudo apt-get install \
apt-transport-https \
ca-certificates \
curl \
gnupg-agent \
software-properties-common
$ curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
$ sudo apt-key fingerprint 0EBFCD88

pub   4096R/0EBFCD88 2017-02-22
      Key fingerprint = 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid                  Docker Release (CE deb) <docker@docker.com>
sub   4096R/F273FCD8 2017-02-22
$ sudo add-apt-repository \
"deb [arch=amd64] https://download.docker.com/linux/debian \
$(lsb_release -cs) \
stable"
 $ sudo apt-get update
 $ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose
```

## Installation

```
$ git clone `url du git`
$ cd elk
$ docker-compose up --build
```

## Documentation

### Emplacement des fichiers de configuration 
```
.
├── docker-compose.yml     # Fichiers docker-compose définissant les images dockers à utiliser
├── logstash
│   ├── config
│   │   └── logstash.yml   # Configuration de logstash
│   └── pipeline
│       ├── apache.conf    # Configuration de logstash pour `apache2`
│       ├── auth.conf      # Configuration de logstash pour `ssh`
│       └── nginx.conf     # Configuration de logstash pour `nginx`
└── README.md              # Fichier README du repo
```

### Utilisation

Les ports pour les différents services sont :
* `elastic` : 9200
* `kibana` : 5601
* `logstash` :
  * `apache2` : 5000
  * `ssh` : 5001
  * `nginx` : 5002

Par conséquent pour ingérer les différents types de logs :
```
$ cat apache_access.log | nc -q0 localhost 5000
$ cat auth.log | nc -q0 localhost 5001
$ cat nginx_access.log | nc -q0 localhost 5002
```

## Sources
* [Installation de docker](https://docs.docker.com/engine/install/debian/)