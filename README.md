# Smart Contract pour la Gestion de Brancardages en Milieu Hospitalier

Ce projet innovant utilise la technologie blockchain pour adresser une problématique cruciale dans la gestion des données de santé : l'accès abusif aux données sensibles. En exploitant la robustesse des smart contracts Ethereum, notre solution vise à améliorer la gestion des brancardages en milieu hospitalier, tout en garantissant une protection renforcée des données des patients contre les accès non autorisés.

## 🚀 Contexte et Enjeux

Dans le secteur hospitalier, la gestion des données patients est au cœur des préoccupations, notamment avec le système d'ORBIS pour lequel les informations sensibles doivent être scrupuleusement protégées. Notre projet prend racine dans l'observation directe de l'utilisation inappropriée des données personnelles des patients, comme observé lors d'un stage au CHU Henri Mondor, révélant la nécessité d'un renforcement de la sécurité des données. 

**Problématique :** Le logiciel PTAH, étroitement lié à ORBIS, soulève des défis similaires en termes de sécurisation des données, car il est susceptible d'être utilisé pour accéder de manière abusive aux informations des patients. Ce constat est particulièrement alarmant et exige une solution capable d'endiguer ces pratiques tout en assurant une gestion fluide des processus hospitaliers. Pour plus de détails sur le fonctionnement du PTAH, consultez cet article : [👁️‍🗨️](https://medium.com/wanabilini/%EF%B8%8F-%EF%B8%8F-coup-doeil-rapide-sur-le-logiciel-ptah-afbc6fe0ab64).

## 🎯 Objectifs du Projet

- **Sécurisation accrue des données patients** : Utiliser la blockchain pour protéger les informations sensibles et personnelles contre les accès non autorisés ou malveillants.
- **Amélioration de la gestion des brancardages** : Assurer une coordination et un suivi efficaces des demandes de transport interne des patients, en apportant une solution digitale transparente et sécurisée.
- **Prévention des accès abusifs aux données sensibles** : Empêcher l'utilisation inappropriée des informations personnelles des patients en exploitant la traçabilité et l'immutabilité offertes par la blockchain.

## 🧱 Structures de Données

Le smart contract `TransportManager` utilise plusieurs structures (structs) pour organiser les données de manière efficace et sécurisée :

- 🤒 **`Patient`** : Représente les informations d'un patient, incluant un identifiant unique (`id`), le nom (`name`), et la date de naissance (`dateOfBirth`)
- 🏥 **`Unit`** : Décrit une unité hospitalière avec un code unique d'unité (`unitCode`), un label (`unitLabel`) pour le nom de l'unité, et le bâtiment où l'unité est localisée (`building`)
- 📋 **`TransportRequest`** : Contient les détails d'une demande de transport, y compris un identifiant unique (`id`), l'identifiant du patient (`patientId`), les codes des unités de départ et d'arrivée (`departureUnitCode`, `arrivalUnitCode`), les heures de début et de fin (`startTime`, `endTime`), le statut de la demande (`status`), ainsi que les adresses de la personne ayant créé la demande (`assignedBy`) et du brancardier assigné (`assignee`)
- 🎬 **`ActionLog`** : Enregistre les actions effectuées dans le contrat, avec un horodatage (`timestamp`), une description de l'action (`action`), et l'adresse de l'utilisateur (`user`) ayant réalisé l'action.


## 🔧 Fonctionnalités Clés

Le smart contract `TransportManager` intègre plusieurs composantes essentielles pour la gestion des brancardages, permettant à l'utilisateur de bénéficier de plusieurs fonctionnalités :

### Gestion des Rôles
- **`assignRole(address userAddress, Role role)`** : Définir des rôles pour différents utilisateurs, en attribuant des rôles spécifiques (Admin, Doctor, Porter). Cela garantit que chaque utilisateur a accès uniquement aux fonctionnalités qui lui sont autorisées, renforçant la sécurité et la conformité du système.
- **`getRoles()`** : Récupérer la liste des adresses et des rôles assignés à chaque utilisateur au sein du système.

### Gestion des Patients
- **`addPatient(string name, uint dateOfBirth)`** : Permettre aux médecins d'ajouter un nouveau patient au système. Chaque patient est ajouté avec un identifiant unique, son nom, et sa date de naissance, assurant une gestion précise et sécurisée des données patient.
- **`getAllPatients()`** : Récupérer les détails de tous les patients enregistrés dans le système, offrant aux utilisateurs autorisés une vue d'ensemble des patients pour faciliter la gestion et la coordination des soins.

### Gestion des Unités Hospitalières
- **`addUnit(string unitCode, string unitLabel, string building)`** : Ajouter une nouvelle unité hospitalière au système, en spécifiant un code d'unité unique, un label et le bâtiment correspondant. Cette fonction est cruciale pour structurer l'organisation des transports au sein des différentes unités de l'hôpital.
- **`getAllUnits()`** : Récupèrer les informations de toutes les unités hospitalières enregistrées, facilitant ainsi la planification et la coordination des demandes de transport entre différentes unités.

### Gestion des Demandes de Transport
- **`addTransportRequest(uint patientId, string memory departureUnitCode, ..., string memory status, address assignee)`** : Permettre aux médecins de créer une nouvelle demande de transport pour un patient, en spécifiant les unités de départ et d'arrivée, les heures de début et de fin prévues, ainsi que le brancardier en charge du transport. Chaque demande est enregistrée avec un identifiant unique et des détails précis pour une traçabilité et une gestion optimales.
- **`updateTransportRequest(uint requestId, string status)`** : Permettre aux brancardiers de mettre à jour le statut d'une demande de transport (par exemple, de "en attente" à "complété"), assurant ainsi un suivi en temps réel du processus de transport.
- **`deleteTransportRequest(uint requestId)`** : Permettre aux médecins de supprimer une demande de transport. Cela peut être nécessaire en cas d'annulation ou de modification des besoins de transport du patient.

### Logs d'Actions
- **`getActionLogs()`** : Récupérer un historique complet des actions effectuées au sein du contrat, y compris l'ajout de patients, la création, mise à jour, et suppression de demandes de transport. Cette fonctionnalité est essentielle pour l'audit et la traçabilité, offrant une transparence totale des opérations réalisées.


## 🛂 Sécurité et Contrôle d'Accès

Votre contrat implémente plusieurs modificateurs (`onlyAdmin`, `onlyDoctor`, `onlyPorter`, `isTaskOwner`, `isTaskExecutor`) pour restreindre l'accès aux fonctions critiques selon le rôle de l'utilisateur, garantissant ainsi que les opérations sont effectuées par les utilisateurs autorisés.


## 🔔 Événements

Des événements (`TransportRequestAdded`, `TransportRequestUpdated`, `TransportRequestDeleted`, `RoleAssigned`) sont émis pour notifier les modifications importantes dans le système, facilitant la réactivité de l'interface utilisateur et l'intégration avec d'autres systèmes.


## 📘 Pour Aller Plus Loin

Nous vous invitons à approfondir leur compréhension des enjeux et des solutions proposées par notre projet, en jetant notamment un coup d'oeil à notre documentation complète sous forme de PowerPoint : Smart_Contract_PTAH.pptx
