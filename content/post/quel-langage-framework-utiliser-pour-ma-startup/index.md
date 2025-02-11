---
title: Quel langage/framework utiliser pour ma startup ?
slug: quel-langage-framework-utiliser-pour-ma-startup
date: 2025-02-11 20:20:00+0000
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

Vous avez une idée de startup et vous vous demandez quel langage/framework utiliser pour développer votre projet ? C'est une question que l'on se pose tous au début.

Malheureusement, il n'y a pas de réponse universelle à cette question. Le choix du langage/framework dépend de nombreux facteurs, tels que le type de produit que vous souhaitez développer, les compétences de votre équipe et des développeurs disponibles sur le marché, la maturité de la technologie, etc.

Dans cet article, je vais essayer de vous donner quelques pistes pour vous aider à faire le bon choix (non) et surtout les choses à ne pas faire.

<!-- more -->

Si vous vous dite tiens je vais utilisé le dernier framework a la mode, c'est trop cool, tout le monde en parle, c'est le futur !

Ce n'est pas une bonne idée, car vous allez devoir apprendre ce nouveau lagage/framework, c'est cool d'apprendre de nouvelles choses, mais quand on monte une startup ou n'importe quel projet, en générale on n'a pas le temps de monté en compétence sur un nouveau langage/framework.

> Pour un side project, clairement il faut découvrir de nouvelle choses, c'est l'occasion a moins que ce side project à pour objectif a devenir un produit et donc une startup.

Il faut allez vite, est surtout testé au plustot votre idée, pour voir si elle est viable ou non, le fameux [Product-Market Fit](https://lehub.bpifrance.fr/comment-valider-son-product-market-fit-sans-y-laisser-30ke/#:~:text=En%20fran%C3%A7ais,%E2%80%9Dproduit%20/%20march%C3%A9%E2%80%9D.).

Il faut donc utilisé des technologies que vous maitrisé, que vous avez déjà utilisé dans le passé, que vous avez déjà déployé en production.

Voila article terminé, au revoir !

Malheureusement, ce n'est pas si simple :) Il y a d'autres facteurs à prendre en compte, tels que :

- Le marché : combien de développeurs maitrisent ce langage/framework ? Si vous avez besoin de recruter, il sera plus facile de trouver des développeurs si vous utilisez des technologies populaires.
- La communauté : est-ce que le langage/framework a une communauté active ? Si vous avez des problèmes, il sera plus facile de trouver de l'aide.
- La documentation : est-ce que la documentation est à jour et de qualité ? C'est important pour gagner du temps lors du développement.
- Les frameworks disponibles : est-ce qu'il existe des frameworks qui répondent à vos besoins ? Par exemple, si vous développez une application web, il est préférable d'utiliser un framework web plutôt que de tout faire à la main.
- Votre motivation : Je comprends que tu ne vaux pas faire ton nouveau projet en PHP ou Python et que tu aimerais testé de nouvelle choses, c'est contratictoire avec ce que je dit plus haut, mais c'est un facteur a prendre en compte aussi.

Si vous maitrisez un langage exotique (par exemple Haskell), pas sur que se soit une bonne idée, posez vous la question, est-ce que je vais trouver facilement des développeurs pour m'aider a développé mon produit ?

Note :

> Je n'ai rien contre Haskell, c'est le premier langage qui met venu en tête, mais vous pouvez le remplacer par n'importe quel langage un peu de niche (Brainfuck ?).

Il existe vraiment beaucoup de langages/frameworks, encore une fois il n'y a pas de réponse universelle à cette question.

Mais restez pragmatique et adapter votre choix en fonction de votre contexte, par exemple :

Vous n'allez pas faire du développement embarqué en PHP pour un satelite ?

Vous n'allez pas faire du développement web en C ([Leboncoin la fait...](https://javaetmoi.com/wp-content/uploads/2019/04/2019-04-18-Du-monolithe-aux-microservices-chez-leboncoin.pdf), Google aussi, je n'est plus la source) ?

C'est possible, mais c'est pas le plus adapté, pour différente raison, les frameworks web apporte beacoup de choses, templating, routeur, acl, query builder, orm (ça fera surement l'objet d'un article ça...), etc.

Vous n'allez pas codé un proxy HTTP en PHP/Ruby ou Python ? c'est possible, j'ai déjà fait un serveur HTTP en PHP... c'étais amusant... mais serieusement ça ne peut pas partir en prod.

Il existe des contre exemple à ça, Algolia, a la base c'étais de la recherche offline sur mobile, je ne me rappel plus du langage utilisé, mais je crois que c'étais du C/C++ (n'hesité pas a me corrigé !) comme le monde mobile à cette epoque été limité en terme de ressource, le code devait être le plus optimisé possible et le plus light, leur premier produit n'a pas trouvé son marché et ils ont pivoté pour devenir ce qu'ils sont aujourd'hui, mais basé toujours sur leur technologie de recherche, vous imaginez bien que le code capable de tournée sur un smartphone de 2012 est bien plus performant coté serveur, et c'est ce qui fait leur force aujourd'hui.

Moi même je fait tous mes side projects en Go, par ce que c'est le langage ou je suis le plus productif et celui qui me motive le plus, mais parfois, je me dit qu'il n'est pas forcément adapté à tous les besoin, par exemple ma femme à une idée de site web, un site classique (une sorte de site d'annonce), est-ce que je vais faire ça en Go et gRPC avec un front en SPA ? Non (oui ça mets passé par la tête), j'ai finalement réfléchi et je me dit que faire ça en PHP/Symfony serais surement plus pertinant (j'en ai fait pendant longtemps), ou alors peut-etre en Go et HTMLX, c'est plus moderne et ça m'évite de devoir faire une API et un front séparér ou de refaire du PHP.

Il n'y a pas de contrainte de temps, c'est vraiment un side project, donc pourquoi pas.

J'en ai déjà parlé dans mon article sur [gRPC]({{< ref "/post/pourquoi-vous-devriez-considerer-grpc/" >}}), je n'aime pas consommé plus que naissaire, surement mon coté écolo... nous développeur on à souvant des machine surpuissante, on ne se rend pas compte de l'impact de nos choix technologique sur des clients plus modeste.

Il est important de prendre en compte tous ces facteurs, est-ce que votre client cible est plus Android premier prix ou iPhone 16 Pro Max ? Est-ce qu'une SPA de 15Mo de js est acceptable pour votre client cible ? Est-ce que votre client cible a une connexion internet stable et rapide ?

J'ai malheureusement vu plusieurs fois des choix fait par des développeurs qui on simplement choisi une techno parce qu'ils y avait une hype autour, sans se poser la question de l'impact sur le produit final.

J'ai quelques exemples, en voici un :

Une startup est parti sur un choix qui semblé bien au début, Hasura, c'étais cool, pas besoins de codé un serveur GraphQL, les développeurs front pouvais directement faire des requêtes GraphQL, mais le produit final était lent, très lent, le temps de réponse était de plusieurs secondes (voir minutes...), c'étais inacceptable pour une application web, en fait Hasura génére les requêtes SQL (tu vois le problème ?), il n'y avais aucune maitrise sur les requêtes généré, ça sorté des requêtes de plus de 1000 km de long (oui c'est un peux exagéré), j'ai vu une requête qui avais mis plus de 6 heurs... on a finalement kill la requête.

La base de donnée été a plus de 85% de CPU usage (c'étais un serveur de 24 cors et 128Go de ram...) pour environs 400 clients (je simplifie pour des questions d'anonymat).

Bien sur c'est plus complexe que ça, mais ça montre une chose, mettez en prod uniquement des choses que vos équipe maitrisé et que vous avez testé en condition réel.

Je vous rassur ça mets arrivé aussi de proposé des solutions qui me paraissé cool et je n'avais jamais mis ça en prod, j'ai eu quelque surprise, mais rien de grave, j'ai appris de mes erreurs.

Donc en résumé :

- Utilisé des technologies que vous maitrisé
- Utilisé des technologies qui répondent à vos besoins
- Ne cédez pas à la hype, soyez pragmatique !
- Assurez-vous que la technologie est suffisamment mature pour être utilisée en production (documentation, communauté, nombre de développeurs, etc.)

> Petit rappel : on optimise uniquement a la fin, si vous n'avez pas de client, ça ne sert a rien d'optimisé, vous allez perdre du temps et de l'argent pour rien.

Bien sur si vous avez la capacité et que ça n'ajoute pas un sur coût, pourquoi pas, mais ne le faite pas en priorité.

Par exemple partir sur du [gRPC à la place d'une API REST]({{< ref "/post/pourquoi-vous-devriez-considerer-grpc/" >}}) :)
