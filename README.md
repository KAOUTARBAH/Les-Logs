# Les-Logs

## Exercice
- Imagine que tu es responsable des logs réseau. Énumère un scénario spécifique dans lequel les logs seraient cruciaux et explique pourquoi.

## Logs sous Linux Ubuntu

Sur un système Linux Ubuntu, plusieurs types de logs sont enregistrés dans le répertoire `/var/log`. Voici deux types de logs courants, leur emplacement et leur contenu :

### Logs du système

- **Emplacement** : `/var/log/syslog`  
- **Description** : Ce fichier contient des informations générales sur le système, y compris les messages des services, du noyau et des applications. Il est utile pour diagnostiquer des problèmes liés au démarrage du système ou aux processus en cours.

### Logs d’authentification

- **Emplacement** : `/var/log/auth.log`  
- **Description** : Ce fichier enregistre tous les événements liés à l’authentification, comme les connexions réussies et échouées, les tentatives de connexion SSH et les élévations de privilèges (`sudo`). Il est essentiel pour surveiller la sécurité du système.

### Autres logs courants

- **`/var/log/dmesg`** : Contient les messages du noyau, notamment ceux générés au démarrage du système.  
- **`/var/log/apache2/access.log`** : Enregistre les requêtes HTTP pour le serveur web Apache (si installé).  

Ces fichiers de logs sont essentiels pour le diagnostic et la maintenance d’un système Linux.

## Exercice
### 📌 Analyse de l'entrée de log  suivante et réponds aux questions :

```bash
2023-07-28 09:15:23 [WARNING] [FileSystem] Disk usage on /dev/sda1 has reached 85%
```

## ❓ Questions et réponses  

### 1️⃣ Quel est le timestamp de cet événement ?  
**🕒 Réponse :** `2023-07-28 09:15:23`  

### 2️⃣ Quel est le niveau de log ?  
**⚠️ Réponse :** `WARNING` (avertissement)  

### 3️⃣ Quelle est la source du log ?  
**📂 Réponse :** `FileSystem`  

### 4️⃣ Quel est le message principal ?  
**💬 Réponse :** `Disk usage on /dev/sda1 has reached 85%`  
*(L'utilisation du disque sur `/dev/sda1` a atteint 85%)*  

### 5️⃣ Quelle action recommanderais-tu suite à ce log ?  
✅ **Recommandations :**  
- Vérifier l'espace disque disponible avec `df -h`  
- Identifier les fichiers volumineux avec `du -sh /chemin/*`  
- Supprimer ou archiver les fichiers inutiles  
- Envisager une extension du stockage si nécessaire  
- Mettre en place un monitoring pour éviter d'atteindre une limite critique  

📢 **⚠️ Attention :** Une utilisation excessive du disque peut entraîner des problèmes de performance ou des erreurs système !  
