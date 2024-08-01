# Microservices vs The World

## Introduction

Une architecture en microservices adopte une approche de développement dans laquelle une application est découpée en services indépendants qui peuvent être déployés de manière autonome.

> **Point architecture monolithique** : architecture en un seul bloc insécable, avec un seul serveur. Peu souple, cette architecture a tout de même ses avantages : simplicité, performance, facilité à débuguer, un monolithe est cohérent, efficace et facile à comprendre. Un monolithe peut necéssiter du scaling (scalabilité) horizontal (multiplier les instances d'un noeud) ou vertical (augmenter les ressources alouées à un noeud) mais cela est couteux, en particulier le scaling vertical qui demande toujours à être augmenté, ou source de bugs dans le cas du scaling horizontal où la duplication est source de problèmes.

> **Point architecture en couches**: L'architecture en couches propose un premier découpage et est plus intuitive, elle isole une partie des responsabilités. Les différentes couches (*présentation* (UI mais aussi controleurs, évolue beaucoup), *métier* (coeur, la plus importante, bouge très peu) et *persistance* (bdd, évolue pour des raisons d'optimisation)) manipulent le modèle.

Chaque architecture a ses avantages et ses inconvénients qu'une bonne phase de conception permet de prendre en compte.

## Comment fonctionne l'architecture en microservices

Cette architecture est basée sur la découpe en plusieurs process, plusieurs serveurs. Il s'agit de découper l'app en sous apps selon les besoins métiers et les ressources. 

Parce que les process sont isolés, ils sont leur cycle de vie propre et on peut les déployer là où on en a besoin.

    ex. On accorde beaucoup de CPU mais très peu de RAM à une machine qui a surtout besoin du CPU.

On peut aussi utiliser des langages différents selon les serveurs et, en général, gèrer plus finement les ressources. C'est une architecture particulièrement résiliente. 

### API Gateway et load balancer

De base, les différents process dialoguent via des appels d'API mais il est possible de simplifier les échanges en passant par une API Gateway (Passerelle API), sorte de proxy vers les microservices, le front ne communique alors plus qu'avec cette facade qui redistribue vers le back. 

    ex. NGINX ou Apache HTTP Server.

L'API Gateway permet un scaling horizontal local en dupliquant un service et en mettant en place un *load balancer* (répartiteur de charge).

Il est aussi possible de mettre en place une *queue* (Queue Messaging) pour faire communiquer des services. On y stocke les messages des différents services pour les traiter de façon asynchrone et assurer qu'ils soient effectivement traités (et ainsi éviter les risques de crash dûs à l'absence de réponse parce qu'un process est temporairement indisponible).

    ex. RabbitMQ, ActiveMQ, Apache Kafka.

### Single Point of Failure (SPOF)

Un point de défaillance de l'architecture qui, s'il tombe, met en danger l'intégrité de l'ensemble du système.

La queue peut être un SPOF car si les messages sont perdus, leur traitement n'est plus possible. Pareil pour l'API Gateway, sans ce lien, impossible de dialoguer.

D'où l'importance d'avoir des fallbacks, généralement un système de cache ou de petites BDD qui stockent des sources de vérité.

Il est essentiel de documenter les SPOF et d'envisager la préparation d'un Disaster Recovery Plan (DRP) si aucun fallback n'est possible.

## Pour résumer

L'architectue en microservices est performante, scalable, maintenable mais plus complexe et couteuse sur tous les plans (de la conception à la prod). Elle est donc à réserver aux projets qui ont vraiment besoin de ce genre de complexité.

Elle necéssite aussi un orchestrateur tel que Docker Compose ou Kubernetes.

En général, il est important de bien penser son architecture pour ne pas surdécouper et créer plus de requètes que necéssaire.

___

Pour les projets :
- Envisager plusieurs architectures et les documenter puis trancher sur une archi.
- En général, argumenter ses choix.
