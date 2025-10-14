---
title: "G03_A Notion de Référentiel Technique (IT)"
date: 2025-03-02
lastmod: 2025-04-02
draft: true
description: "interet carto"
showDateUpdated: true
---


Connaître l’existence d’un référentiel du système d’information (SI), documentant les actifs techniques, les applications, les infrastructures, les flux de données et leurs responsables, constitue un prérequis essentiel à la démarche d’analyse de risques RGPD. 
En s'appuyant sur les recommandations ANSSI , L’élaboration d’une cartographie du système d’information s’intègre à une démarche générale de gestion des risques, et notamment celle relative à la protection des données personnelles.

### Introduction – Le référentiel du Système d’Information comme prérequis à l’analyse de risques RGPD

Ce référentiel permet :

- d’assurer la traçabilité entre les traitements de données et les composants techniques qui les hébergent ou les manipulent ;

- de fiabiliser l’évaluation des risques en identifiant les vulnérabilités réelles du SI ;

- de faciliter la mise en œuvre de mesures de sécurité adaptées, conformément aux recommandations de la CNIL, de l’ANSSI et aux exigences de la norme ISO 27001.

Ainsi, le référentiel SI constitue le socle sur lequel repose la cartographie des traitements, l’analyse d’impact sur la vie privée (AIPD) et la gestion continue des risques liés à la protection des données personnelles.

| Référence                                          | Exigence liée au référentiel SI                                                |
| -------------------------------------------------- | ------------------------------------------------------------------------------ |
| **ISO 27001 / ISO 27005**                          | Inventaire des actifs, appréciation des risques, maîtrise du périmètre         |
| **ANSSI – Guide d’hygiène informatique**           | Connaissance et cartographie du SI, maîtrise des flux et dépendances           |
| **CNIL – Guide sécurité des données personnelles** | Connaissance des traitements, des flux et des supports techniques              |
| **RGPD (art. 30 & 35)**                            | Nécessité de décrire précisément les traitements et leurs contextes techniques |


### La cartographie du système d'information pour répondre aux recommandations de la norme Internationale (ISO 27001)
- Inventaire des informations et des autres actifs associés (A.5.09) ;
- Classification de l'information (A.5.12) ;
- La politique de sécurité de l’information dans les relations avec les fournisseurs (A.5.19) ;
- Réponse aux incidents liés à la sécurité de l'information (A.5.26) ;
- L’emplacement et la protection des matériels (A.7.08) ;
- La gestion des vulnérabilités techniques (A.8.08) ;
- La gestion des changements (A.8.32).

### La cartographie d’un système d’information est un atout pour la protection des données à caractère personnel 
- En cartographiant les éléments du système et leurs relations, il est plus facile de repérer les points de passage des données à caractère personnel. Ces points critiques peuvent inclure des serveurs, des bases de données, des traitements ou encore des interfaces. Il est possible de déterminer où les données sont manipulées et de les associer aux processus de l’organisation. Une fois identifiés, des mesures de protection telles que le chiffrement, l’anonymisation, la pseudonymisation ou les autorisations d’accès peuvent être adoptées ou renforcées.
- La cartographie permet de visualiser l’ensemble du système et de mieux comprendre comment les données circulent et sont stockées. Cela garantit que les données à caractère personnel sont protégées de manière adéquate, conformément à la réglementation en vigueur (articles 24, 26, 27, 28 et 44 du RGPD).
- En examinant la cartographie, on peut repérer les éléments du système qui sont les plus exposés aux risques de fuite de données. Par exemple, des interfaces mal sécurisées ou des connexions non chiffrées peuvent constituer des vulnérabilités menant à une violation de données. Une fois ces risques identifiés, des mesures de protection appropriées peuvent être mises en œuvre (articles 5(1)(f), 25(1) et 32 du RGPD).
- La cartographie d’un système d’information est un outil essentiel pour protéger les données à caractère personnel. Son référencement des acteurs, des processus, des applications, des services et des flux représente une source importante d’informations pour le DPD puisqu’il pourra les croiser avec celles qu’il a rassemblées dans le registre des traitements. L’établissement d’une cartographie constitue un argument fort dans le cadre de la mise en conformité d’une organisation. Elle permet de garantir la sécurité des informations sensibles, de communiquer clairement sur les mesures de protection mises en place et de démontrer les efforts de l’organisation en cas de contrôle de la CNIL.

### Bonnes pratiques

- Inventorier les actifs : applications, serveurs, bases, interconnexions, équipements réseau.

- Qualifier leur lien avec les traitements RGPD : quelles données personnelles sont traitées où ?

- Cartographier les flux de données internes / externes (API, transferts, sauvegardes).

- Attribuer des responsabilités (propriétaire, exploitant, responsable sécurité).

- Mettre à jour régulièrement le référentiel et le relier à la gestion des changements IT.

### Illustration avec un cas pratique 
  | Étape                                          | Objectif                                                             | Production attendue                                           | Références                            |
| ---------------------------------------------- | -------------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------- |
| **1. Constitution du référentiel SI**          | Identifier et décrire les composants techniques et les flux du SI    | Fiche d’actifs, schémas d’architecture, inventaire applicatif | ISO 27001 (A.5.9, A.8.1), ANSSI, CNIL |
| **2. Cartographie des traitements de données** | Relier les traitements RGPD aux éléments du SI concernés             | Registre des traitements, flux de données                     | RGPD art. 30, CNIL                    |
|             |

