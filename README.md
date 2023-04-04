# Story API Rest

Cette application est une API réalisée avec Node.js.

## Etapes:

### Cloner le repository git
Pour récupérer le projet sur votre machine, vous pouvez utiliser la commande suivante:
```bash
git clone https://github.com/othbel/node-api.git
```

### Publier l'image Docker sur Docker Hub
Pour déployer l'application avec kubernetes, l'image Docker doit être disponible sur un registry. Pour publier l'image Docker, il faudra *build* l'image sur votre machine avant, vous pouvez utiliser les commandes suivantes pour *build* et publier l'image:
```bash
docker build -t <DockerID>/node-api:<tag> .
docker push <DockerID>/node-api:<tag>
```

### Déployer l'application avec K8s
Les fichiers **YML** sont dans le dossier ressources du repository. N'hésitez pas à modifier les limites de ressources selon votre machine.

```bash
kubectl apply -f ressources/config.yml,ressources/deployment.yml,ressources/service.yml
```

### Exposer l'API avec minikube
Afin d'avoir accès à l'api, vous pouvez utiliser le tunnel LoadBalancer de Minikube.
```bash
minikube service api-node-service
```


### Tester l'API

Pour tester l'API, il faut utiliser un client REST type Postman afin de réaliser des requêtes POST vers `/story` avec un **JSON** dans le body de la requête contenant comme attribut **text** et une valeur de type **string**. Ex: {"text": "mon texte"}.
Pour récupérer le contenu d'un fichier d'histoire, il suffit d'utiliser le même endpoint `/story` mais cette fois-ci en **GET**.
Pour crasher l'application, une requête GET vers `/error` plantera l'application.