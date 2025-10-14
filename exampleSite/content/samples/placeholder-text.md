---
title: "G6 Gestion projet"
date: "2020-03-09"
lastmod: "2022-01-24"
draft: true
description: "Lorem Ipsum Dolor Si Amet"
tags: ["markdown", "text", "sample", "latin"]
showDateUpdated: true
xml: false
---

développer une culture de gestion de projet à part entière, qui doit concilier :

- la méthodologie de gestion des risques (ISO 27005, EBIOS RM),

- la conformité RGPD (plan de traitement des risques issus de l’AIPD),

- et la gouvernance SSI / DPO de l’organisation.

### Ce que nous dit le RGPD

Le RGPD (Règlement Général sur la Protection des Données), en son article 24, impose au responsable de traitement de mettre en œuvre des mesures techniques et organisationnelles appropriées pour s'assurer et être en mesure de démontrer que les traitements sont effectués conformément au règlement. Ces mesures sont réexaminées et actualisées si nécessaire.
Les réponses aux audits dans le cadre des contrôles doivent être accompagnées d’éléments de preuve (article 24)

### Rappel des objectifs généraux de protection de la vie privée dans la politique de protection de la vie privée 
- La classification exhaustive des données à caractère personnel
- L’obligation de formalisation des registres des traitements, des demandes d’exercices de droit des personnes concernées et de notifications de violations de données à caractère personnel
- L’effectivité des droits des personnes concernées
- Le renforcement de la culture « protection de la vie privée »
- La définition des prérogatives pour engager contractuellement le sous-traitant
- La sécurité des données et des traitements
- L’évolution et le contrôle de la politique...
  
### Le mode projet 
| **Phase**                                 | **Objectif**                                                                   | **Livrables / Outils**                             | **Acteurs principaux**    |
| ----------------------------------------- | ------------------------------------------------------------------------------ | -------------------------------------------------- | ------------------------- |
| **1. Initialisation et cadrage**          | Définir le périmètre, les enjeux, les rôles, et le calendrier du plan d’action | Charte de projet, matrice RACI, calendrier global  | DPO, RSSI, Direction      |
| **2. Priorisation des risques résiduels** | Identifier les risques à traiter en priorité selon leur gravité et faisabilité | Matrice criticité × faisabilité                    | DPO + RSSI                |
| **3. Élaboration du plan d’action**       | Définir les actions, responsables, ressources, et échéances                    | Plan de traitement des risques, fiches actions     | DPO, RSSI, DSIO, métiers  |
| **4. Mise en œuvre et suivi**             | Piloter les actions, suivre l’avancement, ajuster                              | Tableau de bord de suivi, comptes rendus de comité | Chef de projet SSI / RGPD |
| **5. Clôture et réévaluation**            | Valider les mesures, réévaluer les risques, documenter la conformité           | Rapport de traitement des risques, MAJ AIPD        | DPO, RSSI, direction      |


### Travaux pratiques : focus Plan d'action SI
- 1	Accès non sécurisé au logiciel métier --> ex Authentification forte (MFA)	RSSI / Prestataire	
- 2	Sauvegardes non testées	--> Mise en place tests trimestriels + rapport	
- 3	Absence de registre des accès aux dossiers patients	--> archivage logs	DPO + RSSI	Logs disponibles à 6 mois	

### Suivi Tableau de Bord : Les indicateurs pour mesurer l’atteinte des objectifs

#### Objectif : piloter la mise en œuvre des actions et arbitrer les difficultés.

#### Mécanismes : Comité mensuel DPO/RSSI/direction,

#### Suivi de l’avancement par indicateurs, utiliser des indicateurs de maturité (ex. % de mesures ISO 27002 mises en œuvre), Maintenir une traçabilité RGPD (preuve de conformité → CNIL).
- Le nombre de directions métiers ayant classifié les données à caractère personnel et les traitements associés
- Le nombre de traitements entièrement référencés dans le registre
- Le niveau de complétude du registre
- Le nombre de traitements conformes
- Le nombre de services respectant les procédures et les moyens spécifiques aux traitements des données sensibles ou perçues comme sensibles ;
- Le nombre de traitements respectant les exigences réglementaires consécutives à la législation concernant les droits des personnes concernées
- Le pourcentage de règles de sécurité conformes
- Le pourcentage de collaborateurs sensibilisés et la périodicité des formations ou ateliers de sensibilisation
- Le nombre de contrôles.
