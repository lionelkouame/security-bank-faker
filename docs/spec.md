# 📚 Deep Dive : Les Cas d'Usage du "User Provider"

Dans l'architecture de **Security Bank Faker**, 
le **User Provider** (Fournisseur d'utilisateurs) constitue le premier niveau de la pyramide de sécurité. 
Son rôle est d'extraire un objet utilisateur depuis un support de stockage à partir d'un identifiant unique 
(e-mail, matricule, etc.).

## 1. Les Sources de Données (Types de Providers)

### A. Entity User Provider (Doctrine)
**Description** : Charge les utilisateurs depuis une base de données via l'ORM Doctrine.
* **Cas d'usage** : Identification des clients (`ROLE_CUSTOMER`) et du personnel via leur adresse e-mail.
**Fonctionnement** : Symfony utilise la propriété `email` de l'entité `User` pour interroger la base de données.

### B. Memory User Provider (Configuration)
**Description** : Les utilisateurs sont définis directement dans le fichier `security.yaml`.
**Cas d'usage** : Création d'un compte de maintenance d'urgence ("Emergency Admin") accessible même en cas de panne de la base de données.

### C. LDAP User Provider (Entreprise)
**Description** : Charge les utilisateurs depuis un serveur LDAP (Lightweight Directory Access Protocol).
**Cas d'usage** : Authentification centralisée pour les directeurs de succursales gérés au niveau du groupe.

### D. Chain User Provider (Système Hybride)
**Description** : Permet de fusionner plusieurs providers en un seul.
**Cas d'usage** : Symfony parcourt l'ordre des providers définis (ex: LDAP puis Doctrine) jusqu'à ce qu'il trouve une correspondance.
**Avantage** : Indispensable pour notre banque qui possède des sources d'identités hétérogènes.

### E. Custom User Provider
**Description** : Implémentation personnalisée de la `UserProviderInterface`.
**Cas d'usage** : Authentification via un service externe (API de validation interbancaire).

---

## 2. Cycle de Vie et Rafraîchissement
Le User Provider intervient à deux moments critiques de la requête HTTP :

### A. Chargement Initial (Authentification)
Lors de la connexion, le provider charge l'utilisateur basé sur l'identifiant fourni.
Ce mécanisme est également utilisé pour le **Remember Me** et l'**Impersonnalisation**.

### B. Rafraîchissement de Session (Refresh)
Au début de chaque requête (sauf firewall `stateless`), l'utilisateur est désérialisé depuis la session.
Le provider "rafraîchit" l'utilisateur en interrogeant à nouveau la source de données pour garantir que les informations (rôles, mots de passe) sont à jour.
Si une donnée critique (mot de passe, identifiant) a changé, l'utilisateur est déconnecté pour prévenir toute faille de sécurité.


---

## 3. Optimisation et Contrôle Avancé

### A. Comparaison Manuelle (`EquatableInterface`)
* Description** : En implémentant cette interface dans l'entité `User`, vous remplacez la logique de comparaison par défaut de Symfony.
* Cas d'usage** : Déconnecter manuellement un utilisateur si son niveau d'accréditation bancaire a été modifié durant sa session.

### B. Sécurisation de la Session (`__serialize`)
* [cite_start]Pour ne pas stocker le hash du mot de passe en clair dans la session, il est recommandé d'implémenter la méthode magique `__serialize().
* Stratégie CRC32c** : Stocker un hash `crc32c` du mot de passe dans la session permet de valider l'intégrité et d'invalider les sessions lors d'un changement de mot de passe sans exposer le hash principal.


*Ce document technique est basé sur les standards de sécurité de Symfony 8.0.*
