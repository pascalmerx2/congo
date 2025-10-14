---
title: "G03_B Structuration des mesures techniques de sécurité"
date: 2025-02-09
description: "Guide ANSSI"
summary: "Gouvernance, protection, défense, résilience"
---

Se former à ce modèle issu des approches cybersécurité (ANSSI, ISO 27001, NIST CSF) est cohérent avec les exigences RGPD, avec des notions de sécurité “appropriée” et “proportionnée” (art. 32) 

- Gouvernance → piloter et encadrer la sécurité,
- Protection → prévenir les incidents,
- Défense / Détection → identifier et réagir aux attaques,
- Résilience → assurer la continuité et le rétablissement.

## Overview

| **Pilier**                 | **Objectif principal**                                                     | **Exemples de mesures de sécurité RGPD associées**                                                                                                                                           | **Références CNIL / ISO / ANSSI**                                                    |
| -------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| 🧭 **Gouvernance**         | Piloter la conformité, définir les responsabilités, assurer la traçabilité | - Désignation du DPO<br>- Registre des traitements<br>- Politique de sécurité des données personnelles (PSSDP)<br>- Revue annuelle de conformité<br>- Procédure d’homologation ou d’AIPD     | RGPD art. 24-25-35<br>ISO 27001 chap. 5-9<br>ANSSI – PSSI / EBIOS RM                 |
| 🛡️ **Protection**         | Mettre en œuvre des mesures préventives pour limiter les risques           | - Contrôle d’accès / authentification forte<br>- Chiffrement des données de santé<br>- Cloisonnement réseau<br>- Gestion des habilitations<br>- Minimisation et pseudonymisation             | RGPD art. 32 §1 a-b<br>ISO 27002 – domaines A.8, A.9<br>ANSSI – Hygiène informatique |
| 🧰 **Défense / Détection** | Identifier rapidement les incidents et en limiter les impacts              | - Journalisation et audit des accès<br>- Supervision des logs d’accès aux données personnelles<br>- Procédure de détection de violation<br>- Formation du personnel à la gestion d’incidents | RGPD art. 33-34<br>ISO 27035<br>ANSSI – Guide détection d’incidents                  |
| ♻️ **Résilience**          | Garantir la disponibilité, la continuité et la restauration des données    | - Sauvegarde et tests de restauration<br>- Plan de continuité / reprise d’activité (PCA/PRA)<br>- Documentation des procédures<br>- Réversibilité avec prestataires                          | RGPD art. 32 §1 c-d<br>ISO 22301 / ISO 27031<br>ANSSI – Continuité d’activité        |


## Vues détaillées

### Gouvernance
- Cadre de maîtrise du risque (stratégie de sécurité, organisation de management du risque et d’amélioration continue, cartographie des systèmes et services, processus d’intégration de la sécurité dans les projets)
- Maîtrise de l’écosystème (clauses de sécurité dans les contrats de sous-traitances, sécurité des processus de développement et d’acquisition)
- Veille sur les vulnérabilités et les menaces
- Evaluation et suivi du niveau de sécurité (audits et contrôles internes, indicateurs de pilotage de la performance numérique)
- Gestion du facteur humain (sensibilisations, entraînements)

### Protection
- Sécurité de l'architecture du SI (Configuration des systèmes, Cloisonnement, Accès distant, Filtrage, Gestion des entrées/sorties de données et des supports amovibles, Sécurité des passerelles d’interconnexion) 
- Protection  des  données  (intégrité,  confidentialité,  gestion  des  clés  cryptographiques)
- Sécurité de l'administration des SI (administration, supervision) 
- Gestion des identités et des accès (Identification, Authentification, contrôle d’accès) 
- Maintien en conditions de sécurité et gestion d’obsolescence 
- Sécurité physique et environnementale (Sécurité vis-à-vis des signaux parasites compromettantsCadre de maîtrise du risque (stratégie de sécurité, organisation de management du risque et d’amélioration continue, cartographie des systèmes et services, processus d’intégration de la sécurité dans les projets)
- Maîtrise de l’écosystème (clauses de sécurité dans les contrats de sous-traitances, sécurité des processus de développement et d’acquisition)
- Veille sur les vulnérabilités et les menaces
- Evaluation et suivi du niveau de sécurité (audits et contrôles internes, indicateurs de pilotage de la performance numérique)
- Gestion du facteur humain (sensibilisations, entraînements)

### Défense
- Capteurs (sondes, journalisation)
- Détection (classification, corrélation et analyse des journaux, stratégie de supervision) 
- Gestion des incidents (traitement des alertes, qualification, réponse aux incidents)

### Résilience
- Continuité  d’activité  (sauvegarde  et  restauration,  gestion  des  modes  dégradés) ;
- Gestion de crise cyber (préparation, entrainement, dispositif de crise, plans, RETEX) ;
- Reprise  d’activité.

## Travaux pratiques
| **Piliers**     | **Objectif**                                                    | **Mesures associées (exemples)**                                                                                                                               |
| --------------- | --------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Gouvernance** | Assurer le pilotage global de la conformité                     | - Ex Validation du registre de traitements par la direction<br>- Suivi semestriel DPO / RSSI<br>- Contrôle d’accès validé par les métiers                         |
| **Protection**  | Empêcher l’accès non autorisé aux données                       | - Ex Mise en place d’un MFA <br>- Cloisonnement des comptes soignants<br>- Chiffrement du NAS de sauvegarde                                           |
| **Défense**     | Détecter les anomalies et violations                            | - Ex Activation de la traçabilité des accès<br>- Définition d’une procédure interne de notification CNIL<br>- Formation du personnel à la détection de fuites     |
| **Résilience**  | Garantir la continuité des soins et la récupération des données | - Ex Sauvegarde quotidienne testée trimestriellement<br>- Plan de reprise informatique (PRA)<br>- Procédure papier de continuité des soins en cas de panne réseau |

