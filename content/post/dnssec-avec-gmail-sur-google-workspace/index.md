---
title: Activer DNSSEC avec Gmail sur Google Workspace
slug: dnssec-avec-gmail-sur-google-workspace
date: 2023-02-23 00:00:00+0000
aliases:
  - /blog/dnssec-avec-gmail-sur-google-workspace
image: mecsa-result.png
categories:
  - Emailing
tags:
  - gmail
  - dnssec
  - google
  - workspace
  - google workspace
  - mx
  - dns
  - smtp
  - email
---

Si vous aussi, vous voulez configurer DNSSEC avec Gmail sur Google Workspace, vous êtes au bon endroit !

<!-- more -->

J'ai utilisé l'outil [mecsa](https://mecsa.jrc.ec.europa.eu/fr/) de la Commission Européenne pour vérifier que mon fournisseur de mail (Google Workspace) respectait bien les recommandations et bonnes pratiques en matière de sécurité.

Spoiler alert: Google Workspace ne respecte pas les recommandations de la Commission Européenne.

Je vais faire une série d'articles pour expliquer comment faire pour passer la totalité des recommandations de la Commission Européenne.

![Photo montrant le résultat du test mecsa.](mecsa-result.png)

## C'est quoi DNSSEC ?

DNSSEC est un protocole qui permet de sécuriser les requêtes DNS. Il permet de vérifier que les réponses DNS ne sont pas modifiées par un attaquant.

## Activer DNSSEC avec Gmail

Bien évidemment, il ne suffit pas de configurer DNSSEC sur votre domaine pour que ça passe le validateur de la Commission Européenne.

Je ne vais pas expliquer comment configurer DNSSEC sur votre domaine, je vous laisse regarder les différents articles sur le sujet en fonction de votre registre et de votre fournisseur de DNS (s'il est différent de votre registre).

Pourquoi ça ne suffit pas ? Parce que Gmail va envoyer les mails via son propre domaine (google.com) et non pas via votre domaine, donc google.com doit aussi avoir un enregistrement DNSSEC valide et ce n'est pas le cas.

Voici les MX officiels de Google Workspace :

```
aspmx.l.google.com
alt1.aspmx.l.google.com
alt2.aspmx.l.google.com
alt3.aspmx.l.google.com
alt4.aspmx.l.google.com
```

J'ai demandé à Google plusieurs fois de corriger ce problème, mais ils ne m'ont pas répondu.

Alors comment faire vu que je n'ai pas la main sur le domaine google.com ?

Il se trouve que Google fournit un domaine compatible DNSSEC, c'est documenté nul part, seules quelques personnes en parlent, au début, je me suis dit que c'était bizarre et que je ne pouvais pas utiliser ça en production, mais bon, je voulais absolument configurer DNSSEC avec Gmail sur Google Workspace, alors j'ai testé et ça fonctionne.

Voici les MX de Google Workspace compatibles DNSSEC :

```
mx1.smtp.goog
mx2.smtp.goog
mx3.smtp.goog
mx4.smtp.goog
```

J'ai fait plusieurs tickets au support Google Workspace, pour savoir si je pouvais utiliser ces MX, les personnes que j'ai eues n'étaient pas au courant de l'existence de ce domaine et me conseillaient d'utiliser les MX officiels de Google...

Après avoir insisté et expliqué que ces MX étaient la propriété de Google, la personne du support a fini par demander à l'équipe technique responsable du domaine google.com si je pouvais utiliser ce domaine.

La réponse est oui, vous pouvez utiliser ce domaine, mais il faut savoir que ça risque de poser un problème avec Google Workspace qui s'attend à d'autre MX que celui-ci.

Par exemple, si vous configurez un domaine secondaire et que vous rajoutez ces MX, vous ne passerez pas la validation de configuration de Google Workspace qui s'attend au MX officiel (normal).

Donc il faut toujours configurer les nouveaux domaines avec les MX officiels de Google Workspace, une fois la validation faite, vous pouvez changer ces MX sans problème, donc rien d'insurmontable.

Voilà pour ce premier article, je vais faire un article pour chaque recommandation de la Commission Européenne.
