---
title: Pourquoi vous devriez considérer gRPC ?
slug: pourquoi-vous-devriez-considerer-grpc
date: 2025-02-11 10:00:00+0000
image: grpc.png
categories:
  - Dev
tags:
  - gRPC
  - API
  - Rest
  - gRPC-Web
  - Protobuf
  - Protocol Buffers
draft: false
---

Pourquoi vous devriez considérer gRPC pour vos prochaines APIs ?

C'est quoi gRPC ? Pourquoi c'est pertinent pour vos APIs ? Quels sont les avantages et inconvénients de gRPC ?

Je vais essayer de répondre à ces questions !

Avant d'entrer dans le sujet, je pense qu'il est important d'ajouter un peu de contexte et de pragmatisme.

Pourquoi utiliser JSON comme format de donnée pour communiquer entre un serveur et un client ? Quel est l'avantage ?

J'ai beaucoup de mal avec le fait de faire des choses pas optimisées ou qui consomment beaucoup plus que nécessaire.

Dans le cadre d'une API qui est consommée par du code, pourquoi ne pas utiliser un format qui a le moins d'impact en termes de poids et de temps de parsing ? Protocol Buffers est parfait pour ça (il en existe d'autres, Thrift, Avro, etc...).

JSON ou XML n'a pas forcément de sens dans ce contexte.

C'est une chose importante en développement de choisir les bons outils en fonction de la situation.

Par exemple, utiliser Protocol Buffers comme fichier de configuration n'est pas pertinent, on peut, mais va t'amuser à écrire du binaire à la main...

Bref, retournons à notre sujet !

<!-- more -->

## gRPC c'est quoi ?

[gRPC](https://grpc.io/) est un framework RPC (Remote Procedure Call) créé et mis en open source par Google en 2016. C'est basé sur [HTTP/2](https://fr.wikipedia.org/wiki/Hypertext_Transfer_Protocol/2) et [Protocol Buffers](https://protobuf.dev/).

Ça a été conçu pour parler de machine à machine, mais ça peut être utilisé aussi pour des applications web et mobiles.

## Comment ça marche ?

gRPC est un framework qui support plusieurs langages nativement ou via des générateurs communautaire, il est basé sur Protocol Buffers pour décrire le contrat d'interface qui sera utilisé pour générer les modèles (`message`) et les services (`service`) clients et serveurs, le transport passe par HTTP/2 ce qui permet d'avoir du streaming bidirectionnel.

Exemple :

```protobuf
syntax = "proto3";

package acme.api.v1;

message CreateUserRequest {
  string email = 1;
  string password = 2;
}

message CreateUserResponse {
  bool success = 1;
}

service AcmeAccountService {
  rpc CreateUser(CreateUserRequest) returns (CreateUserResponse);
}
```

## Quel avantage comparé à REST ?

gRPC a plusieurs avantages comparé à REST, notamment : performance, sécurité (TLS par défaut), streaming bidirectionnel, multiplexage, génération de code, garantie de type, payload binaire (donc réduction de poids comparé à JSON), etc.

### Performance

Le fait d'utiliser HTTP/2 permet d'avoir une seule connexion pour plusieurs requêtes, ce qui permet d'avoir un gain de performance, surtout si vous avez beaucoup de requêtes à faire.

Protocol Buffers y est aussi pour quelque chose, le payload est plus léger que du JSON, donc moins de données à transmettre et le parsing est très rapide.

### Sécurité

gRPC utilise TLS par défaut, donc vous avez une connexion sécurisée entre le client et le serveur de base.

### Payload binaire

Le fait que le payload soit en Protocol Buffers est un avantage, mais peut être perçu comme un inconvénient...

La plupart des développeurs sont attachés au JSON et aux APIs REST qui est facile à lire ou a executé via des outils comme Postman, gRPC c'est du binaire... donc oublie l'onglet Network de ton navigateur pour voir les requêtes... tu peux, mais bon, tu ne verras que du binaire !

Mais c'est un faux problème, en fait comme tu as défini ton contrat d'interface en Protocol Buffers, tu as une documentation de ton API à jour, les clients et le serveur sont générés, donc pas de problème de compatibilité entre le client et le serveur, que ce soit en termes de mapping de nom de champ ou de type de donnée.

Si tu veux voir les données reçues, un simple point d'arrêt (ou un console.log/print du retour de la method du client) suffit pour avoir les données en clair.

Protocol Buffers vient aussi avec des inconvénients, par exemple, tu ne dois jamais changer le type d'un index.

Je m'explique, voici un exemple :

```protobuf
message MyPayload {
  uint32 year = 1;
}
```

Si tu changes en :

```protobuf
message MyPayload {
  string year = 1;
}
```

Tu crées un breaking change (tu auras le même problème avec JSON, si tes clients sont dans des langages fortement typés).

En Protocol Buffers, tu peux renommer les champs, mais le type et l'index doivent rester les mêmes.

Si tu dois gérer une évolution, tu rajoutes un nouveau champ avec un nouvel index, chaque index doit être unique dans un message.

```protobuf
message MyPayload {
  uint32 old_year = 1; // deprecated
  string year = 2;
}
```

Pour le versioning il y a une convention :

La structure doit être la suivante :

```
/proto/acme/api/v1/*.proto
```

Donc, tu peux facilement avoir une version 1 et une version 2 qui cohabitent.

Pour en savoir plus, je t'invite à lire cette documentation https://buf.build/docs/concepts/modules-workspaces/#workspace-layout

### Streaming bidirectionnel

Autre avantage de gRPC, c'est qu'avec une seule API, tu peux faire des requêtes simples ou en streaming, donc plus besoin de faire une API REST pour les requêtes simple et un WebSocket pour les requêtes en streaming ou ([SSE](https://fr.wikipedia.org/wiki/Server-sent_events)).

Tous passe par le même client !

Cependant, il y a une limitation, pour le moment les streams bidirectionnels ne sont pas totalement fonctionnel côté [gRPC-Web](https://grpc.io/docs/platforms/web/quickstart/), mais ça va arriver, ça a été priorisé dans leur [roadmap](https://github.com/grpc/grpc-web/blob/master/doc/streaming-roadmap.md) et ça utilisera [WebTransport](https://developer.mozilla.org/en-US/docs/Web/API/WebTransport)

Mais globalement, gRPC est utilisable sur le web.

### Multiplexage

Avec une même connexion, vous pouvez faire plusieurs requêtes, ce qui permet d'avoir de meilleures performances, la connexion reste ouverte comme en WebScokets.

### Génération de code

Si tu es développeur full stack ou simplement que tu touches au back et au front (pas forcément web) tu as dû être confronté au fait de devoir implémenter le modèle pour mapper la réponse de l'API dans chaque langage utilisé par les différents fronts (ts, js, swift, java/kotlin, ...), personnellement je fais beaucoup de Go et d'Angular (ts) et parfois du Swift, ça me prend un certain temps à devoir synchroniser ces modèles.

Avec la génération de code gRPC, je n'ai plus ce problème !

Note:

> Vous pouvez aussi utiliser des générateurs avec Swagger/OpenAPI pour des API REST, mais c'est moins intégré et surtout ça demande à ce que ton Swagger/OpenAPI soit très bien définie et à jour ou alors que tu l'utilises pour générer le serveur aussi, mais je n'ai jamais vu personne faire ça dans ma carrière, mais c'est possible de le faire.

gRPC utilise `protoc` pour générer le code des modèles (`message`) et des clients et serveurs (`service`), il existe des plugins pour générer le code dans les différents langages de programmation.

J'utilise [Buf](https://buf.build/) pour gérer ça, ça gère les dépendances via des plugins et ça permet de faire des vérifications de code (lint) et de générer le code (ça passe toujours par `protoc`).

Il est possible de rajouter un plugin pour faire de la validation de données avec [protoc-gen-validate](https://github.com/bufbuild/protoc-gen-validate/blob/main/README.md)

### Meilleur workflow pour l'équipe

Chez Angell, nous utilisions Protocol Buffers pour définir nos messages d'échange entre le mobile et le vélo via BLE et le vélo et le backend via MQTT, nos fichiers proto étaient dans un repo git, chaque modification passé par une PR et toute l'équipe concerné (embarqué et backend ou mobile et embarqué) pouvaient réfléchir et interagir sur les modifications a apporté et les contraintes que ça pouvait avoir dans leur contexte.

C'était une bonne chose de travailler sur un contrat d'interface, ça nous a facilité la vie au quotidien !

## Limitation

### Taille de chaque message

J'ai parlé de la limitation des streams sur le web, mais il y a d'autres limitations, par exemple la taille des payloads qui est limitée à 4 MB par défaut.

Cette limitation est une bonne chose, en informatique, il faut une limite à tout, sinon on se retrouve avec des problèmes de performance, de sécurité, etc.

Un exemple concret, si vous voulez envoyer un fichier (une image ?) de plus de 4 MB, la solution est simple : découper votre fichier en plusieurs morceaux et envoyer les morceaux un par un via un stream, c'est clairement plus compliqué qu'un simple POST sur un endpoint HTTP.

Exemple :

```protobuf
syntax = "proto3";

package acme.api.v1;

message UploadFileMetadata {
  string name = 1;
  bytes checksum = 2; // sha256
  string content_type = 3; // mime type, e.g. "image/jpeg"
  uint64 size = 4; // size in bytes
  uint64 number_of_chunks = 5;
}

message UploadFileChunk {
  uint64 index = 1;
  fixed32 crc = 2; // crc32
  bytes data = 3;
}

message UploadFileRequest {
  oneof request {
    UploadFileMetadata metadata = 1;
    UploadFileChunk chunk = 2;
  }
}

message UploadFileResponse {
  bool success = 1;
}

service AcmeFileService {
  rpc UploadFile(stream UploadFileRequest) returns (UploadFileResponse);
}
```

Le `oneof` permet de dire que le message `UploadFileRequest` peut-être soit un `UploadFileMetadata` soit un `UploadFileChunk`.

Donc, tu peux envoyer un premier message `UploadFileMetadata` avec les infos de ton fichier, ensuite tes morceaux de x MB avec leur checksum via `UploadFileChunk` une fois que tous les morceaux ont été reçus, le serveur te retourne une réponse `UploadFileResponse` qui termine le stream.

Note :

> Pense à tenir compte que ton message proto va avoir un poids, donc ne fait pas des morceaux de 4 MB.

C'est un peu plus compliqué, mais c'est faisable et ça permet de gérer des fichiers de plusieurs Go.

Après, tu peux aussi faire un endpoint HTTP classique sur ton API pour gérer l'envoi de fichiers.

### Gestion des erreurs

gRPC utilise des codes d'erreur standard.

Il y a des codes d'erreurs pour les erreurs de validation, d'authentification, de permission, etc.

- `INVALID_ARGUMENT`
- `NOT_FOUND`
- `ALREADY_EXISTS`
- `FAILED_PRECONDITION`
- `ABORTED`
- `OUT_OF_RANGE`
- `DATA_LOSS`

Voir la documentation des [status codes](https://grpc.io/docs/guides/status-codes/).

Tu peux aussi utiliser les détails pour ajouter des informations supplémentaires.

Google met à disposition un [package go](https://pkg.go.dev/google.golang.org/genproto/googleapis/rpc/errdetails) pour ça.

## Qui utilise gRPC ?

C'est évident, le premier à utiliser gRPC, c'est Google, l'[API de Google Cloud](https://github.com/googleapis/googleapis/tree/master) est entièrement définie en gRPC.

Note :

> Il existe un service qui permet de convertir une API gRPC en API REST, Google l'utilise. Il faut rajouter des attributs dans les fichiers proto et run un service supplémentaire qui sert de proxy.

Si vous utilisez le SDK Firebase, c'est aussi du gRPC, Zenly utilise aussi du gRPC, Netflix, etc.

## Conclusion

Très franchement, j'ai arrêté de faire des API REST, gRPC est objectivement plus adapté pour faire des APIs qui doivent être consommées par du code (en vrai, je ne connais aucune API à destination d'humain...).

Pourquoi consommer plus ? Quel est l'intérêt ?

En informatique, il n'y a pas de solution miracle qui marche dans toutes les situations. Cela dépend du contexte. Posez-vous la question de la pertinence et résistez à la hype.

Si votre application n'est qu'une application web et que vous n'avez pas besoin d'API, alors pourquoi partir sur une API ? HTMLX ou d'autres solutions sont toutes aussi pertinentes !
