# Smart Contract pour la Gestion de Brancardages en Milieu Hospitalier

Ce projet innovant utilise la technologie blockchain pour adresser une problématique cruciale dans la gestion des données de santé : l'accès abusif aux données sensibles. En exploitant la robustesse des smart contracts Ethereum, notre solution vise à améliorer la gestion des brancardages en milieu hospitalier, tout en garantissant une protection renforcée des données des patients contre les accès non autorisés.

## 🚀 Contexte et Enjeux

Dans le secteur hospitalier, la gestion des données patients est au cœur des préoccupations, notamment avec le système d'ORBIS pour lequel les informations sensibles doivent être scrupuleusement protégées. Notre projet prend racine dans l'observation directe de l'utilisation inappropriée des données personnelles des patients, comme observé lors d'un stage au CHU Henri Mondor, révélant la nécessité d'un renforcement de la sécurité des données. 

**Problématique :** Le logiciel PTAH, étroitement lié à ORBIS, soulève des défis similaires en termes de sécurisation des données, car il est susceptible d'être utilisé pour accéder de manière abusive aux informations des patients. Ce constat est particulièrement alarmant et exige une solution capable d'endiguer ces pratiques tout en assurant une gestion fluide des processus hospitaliers. Pour plus de détails sur le fonctionnement du PTAH, consultez [cet article](https://medium.com/wanabilini/%EF%B8%8F-%EF%B8%8F-coup-doeil-rapide-sur-le-logiciel-ptah-afbc6fe0ab64).

## 🎯 Objectifs du Projet

- **Sécurisation accrue des données patients** : Utiliser la blockchain pour protéger les informations sensibles et personnelles contre les accès non autorisés ou malveillants.
- **Amélioration de la gestion des brancardages** : Assurer une coordination et un suivi efficaces des demandes de transport interne des patients, en apportant une solution digitale transparente et sécurisée.
- **Prévention des accès abusifs aux données sensibles** : Empêcher l'utilisation inappropriée des informations personnelles des patients en exploitant la traçabilité et l'immutabilité offertes par la blockchain.

## 🔧 Fonctionnalités Clés

Le smart contract `TransportManager` intègre plusieurs composantes essentielles pour la gestion des brancardages :

### Gestion des Rôles
- **assignRole(address userAddress, Role role)** : Assigner des rôles spécifiques (Admin, Doctor, Porter) aux utilisateurs, permettant un contrôle d'accès basé sur les rôles.

### Gestion des Patients
- **addPatient(string name, uint dateOfBirth)** : Ajouter un nouveau patient au système, accessible uniquement par les médecins.
- **getAllPatients()** : Récupérer les détails de tous les patients enregistrés dans le système.

### Gestion des Unités Hospitalières
- **addUnit(string unitCode, string unitLabel, string building)** : Ajouter une nouvelle unité hospitalière au système pour faciliter la coordination des transports.

### Gestion des Demandes de Transport
- **addTransportRequest(...)** : Créer une nouvelle demande de transport pour un patient, spécifiant l'unité de départ, l'unité d'arrivée, et les heures de début et de fin.
- **updateTransportRequest(uint requestId, string status)** : Mettre à jour le statut d'une demande de transport, accessible par les brancardiers.
- **deleteTransportRequest(uint requestId)** : Supprimer une demande de transport, accessible par les médecins.

### Logs d'Actions
- **getActionLogs()** : Récupérer l'historique des actions effectuées au sein du smart contract pour audit et traçabilité.

## 📘 Pour Aller Plus Loin

Nous invitons les parties intéressées à approfondir leur compréhension des enjeux et des solutions proposées par notre projet, en jetant un coup d'oeil à notre documentation complète sous forme de PowerPoint.
