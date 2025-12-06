# 3. Système d’e-mails asynchrones (Redis + Queue)

Pour l’inscription utilisateur, l’envoi des e-mails se fait en arrière-plan grâce à Redis.

## 3.1. Principe

Lors du POST /auth/signup, le backend :

crée l’utilisateur avec isVerified = false

génère un token de vérification stocké en base

push un job dans une file Redis (queue) avec l’adresse e-mail, le sujet et le contenu

Un worker séparé lit la queue Redis et envoie réellement les e-mails
(e-mail de vérification puis e-mail de bienvenue).

Avantages :

API plus rapide (l’envoi d’e-mail ne bloque pas la requête)

système scalable

meilleure architecture (API ≠ worker)

## 3.2. Prérequis Redis

Installer Redis en local ou utiliser Docker :


## 3.3. Démarrer Redis en local (Windows)

Sur Windows, il faut démarrer Redis manuellement :

Ouvrir un terminal dans le dossier où se trouve redis-server.exe
(ex : C:\redis).

Lancer le serveur Redis :

redis-server.exe