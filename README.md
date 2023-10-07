# Administration de mon serveur Minecraft

Penser à installer Java 8 (openjdk-8-jre)

## Exemple de script pour lancer le serveur BungeeCord
```bash
#!/bin/bash
java -Xms512M -Xmx1G -jar BungeeCord.jar nogui
```

## Exemple de script pour lancer le serveur
```bash
#!/bin/bash
java -Xms512M -Xmx2G -jar spigot-1.8.8-R0.1-SNAPSHOT-latest.jar nogui --log-limit=10M
```

## Utilisation de screen

### Installation
```bash
sudo apt install screen
```

### Utilisation
```bash
# Creer une session
screen -S <session_name>

# Lister des sessions
screen -ls

# Se détacher d'une session
Ctrl+a d

# Se rattacher à une session existante
screen -r <session_name>
screen -R <PID>

# Fermer une session
screen -S <session_name> -X quit
kill <session_id>
#ou pour fermer la session courante
exit
```

## Utilisation de systemd

### Créer un service systemd pour le serveur BungeeCord
```bash
sudo nano /etc/systemd/system/minecraft_bungee.service
```

Et ajoutez le contenu suivant au fichier :
```ini
[Unit]
Description=Minecraft BungeeCord Server
After=network.target

[Service]
User=minecraft-user # Remplacez par le nom de l'utilisateur sous lequel vous souhaitez exécuter le serveur
WorkingDirectory=/chemin/vers/votre/serveur/minecraft
ExecStart=/usr/bin/java -Xms512M -Xmx1G -jar BungeeCord.jar nogui
Restart=on-failure
RestartSec=30
StandardInput=null

[Install]
WantedBy=multi-user.target
```

On recharge systemd:

```bash
sudo systemctl daemon-reload
```

On démarre le service:
```bash
sudo systemctl start minecraft_bungee.service
sudo systemctl enable minecraft_bungee.service
```

Pour vérifier l'état du service:
```bash
sudo systemctl status minecraft_bungee.service
```

### Créer un service systemd pour le serveur
```bash
sudo nano /etc/systemd/system/minecraft_serveur1.service
```

Et ajoutez le contenu suivant au fichier :

```ini
[Unit]
Description=Minecraft Serveur1 Server
After=network.target

[Service]
User=minecraft-user # Remplacez par le nom de l'utilisateur sous lequel vous souhaitez exécuter le serveur
WorkingDirectory=/chemin/vers/votre/serveur/minecraft
ExecStart=/usr/bin/java -Xms512M -Xmx2G -jar spigot-1.8.8-R0.1-SNAPSHOT-latest.jar nogui --log-limit=10M
Restart=on-failure
RestartSec=30
StandardInput=null

[Install]
WantedBy=multi-user.target
```

On recharge systemd:

```bash
sudo systemctl daemon-reload
```

On démarre le service:
```bash
sudo systemctl start minecraft_serveur1.service
sudo systemctl enable minecraft_serveur1.service
```

Pour vérifier l'état du service:
```bash
sudo systemctl status minecraft_serveur1.service
```

### Pour consulter le journal
```bash
journalctl -xeu minecraft_bungee.service
``` 