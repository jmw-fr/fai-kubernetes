# FAI-Kubernetes

Le but de ce repository est d'automatiser l'installation de server Kubernetes avec l'excellent outil [FAI](https://fai-project.org).

## Installation du Debian

### VirtualBox

Avec VirtualBox, il peut être utile d'installer les extensions de VirtualBox.
Pour cela il faut activer les packages de compilation de Linux :
```
apt-get update
apt-get install build-essential
apt-get install linux-headers-amd64 linux-headers-4.9.0-6-amd64
```

```
bash /media/cdrom/VBoxLinuxAdditions.run
```

## Installation de FAI avec Ubuntu ou Debian

```
apt-get install wget aptitude
wget -O - https://fai-project.org/download/074BCDE4.asc | apt-key add -
echo "deb http://fai-project.org/download stretch koeln" > /etc/apt/sources.list.d/fai.list
apt-get update
apt-get instal reprepro squashfs-tools
aptitude install fai-server
```

Configuration de FAI
```
fai-setup -v
```

## Compilation d'une image ISO

### Récupération des sources

Installation de Git si nécessaire :

```
apt-get install git
```

Récupération des souces :

```
git clone https://github.com/jmw-fr/fai-kubernetes.git /srv/fai/config
```


### Création de l'ISO

```
fai-mirror -C /srv/fai/config/fai-kubernetes-master -m999 -cAMD64,DEBIAN,DHCPC,DEMO,GRUB_PC,FAIBASE,STRETCH,ONE,SSH_SERVER,STANDARD,FAIME /tmp/mirror

fai-cd -C /srv/fai/config/fai-kubernetes-master -g grub.cfg.install-only -m/tmp/mirror faime-ZUFSIL7F.iso
```