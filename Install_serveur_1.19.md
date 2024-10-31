# Installation d'un serveur minecraft 1.19.4

## Mise à jour du systeme

```bash
sudo apt update
sudo apt upgrade
```

## Installation de Java

On installe OpenJDK 17 (la version exigée par Minecraft 1.19.4)

```bash
sudo apt install openjdk-17-jre-headless
```

## Création d'un nouvel utilisateur pour le serveur minecraft

```bash
sudo useradd -m -d /opt/minecraft minecraft
```

## Téléchargement et installation de Minecraft server

On se connecte en tant qu'utilisateur minecraft pour télécharger le jar

```bash
sudo su - minecraft
cd /opt/minecraft
wget https://piston-data.mojang.com/v1/objects/8f3112a1049751cc472ec13e397eade5336ca7ae/server.jar
```

## On démarre le serveur

```bash
java -Xmx1024M -Xms1024M -jar server.jar nogui
```

## Acceptation des conditions d'utilisation

On édite pour cela le fichier eula.txt et on change la valeur de eula=false en eula=true

## Démarrage automatique du serveur comme un service systemd

On créer un nouveau fichier '/etc/systemd/system/minecraft.service' avec le contenu suivant:

```ini
[Unit]
Description=Minecraft Server
After=network.target

[Service]
User=minecraft
Group=minecraft
Type=simple
WorkingDirectory=/opt/minecraft
ExecStart=/usr/bin/java -Xmx1024M -Xms1024M -jar server.jar nogui
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

Ensuite, on active et on démarre le service avec la commande suivante:

```bash
sudo systemctl enable minecraft
sudo systemctl start minecraft
```
