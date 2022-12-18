[retour](../README.md)

# Self Hosted Supabase

## Docker

Voici les étapes générales pour héberger un conteneur Docker avec une image de Supabase :

1. Assurez-vous que vous avez installé Docker sur votre ordinateur. Si ce n'est pas le cas, vous pouvez le télécharger et l'installer à partir du site Web de Docker.
2. Ouvrez votre terminal et connectez-vous à votre compte Docker Hub en utilisant la commande docker login. Vous devrez entrer votre nom d'utilisateur et votre mot de passe Docker Hub pour vous connecter.
3. Téléchargez l'image de Supabase en utilisant la commande docker pull supabase/supabase-postgres:latest. Cette commande téléchargera la dernière version de l'image de Supabase dans votre ordinateur.
4. Exécutez le conteneur en utilisant la commande docker run -p 3000:3000 -p 5432:5432 supabase/supabase-postgres:latest. Cette commande démarrera le conteneur et exposera les ports 3000 et 5432 de votre ordinateur, ce qui vous permettra d'accéder à l'application Supabase et à la base de données PostgreSQL à partir de votre ordinateur.
5. Ouvrez votre navigateur et accédez à l'URL http://localhost:3000 pour vérifier que le conteneur est en cours d'exécution et que vous pouvez accéder à l'application Supabase.

Il est important de noter que ces étapes ne couvrent que les bases de l'hébergement d'un conteneur Docker avec une image de Supabase. Il existe de nombreuses autres options et fonctionnalités que vous pouvez utiliser pour configurer et personnaliser votre conteneur, en fonction de vos besoins et de votre utilisation prévue de Supabase.

## Kubernetes

Voici les étapes générales pour créer un conteneur Kubernetes avec l'image de Supabase :

1. Assurez-vous que vous avez installé kubectl sur votre ordinateur. Si ce n'est pas le cas, vous pouvez le télécharger et l'installer à partir du site Web de Kubernetes.
2. Créez un fichier de définition de conteneur (également appelé fichier YAML) qui décrit votre conteneur et ses paramètres de déploiement. Voici un exemple de fichier de définition de conteneur pour un conteneur Supabase :

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: supabase-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: supabase
  template:
    metadata:
      labels:
        app: supabase
    spec:
      containers:
      - name: supabase
        image: supabase/supabase-postgres:latest
        ports:
        - containerPort: 3000
        - containerPort: 5432

```

3. Enregistrez ce fichier de définition de conteneur sous le nom de supabase.yaml.
4. Ouvrez votre terminal et connectez-vous à votre cluster Kubernetes en utilisant la commande kubectl cluster-info.
5. Créez votre conteneur en utilisant la commande kubectl create -f supabase.yaml. Cette commande utilisera le fichier de définition de conteneur que vous avez créé pour créer un conteneur Supabase dans votre cluster Kubernetes.
6. Vérifiez que votre conteneur est en cours d'exécution en utilisant la commande kubectl get pods. Vous devriez voir un pod nommé supabase-deployment-XXXXX dans la liste des pods en cours d'exécution.
7. Exposez votre conteneur au monde extérieur en utilisant la commande kubectl expose deployment supabase-deployment --type=LoadBalancer --port=3000 --target-port=3000. Cette commande crée un LoadBalancer pour votre déploiement de conteneur, qui expose votre conteneur sur le port 3000 au monde extérieur. Le LoadBalancer redirige les requêtes entrantes vers le port 3000 sur votre conteneur, ce qui permet à vos utilisateurs d'accéder à votre application depuis l'extérieur de votre cluster Kubernetes. Cette commande est utile lorsque vous souhaitez rendre votre application accessible à vos utilisateurs ou à d'autres applications.
8. Créez votre conteneur en utilisant la commande kubectl create -f supabase.yaml. Cette commande utilisera le fichier de définition de conteneur que vous avez créé pour créer un conteneur Supabase dans votre cluster Kubernetes.
9. Vérifiez que votre conteneur est en cours d'exécution en utilisant la commande kubectl get pods. Vous devriez voir un pod nommé supabase-deployment-XXXXX dans la liste des pods en cours d'exécution.
10. Exposez votre conteneur au monde extérieur en utilisant la commande kubectl expose deployment supabase-deployment --type=LoadBalancer --port=3000 --target-port=3000. Cette commande créera un équilibreur de charge qui expose le port 3000 de votre conteneur au monde extérieur.
11. Vérifiez que votre conteneur est exposé en utilisant la commande kubectl get services. Vous devriez voir un service nommé supabase-deployment dans la liste des services exposés.
12. Accédez à l'application Supabase en utilisant l'adresse IP externe de votre équilibreur de charge. Vous devriez être en mesure d'accéder à l'application en ouvrant votre navigateur et en accédant à l'URL http://<EXTERNAL-IP>:3000.
  
Il est important de noter que ces étapes ne couvrent que les bases de la création d'un conteneur Kubernetes avec l'image de Supabase. Il existe de nombreuses autres options et fonctionnalités que vous pouvez utiliser pour configurer et personnaliser votre conteneur, en fonction de vos besoins et de votre utilisation prévue de Supabase.

## Hébergement

Il existe plusieurs options pour héberger gratuitement un conteneur Kubernetes avec l'image de Supabase :

- Utiliser un service de cloud computing gratuit qui offre une limite de temps d'utilisation gratuite, comme Google Cloud Platform ou Amazon Web Services. Ces services vous permettent de créer un cluster Kubernetes gratuitement pendant une période limitée, ce qui vous permet de tester votre application avant de décider de la passer en production.
- Utiliser un service de cloud computing spécialisé dans l'hébergement de conteneurs, comme Heroku ou OpenFaaS. Ces services offrent généralement une certaine quantité de temps d'utilisation et de stockage gratuits, ce qui vous permet de déployer votre application sans frais.
- Utiliser un service de cloud computing spécialisé dans l'hébergement de projets open source, comme GitHub Pages ou GitLab Pages. Ces services vous permettent de déployer votre application gratuitement sous forme de site statique, ce qui peut être suffisant pour certaines applications simples.

Il est important de noter que ces options gratuites peuvent avoir des limites en termes de performances, de scalabilité et de disponibilité, et qu'elles peuvent ne pas être adaptées à tous les projets. Si vous avez besoin de plus de fonctionnalités et de flexibilité, vous devrez peut-être opter pour un service d'hébergement payant.

### GitHub Pages
  
Voici les étapes à suivre pour héberger un conteneur Kubernetes sur GitHub Pages :

- Créez un dépôt GitHub et ajoutez votre code source à ce dépôt.
- Créez un fichier Dockerfile dans votre dépôt qui définit comment construire l'image Docker de votre application.
- Créez un fichier .github/workflows/build.yml dans votre dépôt qui définit un workflow GitHub Actions pour construire l'image Docker de votre application lorsque vous poussez du code dans votre dépôt.
- Créez un fichier kubernetes/deployment.yml dans votre dépôt qui définit un déploiement Kubernetes qui utilise votre image Docker.
- Créez un fichier kubernetes/service.yml dans votre dépôt qui définit un service Kubernetes qui expose votre déploiement sur un port public.
- Créez un fichier kubernetes/ingress.yml dans votre dépôt qui définit un ingress Kubernetes qui route les requêtes vers votre service en fonction de l'URL.
- Créez un fichier kubernetes/secrets.yml dans votre dépôt qui définit les secrets Kubernetes nécessaires pour accéder à votre cluster Kubernetes, comme les clés d'authentification et les jetons d'accès.
- Créez un fichier .github/workflows/deploy.yml dans votre dépôt qui définit un workflow GitHub Actions pour déployer votre application sur votre cluster Kubernetes lorsque vous poussez du code dans votre dépôt.
- Activez GitHub Pages pour votre dépôt et spécifiez l'URL de votre ingress Kubernetes comme URL de votre site.

Une fois ces étapes terminées, votre application devrait être accessible via l'URL de votre site GitHub Pages. Notez que cette méthode ne convient que pour les applications statiques ou les applications simples qui ne nécessitent pas de ressources importantes ou de hautes performances. Pour des applications plus complexes, vous devrez peut-être utiliser un service d'hébergement de conteneurs plus robuste.
