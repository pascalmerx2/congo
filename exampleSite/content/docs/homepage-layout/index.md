---
title: "securisation site web"
date: 2020-08-13
draft: false
description: "etude de cas"
slug: "homepage-layout"
tags: ["homepage", "layouts", "docs"]
---

Étude de cas : sécurisation d'une application web pour la gestion des ressources humaines

Une entreprise de taille moyenne nommée ESDown opérant dans le secteur des technologies de l'information a récemment développé une application web interne pour la gestion des ressources humaines. Cette application est destinée à stocker et gérer des données personnelles sensibles telles que les informations de contact des employés, et d’aider à la gestion des rémunérations et performances des collaborateurs de l’organisation. Étant donné la nature des données traitées, la sécurité de cette application est une priorité majeure pour l'entreprise.
Bien que l'entreprise dispose d'une équipe de sécurité des systèmes d'information compétente, elle reconnaît le besoin d'une approche structurée et collaborative pour identifier et gérer les risques associés à l'application web. Le défi est de s'assurer que l'application est bien protégée contre les menaces externes et internes, tout en garantissant la conformité avec les réglementations sur la protection des données.

Atelier 1 : cadrage et socle de sécurité

Rappels :
    Valeur métier (VM) : toute ressource qui a de la valeur pour l'organisme et qui est nécessaire à la réalisation de ses objectifs (données, processus, fonctions) 
    Bien de support (BS) : composante du système d’information sur laquelle reposent une ou plusieurs valeurs métier. Un bien support peut être un logiciel, matériel, réseau, une personne, etc.
    Événements redoutés (ER) : ils correspondent à une situation défavorable qui affecte une ou plusieurs valeurs métiers. Cela peut englober l'interruption d'un service, la divulgation non autorisée d'informations sensibles, ou des altérations indésirables dans une base de données 
    Impact (IP) : sens juridique pour un PIA

Question à se poser : quels sont les scénarios que l’entreprise redoute (événements redoutés) ?
    - VM : Données personnelles
    - ER : Divulgation de données, perte de données
    - IP : Juridique, réputation, financier

Question à se poser : quel est l’existant en matière de sécurité de l’information (socle de sécurité) ?
     - Un DPD (Délégué à la Protection des Données) est nommé dans l’entreprise, il travaille sur le sujet. Nous avons besoin de son retour


Atelier 2 : sources de risque

Rappels :
    Source de risque (SR): élément, personne, groupe de personnes ou organisation susceptible d’engendrer un risque. Exemple : services étatiques, hacktivistes, concurrents, employés vengeurs ;
    Objectif visé (OV) : finalité visée par une source de risque, selon ses motivations. Exemple : voler des informations à des fins lucratives ou d’espionnage industriel, diffuser un message idéologique, se venger d’un organisme, générer une crise sanitaire ;
    Motivation : motivation de la source de risque à atteindre son objectif ;
    Ressources : ressources financières, compétences, infrastructures d’attaque.

Question à se poser : quels sont les sources de risques et leurs objectifs visés ? Quel est le niveau de pertinence pour chaque groupe SR/OV ?
   - Cybercriminels, hackers  : valeur métier "données personnelles"
   - Employés malintentionnés : valeur métier "données personnelles"

Commentaire : Il est noté que le cybercriminel serait potentiellement plus intéressé par la valeur métier « Données personnelles » alors que « l’employé malintentionné » sur l’ensemble des valeurs métiers (« Données personnelles » et « Dossiers de performance et rémunération ») pour du sabotage.


Atelier 3 : scénarios stratégiques

Rappels :
    Partie prenante : élément (personne, système d’information, organisation) en interaction directe ou indirecte avec l’objet de l’étude. Exemple : partenaire, prestataire, client, fournisseur, etc.
    Écosystème : ensemble des parties prenantes en interaction avec l’objet de l’étude ;
    Scénario stratégique : ensemble de chemins d'attaque possibles qu'une source de risque pourrait suivre pour atteindre un objectif. Ce chemin peut impliquer des interactions avec les parties prenantes au sein de l'écosystème, ou peut directement cibler les valeurs métier ;
    Dépendance : le niveau de dépendance représente l'importance vitale de la relation avec une partie prenante pour le succès de l'activité ;
    Pénétration : le niveau de pénétration indique la mesure dans laquelle une partie prenante a accès aux ressources internes de l'organisation ;
    Maturité cyber : le niveau de maturité cyber évalue les capacités de la partie prenante en matière de sécurité des systèmes d'information ;
    Confiance : le niveau de confiance mesure à quel point les intentions ou les intérêts de la partie prenante sont alignés ou contraires aux objectifs de l'organisation.

Question à se poser : quelles sont les parties prenantes (fournisseurs, clients, partenaires) dans notre écosystème et sont-elles menaçantes pour l’organisation ?
Question à se poser : quels sont les scénarios d'attaque envisageables ? Quels chemins peuvent être empruntés par les sources de risque ?
    Le cybercriminel attaque l'hébergeur pour obtenir les données personnelles et les dossiers de performance et de rémunération.
    Le cybercriminel qui attaque en direct les systèmes pour obtenir les données personnelles et les dossiers de performances et rémunération.
    Employé mal intentionné qui est déjà à l’intérieur de l’entreprise et qui attaque les données personnelles et les dossiers de performance et de rémunération.
    Employé mal intentionné qui passe par les postes des développeurs freelances et qui attaque les données personnelles et les dossiers de performance et rémunération.

Atelier 4 : Scénarios opérationnels

Rappels :
    Scénario opérationnel : enchaînement d’actions malveillantes portées sur les biens supports de l’objet étudié ou de son écosystème.

Question à se poser : quels sont les scénarios techniques (modes opératoires) possibles sur les chemins d’attaque (atelier 3) ?

Atelier 5 : traitement du risque

Rappels :
    Risque initial : scénario de risque évalué avant application de la stratégie de traitement du risque. Cette évaluation repose sur la gravité et la vraisemblance du risque ;
    Risque résiduel : scénario de risque subsistant après application de la stratégie de traitement du risque. Cette évaluation repose sur la gravité et la vraisemblance du risque.

Question à se poser : quels sont les scénarios de risque (récapitulatif) ?
