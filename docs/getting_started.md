# Getting started

## Prérequis

- Python 3.8+
- Node.js
- npm
- Git
- pip

## Mode développement

### unixfilters-franceIOI

Cloner le repo unixfilters-franceIOI

```bash
git clone https://github.com/waningcrescendo/unixfilters-franceIOI.git
```

Ajouter le repo bebras-modules dans le dossier public

```bash
cd unixfilters-franceIOI/public
git clone https://github.com/France-ioi/bebras-modules.git
```

Mettre en place l'environnement virtuel pour le serveur Python

```bash
cd ../python_lib
```

```bash
python3 -m venv venv
```

- Sur **Linux/macOS** :

```bash
source venv/bin/activate
```

- Sur **Windows** :

```bash
venv\Scripts\activate
```

Installer flask et lancer le serveur python dans un environnement virtuel

```bash
pip install flask-cors
```

```bash
python3 server.py
```

Dans un autre terminal, installer Node.js

- Sur **Linux** (Debian/Ubuntu) :

```bash
sudo apt update
sudo apt install nodejs npm
```

- Sur **macOS** :

  ```bash
  brew install node
  ```

- Sur **Windows** :

Télécharger et installer Node.js depuis [le site officiel](https://nodejs.org/).

Vérifier l'installation :

```bash
node -v
npm -v
```

Installer les dépendances

```bash
npm install
```

À la racine du projet, lancer le serveur node

```bash
node server.js
```

URL en développement : http://localhost:3000

### checker

En dehors du dossier unixfilters, cloner le repo

```bash
cd ..
```

```bash
git clone https://github.com/UnixFilters/checker.git
```

Dans le fichier [server.py](https://github.com/UnixFilters/unixfilters-franceIOI/blob/main/python_lib/server.py#L8), changer le chemin

```python
PATH_BASE = "CHEMIN" # Remplacer par le chemin vers le dossier tests du checker
PATH_GEN = os.path.join(PATH_BASE, "gen")
PATH_FILES = os.path.join(PATH_BASE, "files")
```

## Mode production

Ajouter les fichiers modifiés sur le SVN

## Suite de la documentation

- [Documentation fonctions](https://unixfilters.github.io/unixfilters-docs/)
- [Documentation checker](https://github.com/UnixFilters/checker/blob/main/docs/documentation_checker.md)
- [Mise en place d'une tâche](https://github.com/UnixFilters/unixfilters-franceIOI/blob/main/docs/init_task.md)
