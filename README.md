# Anatoli
Server API Rest nodejs dockerized

## Installation:

Executer ces commandes:
```bash
git clone 
cd Anatoli
docker build . -t anatoli
```

Vérifié que l'images à bien été créé avec :
```bash
docker images
```

Lancer l'image avec la commande:
```bash
docker run -d -p 3000:3000 --name anatoli anatoli
```

Voir les conteneurs en fonctionnement:
```bash
docker ps
```


# Do it yourself

## Créer une API Rest Nodejs avec express

Commencez par créer un nouveau répertoire contenant tous les fichiers. Dans ce répertoire, créez un package.jsonfichier décrivant votre application et ses dépendances:

```json
{
  "name": "anatoli",
  "version": "1.0.0",
  "description": "Node.js on Docker",
  "author": "Aloïs HIAS",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.16.1"
  }
}
```

Avec votre nouveau package.jsonfichier, lancez npm install. Si vous utilisez la npm version 5 ou ultérieure,
cela générera un package-lock.jsonfichier qui sera copié dans votre image Docker.

Créez ensuite un server.jsfichier qui définit une application Web à l'aide de la structure Express.js :

```js
'use strict';

const express = require('express');

// Constants
const PORT = 3000;
const HOST = '0.0.0.0';

// App
const app = express();
app.get('/', (req, res) => {
  res.send('Hello Epsi, je ne sais pas mettre de quote dans un string\n');
});

app.listen(PORT, HOST);
console.log(`Running on http://${HOST}:${PORT}`);
```

Dans les étapes suivantes, nous verrons comment exécuter cette application dans un conteneur Docker 
à l'aide de l'image officielle de Docker. Tout d'abord, vous devez créer une image Docker de votre application.

## Création d'un fichier Docker

Créez un fichier vide appelé Dockerfile:
```bash
touch Dockerfile
```

Ouvrez le Dockerfiledans votre éditeur de texte préféré et y écrire:
```Dockerfile
FROM node:10

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./

RUN npm install
# If you are building your code for production
# RUN npm ci --only=production

# Bundle app source
COPY . .

EXPOSE 8080
CMD [ "node", "server.js" ]
```
## .dockerignore file
Créez un .dockerignorefichier dans le même répertoire que votre Dockerfile avec le contenu suivant:

```Dockerfile
node_modules
npm-debug.log
```
Cela empêchera vos modules locaux et les journaux de débogage d'être copiés sur votre image 
Docker et éventuellement de remplacer les modules installés dans votre image.





