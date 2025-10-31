---
title: C'est quoi le mieux, monolithique ou microservices ?
slug: cest-quoi-le-mieux-monolithique-ou-microservice
date: 2025-10-31 08:00:00+0000
image: cover.png
categories:
  - Dev
tags:
  - Architecture
  - Monolithique
  - Microservices
  - Choix technologique
draft: false
---

Vaste question que celle de choisir entre une architecture monolithique et une architecture microservices pour votre application.

Je vois beaucoup trop de startups ou de projets qui se lancent dans une architecture microservices sans vraiment comprendre les implications et les contraintes que cela implique.

Je vais vous donner mon avis sur le sujet, mais comme toujours, il n'y a pas de réponse universelle : tout dépend de votre contexte, de votre équipe, de votre produit, etc.

<!-- more -->

Avant d'aller plus loin, posons les bases.

## C'est quoi un monolithe ?

Un monolithe est une application développée en une seule pièce.  
Toutes les fonctionnalités de l'application sont regroupées dans un seul et même code source, déployé en un seul service.

## C'est quoi un microservice ?

Une architecture microservices découpe l'application en plusieurs petits services indépendants.  
Chaque service regroupe une fonctionnalité ou un domaine métier (ex : `payment-service`, `catalog-service`, etc.), communique avec les autres via une API ou de manière asynchrone via une [queue](https://en.wikipedia.org/wiki/Message_broker), et peut être développé ou déployé séparément.

## C'est quoi le mieux ?

Comme je le disais plus haut, il n'y a pas de réponse universelle.  
Mais je peux déjà te dire qu'un grand nombre de startups ont suivi la hype du microservice sans vraiment réfléchir à la question. *Spoiler alert* : ça ne s'est pas bien passé pour elles.

## Quelle architecture choisir ?

Avant tout, il faut comprendre les besoins réels de ton application.

Commence par un **monolithe** si :
- tu es une petite équipe,
- ton produit est simple,
- tu veux aller vite sur le marché.

Faire du monolithique ne veut pas dire faire du code spaghetti.  
Tu peux très bien concevoir un monolithe **bien structuré**, **bien découpé**, avec **de bonnes pratiques**. Ce sera plus facile à maintenir, à tester et à faire évoluer.  
Et surtout : le jour où tu auras besoin de scaler (spoiler : un monolithe scale très bien), tu pourras toujours extraire certaines parties vers des microservices.

Dans le cadre d'une startup, partir directement sur du microservice est souvent **overkill**.  
Tu n'as pas besoin de ça : tu as besoin de **tester ton idée rapidement**, de **pivoter facilement** et de **réduire la complexité au minimum**.

C'est une méthode pragmatique : tu commences simple.  
D'ailleurs, de grosses boîtes comme GitHub ou Doctolib ont longtemps tourné avec un monolithe (Doctolib vient tout juste d'annoncer sa [transition vers les microservices](https://www.linkedin.com/posts/julien-bideau_techtransformation-architecture-devops-activity-7295709538496745476-gR-t?utm_source=share&utm_medium=member_desktop&rcm=ACoAAAhzP9IBGbe_ar6eg4uw-FsxUL_d4hAo9EA)).

Quand ton application commence à rencontrer des problèmes de scalabilité — par exemple un domaine métier qui prend trop de charge ou qui a un cycle de déploiement différent —, tu peux **extraire ce domaine en microservice** tout en gardant le reste en monolithe.

L'idée, c'est de **ne pas complexifier ton architecture inutilement**, surtout au début.  
Oui, le monolithe c'est moins "sexy" que le microservice, mais c'est souvent le choix le plus judicieux pour une startup.

## Les inconvénients des microservices

Quelques points à ne pas négliger :

- **Complexité accrue** : plus de services = plus de communication inter-services, de gestion de versions, de déploiements…
- **Coûts opérationnels** : chaque service a besoin de son environnement, ce qui augmente les coûts d'infrastructure et de maintenance.
- **Latence** : les appels réseau entre services ajoutent de la latence.
- **Tests plus complexes** : il faut s'assurer que tous les services fonctionnent ensemble correctement.
- **Maintenance plus lourde** : gérer plusieurs services indépendants, leurs dépendances, leurs mises à jour de sécurité… ça finit par peser.

## Quand choisir les microservices ?

Les microservices prennent tout leur sens quand tu as des besoins **très spécifiques**.  
Par exemple, ton monolithe est en PHP, mais tu veux ajouter une fonctionnalité qui nécessite une autre techno plus adaptée (traitement d'image, vidéo, machine learning…).  
Tu peux alors extraire cette partie en microservice, dans la techno la plus adaptée.

Exemple concret :  
Dans ma dernière startup, nous avions un monolithe Spring Boot mal conçu (avec les joies qui vont avec : bugs, lenteurs, coûts de devs…).  
J'ai donc décidé de refaire une API v2 en Go/gRPC — choix pragmatique : j'étais plus productif en Go, et un dev de mon équipe était très motivé à apprendre le langage.  
Petit souci : impossible de trouver une lib HTML2PDF en Go qui gérait nos besoins.  
Résultat : j'avais prévu de faire un **microservice Java** dédié à la génération de PDF (léger, sans base de données, juste ce qu'il faut).

C'est là que réside la vraie force du microservice : **choisir la bonne techno pour le bon besoin**.  
Tu veux faire de l'IA ? Fais un microservice en Python ou en [Zig](https://ziglang.org/) avec [ZML](https://zml.ai/).

## En conclusion

Le choix entre monolithe et microservices dépend de ton contexte, de ton équipe et de ton produit.

Un monolithe bien conçu n'est **pas une prison** : tu peux toujours migrer vers du microservice petit à petit, **quand ton produit et ton équipe sont prêts** (ou pas).

Le mot d'ordre : **ne complexifie pas inutilement**.  
Tu n'as pas les mêmes besoins qu'une GAFAM.  
Et dans la plupart des cas, **le pragmatisme bat la hype**.
