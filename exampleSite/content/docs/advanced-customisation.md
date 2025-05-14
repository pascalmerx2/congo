---
title: "Atelier 0.1 checklist"
date: 2025-02-01
draft: false
description: "Learn how to build Congo manually."
summary: "Congo supports advanced customisations that include modifying the underlying Tailwind configuration, building the theme manually and providing custom CSS."
slug: "advanced-customisation"
tags: ["advanced", "css", "docs"]
---
## Step 1: Authentifier les utilisateurs
Définir un identifiant unique à chaque utilisateur.
Adopter une politique de mot de passe conforme à la recommandation CNIL
Obliger l'utilisateur à changer son mot de passe après réinitialisation.
Limiter le nombre de tentatives d'accès à un compte.

## Step 2: Gérer les habilitations
Définir des profils d'habilitations.
Tout compte utilisateur ou de service doit appartenir à un profil d’habilitation.
Un profil d'habilitation ne doit avoir accès qu'aux données strictement nécessaire à la réalisation de ses missions.
Supprimer les permissions des accès obsolètes.
Réaliser une revue annuelle des profils d'habilitations

## Step 3: Tracer les accès et gérer les incidents
Prévoir un système de logs d'accès.
Informer les utilisateurs de la mise en place d'un système de logs d'accès.
Protéger le système de logs de toute compromission ou d'altération des logs.
Prévoir les procédures pour les notifications de violation de données à caractère personnel.
Prévoir la durée de conservations maximale des logs.

## Step 4: Tracer les accès et gérer les incidents
Fermer tous les ports réseaux par défaut sur les serveurs ou containers. Ouvrir seulement les ports nécessaires

## Step 5: Sécuriser les applications web
Utiliser le protocole TLS 1.2+ pour toute communication interne ou externe.
Contrôler que les entrées des utilisateurs correspondent aux formats attendus

## Step 6: Sauvegarder et prévoir la continuité d'activité
Effectuer des sauvegardes journalières de manière complète ou incrémentale.
Tester la restauration des sauvegardes.
Stocker les supports de sauvegarde dans un endroit sûr.
Prévoir des moyens de sécurité pour le transport des sauvegardes afin d'assurer leur intégrité et leur confidentialité.
Prévoir et tester régulièrement l'interruption de services et leur résilience.

## Step 7: Archiver de manière sécurisée
Restreindre les accès aux données archivées aux seules personnes habilitées.
Limiter la conservation des données selon politique établissement 
Détruire les archives obsolètes et s'assurer de leur destruction

## Step 8: Archiver de manière sécurisée
Chiffrement des données au repos et en transit par défaut ç

## Step 9 : Utiliser des fonctions cryptographiques
Utiliser des algorithmes, logiciels et librairies reconnues
Conserver les secrets (mot de passe, token, clé de chiffrement, ...) dans un coffre-fort 

