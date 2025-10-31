---
title: Quel langage/framework utiliser pour ma startup ?
slug: quel-langage-framework-utiliser-pour-ma-startup
date: 2025-10-31 08:20:00+0000
image: cover.png
categories:
  - Dev
tags:
  - Langage
  - Framework
  - Startup
  - Choix technologique
draft: false
---

Vous avez une idée de startup et vous vous demandez quel langage ou framework utiliser pour développer votre projet ?  
C'est une question que tout le monde se pose au début.

Malheureusement, il n'y a **pas de réponse universelle**. Le choix dépend de nombreux facteurs : le type de produit, les compétences de votre équipe, la disponibilité de développeurs sur le marché, la maturité de la techno, etc.

Dans cet article, je vais essayer de vous donner quelques pistes pour faire le bon choix (ou au moins éviter les mauvais).

<!-- more -->

## Le piège du "dernier framework à la mode"

Si vous vous dites *« tiens, je vais utiliser le dernier framework hype, tout le monde en parle, c'est le futur ! »*,  
mauvaise idée.

Apprendre un nouveau langage ou framework, c'est cool.  
Mais quand on monte une startup, on n'a **pas le temps de monter en compétence** sur une techno qu'on ne maîtrise pas encore.

> Pour un side project, foncez, c'est fait pour ça !  
> Mais si ce side project a vocation à devenir un produit, donc une startup, ce n'est plus le même contexte.

## Allez vite, testez tôt

L'objectif, c'est d'aller vite et de tester votre idée le plus tôt possible — pour valider (ou non) le fameux [Product-Market Fit](https://lehub.bpifrance.fr/comment-valider-son-product-market-fit-sans-y-laisser-30ke/#:~:text=En%20fran%C3%A7ais,%E2%80%9Dproduit%20/%20march%C3%A9%E2%80%9D.).

Donc utilisez des technologies que **vous maîtrisez déjà**, que vous avez déjà déployées en production, et avec lesquelles vous êtes productif.

Mais bien sûr, ce n'est pas aussi simple :)

## Les autres facteurs à prendre en compte

- **Le marché** : combien de développeurs maîtrisent cette techno ? Si vous devez recruter, c'est un point clé.  
- **La communauté** : est-elle active ? Trouver de l'aide rapidement, c'est vital.  
- **La documentation** : à jour, claire et complète ? Vous gagnerez du temps.  
- **Les frameworks disponibles** : existe-t-il déjà un framework adapté à vos besoins ?  
- **Votre motivation** : oui, c'est important aussi. Si une techno vous démotive, vous tiendrez pas longtemps.

Si vous maîtrisez un langage exotique (disons Haskell), demandez-vous si vous trouverez facilement des devs pour vous aider à faire grandir votre produit.

> Je n'ai rien contre Haskell — c'est juste le premier qui m'est venu en tête.
> Remplacez-le par n'importe quel langage confidentiel (Brainfuck, par exemple, mais là on est dans le sport extrême).

## Le bon sens avant tout

Restez pragmatique :  
vous n'allez pas faire du développement embarqué en PHP pour un satellite, ni du développement web en C (quoique [Leboncoin l'a fait](https://javaetmoi.com/wp-content/uploads/2019/04/2019-04-18-Du-monolithe-aux-microservices-chez-leboncoin.pdf)... et Google aussi).

C'est *possible*, mais pas adapté. Les frameworks web apportent déjà beaucoup : templating, routeur, ACL, ORM, etc.

Et non, vous n'allez pas coder un proxy HTTP en PHP ou en Ruby (même si, avouons-le, on l'a tous fait "pour voir").  
J'ai moi-même écrit un petit serveur HTTP en PHP. C'était amusant. Mais pas productif.

## Les contre-exemples (ou presque)

Algolia, par exemple.  
À la base, c'était un moteur de recherche *offline* pour mobile, probablement écrit en C ou C++ (corrigez-moi si je me trompe).  
Leur code devait être ultra léger et performant pour tourner sur les smartphones de 2012.  
Quand ils ont pivoté vers une solution serveur, ils avaient une base ultra optimisée — et c'est toujours ce qui fait leur force aujourd'hui.

## Mon cas personnel

Moi, je fais tous mes side projects en Go, parce que c'est le langage où je suis le plus productif et celui qui me motive le plus.

Mais ce n'est pas toujours le plus adapté.  
Par exemple, ma femme a une idée de site d'annonces. Est-ce que je vais faire ça en Go et gRPC avec un front SPA ?  
Non (enfin… j'y ai pensé).  
Finalement, je me dis qu'un bon vieux **PHP/Symfony** serait plus pertinent — ou peut-être du **Go + HTMX**, histoire d'éviter une API séparée.

C'est un side project, sans contrainte de temps, donc je peux me le permettre.

J'en parlais d'ailleurs dans mon article sur [gRPC]({{< ref "/post/pourquoi-vous-devriez-considerer-grpc/" >}}) :  
je n'aime pas consommer plus que nécessaire — sûrement mon côté écolo.  
On a tous des machines surpuissantes, et on oublie souvent l'impact de nos choix techno sur les utilisateurs finaux.

Est-ce que votre client cible a une bonne connexion ?  
Est-ce qu'il est sur un Android premier prix ou un iPhone 16 Pro Max ?  
Est-ce qu'une SPA de 15 Mo de JS est raisonnable pour lui ?

## La hype, le vrai danger

J'ai vu plusieurs fois des projets partir dans le mur à cause d'un choix fait “par hype”.

Un exemple concret : une startup partie sur **Hasura**.  
Au début, tout semblait parfait : pas besoin de coder de backend, les devs front pouvaient interroger directement la base via GraphQL.  
Mais en prod… l'horreur.

Requêtes SQL générées automatiquement, monstrueuses, incontrôlables.  
Des temps de réponse de plusieurs secondes (voire minutes).  
Une requête a même tourné **plus de 6 heures** avant qu'on la kill.  
Le serveur SQL (24 cœurs, 128 Go de RAM) était à 85 % de CPU constant pour 400 clients.  
Autant dire : pas tenable.

Moralité : **ne mettez en prod que ce que vous maîtrisez**. Et testez en conditions réelles.

Je ne jette pas la pierre, je me suis aussi fait piéger par des technos “prometteuses”.  
Mais on apprend vite à devenir méfiant.

## En résumé

- Utilisez des technos que vous maîtrisez.  
- Choisissez celles qui répondent à vos besoins réels.  
- Ne cédez pas à la hype.  
- Vérifiez la maturité (communauté, docs, stabilité).  
- Et surtout : restez pragmatique.

> Rappel : on optimise **à la fin**.  
> Si vous n'avez pas de clients, optimiser ne sert à rien — vous perdez du temps et de l'argent.

Bien sûr, si vous pouvez optimiser sans surcoût, allez-y.  
Mais sinon, concentrez-vous sur l'essentiel : **faire un produit qui marche**.

Et si vous tenez absolument à expérimenter… faites-le sur un side project, pas sur votre cœur de business 😉

