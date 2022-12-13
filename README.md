# Créer un blog en Nextjs

## Introduction

Dans ce document, nous allons vous montrer comment créer un blog en Nextjs en utilisant des bases de données NoSql et de l'authentification. Nous allons utiliser Redis et Mongodb pour stocker et accéder aux données du blog, et Supabase pour gérer l'authentification des utilisateurs. En suivant les étapes décrites dans ce document, vous pourrez créer votre propre blog en Nextjs en utilisant des bases de données NoSql et de l'authentification.

## Les prérequis

- [Git](https://git-scm.com/)
- [VsCode](https://code.visualstudio.com/)
- [Nodejs](https://nodejs.org/en/)
- [Tailwindcss](https://tailwindcss.com/)
- [Redis](https://redis.io/)
- [Mongodb](https://www.mongodb.com/)
- [Supabase](https://supabase.com/)

## Les étapes

Voici les étapes de création d'un blog en Nextjs utilisant Redis, Mongodb et Supabase :

- Tout d'abord, il faut installer et configurer Redis, Mongodb et Supabase sur le serveur.
- Ensuite, dans le code de l'application Nextjs, il faut inclure les bibliothèques de Redis, Mongodb et Supabase pour pouvoir les utiliser.
- Il faut créer une connexion à la base de données Mongodb en utilisant l'API de Mongodb. Cette connexion sera utilisée pour accéder aux données du blog.
- Il faut initialiser Redis en utilisant l'API de Redis et configurer un cache pour stocker les données du blog.
- Il faut également initialiser Supabase en utilisant l'API de Supabase pour créer une connexion à la base de données Postgres. Cette connexion sera utilisée pour stocker les données de l'utilisateur du blog.
- Dans l'application Nextjs, il faut créer une interface utilisateur pour permettre à l'utilisateur de créer, lire, mettre à jour et supprimer les articles du blog.
- Pour chaque action effectuée sur l'interface utilisateur, il faut accéder aux données du blog en utilisant Redis comme cache et Mongodb comme base de données.
- Pour les données de l'utilisateur du blog, il faut utiliser Supabase pour stocker et gérer ces données.

En suivant ces étapes, vous pouvez créer un blog en Nextjs en utilisant Redis, Mongodb et Supabase pour gérer et accéder aux données.

## Les tutoriels

- [utiliser git](./git.md)
- [mongodb et redis](./Redis-Mongodb.md)
- [supabase](./supabaseOAuth.md)
- tailwindcss (soon)
- les effets (soon)
