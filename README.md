# Administration de mon serveur Minecraft

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
