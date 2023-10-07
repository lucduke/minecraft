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


