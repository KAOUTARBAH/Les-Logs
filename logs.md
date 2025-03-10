#  Challenge : Installation et Analyse d'un Serveur Web
  
1. **Installer** un serveur web (Apache ou Nginx) sur une machine virtuelle Linux.  
2. **Configurer** le logging pour enregistrer :  
   - Les accès  
   - Les erreurs  
3. **Générer du trafic** sur le serveur web à l’aide d’outils comme `curl` ou un navigateur.  
4. **Analyser les logs** pour identifier :  
   - Les requêtes réussies (code **200**)  
   -  Les erreurs **404** (page non trouvée)  
   -  Les adresses **IP les plus fréquentes**  


## 🛠 Étapes  

### 1️. Installation du serveur web  
👉 **Sur une machine virtuelle Linux**, installe Apache ou Nginx :  

#### 🔹 Installer  Apache  
```bash
sudo apt update
sudo apt install apache2 -y
```
#### 🔹Vérifier l'état du service Apache
```bash
systemctl status apache2
```
#### 🔹Tester l'installation

- Ouvrez un navigateur web et accédez à http://localhost ou http://[IP_de_la_VM]. Vous devriez voir la page par défaut d'Apache, ce qui signifie qu'Apache est installé et fonctionne correctement.

### 2. Configurer les logs Apache

Les logs d'Apache sont déjà configurés par défaut, mais vous pouvez les personnaliser si nécessaire.

## 🔹 Fichiers de logs par défaut :
- **Logs d'accès** : `/var/log/apache2/access.log`
- **Logs d'erreurs** : `/var/log/apache2/error.log`

## 🔹 Vérifier ou personnaliser la configuration des logs
Pour vérifier ou personnaliser la configuration des logs, vous pouvez éditer les fichiers de configuration d'Apache.

### Modifier les logs (facultatif) :
1. Ouvrez le fichier de configuration `apache2.conf` avec `nano` :
   ```bash
   sudo nano /etc/apache2/apache2.conf

2. Recherchez la ligne suivante pour personnaliser le format des logs :
    ```bash
    LogFormat "%h %l %u %t \"%r\" %>s %b" combined
    CustomLog /var/log/apache2/access.log combined
    ErrorLog ${APACHE_LOG_DIR}/error.log
    ```
-  Appliquer les changements
    ```bash
    sudo systemctl restart apache2
    ```

### 3. Générer du trafic sur le serveur

Pour générer des requêtes et des logs, vous pouvez utiliser `curl` ou un navigateur.

#### Utilisation de curl pour simuler des requêtes :

```bash
curl http://localhost           # Accède à la page d'accueil
curl -I http://localhost

curl http://localhost/test      # Page inexistante (génère une erreur 404)
curl -I http://localhost/test

curl -A "Googlebot" http://localhost  # Simulation d'un bot
```

#### Utilisation d'un navigateur :

Accédez à [http://localhost](http://localhost) ou [http://[IP_de_la_VM]](http://[IP_de_la_VM]) dans votre navigateur et naviguez sur différentes pages pour générer des logs.

## Générer du trafic avec un script shell :

Pour générer du trafic massif, utilisez ce script :

```bash
for i in {1..50}; do curl -s http://localhost > /dev/null; done
```
cat /var/log/apache2/access.log | tail -n 50

### 3. Analyser les logs générés

#### 🔹 Requêtes réussies (code 200)
Pour rechercher les requêtes ayant renvoyé le code **200** (succès) dans le fichier `access.log`, exécutez cette commande :

```bash
cat /var/log/apache2/access.log | grep ' 200 '
```

#### 🔹 Erreurs 404 (Page non trouvée)
Pour rechercher les erreurs **404** (page non trouvée) dans les logs, exécutez la commande suivante :

```bash
cat /var/log/apache2/access.log | grep ' 404 '
```

#### 🔹 Adresses IP les plus fréquentes
Pour afficher les **adresses IP les plus fréquentes** dans les logs d'accès, utilisez la commande suivante :

```bash
awk '{print $1}' /var/log/apache2/access.log | sort | uniq -c | sort -nr | head -10
```

Cela vous montrera les 10 adresses IP les plus fréquentes dans le fichier access.log.