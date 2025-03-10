
# Guide de configuration d'une machine virtuelle Windows Server avec rôle DNS et création d'une vue personnalisée dans l'Event Viewer

Ce guide vous explique comment configurer une machine virtuelle Windows Server, installer le rôle DNS, et créer une vue personnalisée dans l'Event Viewer pour surveiller les événements DNS.

## Étapes à suivre

### 1. Créer une machine virtuelle Windows Server
- Créez une machine virtuelle sur une plateforme de virtualisation comme **Hyper-V**, **VMware**, ou **VirtualBox**.
- Assurez-vous que votre machine virtuelle est installée avec une version de **Windows Server** (par exemple, Windows Server 2019 ou 2022).

### 2. Installer le rôle DNS
- Connectez-vous à la machine virtuelle Windows Server.
- Ouvrez **Server Manager**.
- Cliquez sur **Add roles and features** (Ajouter des rôles et des fonctionnalités).
- Sélectionnez le rôle **DNS Server**.
- Suivez les instructions pour installer le rôle DNS. Cela activera le serveur DNS sur la machine.

### 3. Ouvrir l'Event Viewer (Visionneuse d'événements)
- Pressez **Win + R**, tapez `eventvwr.msc` et appuyez sur **Entrée** pour ouvrir l'Event Viewer.

### 4. Créer une vue personnalisée
Dans l'Event Viewer, suivez ces étapes pour créer une vue personnalisée en fonction des critères fournis :

#### Accéder à la création de la vue personnalisée :
- Dans le panneau gauche, sous **Custom Views** (Vues personnalisées), cliquez avec le bouton droit et sélectionnez **Create Custom View** (Créer une vue personnalisée).

#### Configurer les niveaux d’événements à surveiller :
- Dans l'onglet **Filter** (Filtre), sous **Event Level** (Niveau d'événement), cochez les cases suivantes :
  - **Critical** (Critique)
  - **Error** (Erreur)
  - **Warning** (Avertissement)
  - **Information** (Information)

#### Sélectionner les sources d'événements à inclure :
- Dans la section **Event sources** (Sources d'événements), cliquez sur **<All Event Sources>** et entrez les sources suivantes :
  - **DNS-Server-Service** : pour les événements du serveur DNS.
  - **DNS Client Events** : pour les événements côté client.

#### Configurer les ID d’événements spécifiques à surveiller :
- Sous **Event IDs** (ID d'événements), entrez les ID suivants :
  - **2** : Démarrage du serveur DNS.
  - **4** : Arrêt du serveur DNS.
  - **409** : Erreur de résolution de nom.
  - **501-502** : Échec de chargement de zone.
  - **6001-6002** : Problèmes de réplication DNS.

#### Nommer la vue personnalisée :
- Sous **Name** (Nom), donnez un nom descriptif à votre vue, par exemple : `DNS Server Events`.

#### Enregistrer la vue personnalisée :
- Cliquez sur **OK** pour enregistrer la vue personnalisée.
- La nouvelle vue devrait apparaître sous **Custom Views** (Vues personnalisées) dans l'Event Viewer.

### 5. Exporter la vue au format XML
Une fois la vue personnalisée configurée, voici comment l'exporter :

- Cliquez avec le bouton droit sur la vue personnalisée que vous venez de créer sous **Custom Views**.
- Sélectionnez **Export Custom View...**.
- Sauvegardez le fichier XML sur votre ordinateur, par exemple sous le nom `DNS_Events_View.xml`.

### 6. Ajouter le fichier XML sur GitHub
- Créez un dépôt sur **GitHub** (ou utilisez un dépôt existant).
- Téléversez le fichier `DNS_Events_View.xml` dans ce dépôt.
- Créez un fichier `README.md` pour expliquer la vue personnalisée.

#### Exemple de contenu pour le README :
```markdown
# Vue personnalisée pour les événements DNS

Ce dépôt contient une vue personnalisée pour l'Event Viewer sur Windows Server afin de surveiller les événements liés au service DNS et son état.


## Critères de la vue personnalisée :
- Niveaux surveillés : Critique, Erreur, Avertissement, Information
- Sources d'événements : DNS-Server-Service, DNS Client Events
- Événements surveillés :
  - 2 : Démarrage du serveur DNS
  - 4 : Arrêt du serveur DNS
  - 409 : Erreur de résolution de nom
  - 501-502 : Échec de chargement de zone
  - 6001-6002 : Problèmes de réplication DNS
![log-dns](https://github.com/KAOUTARBAH/Les-Logs/blob/main/images/log-dns.png)

## Instructions
1. Téléchargez le fichier XML.
2. Importez-le dans l'Event Viewer en cliquant sur **Import Custom View**.
