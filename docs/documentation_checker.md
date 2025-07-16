# Documentation du checker

Ce projet permet d'évaluer le code envoyé depuis l'[interface](https://github.com/UnixFilters/unixfilters-franceIOI/tree/main), en comparant la sortie produite par le code avec une sortie attendue.

## Architecture

```bash
.
├── blocklyUnixFilters_lib.js
├── docs
│ ├── documentation_checker.md
│ └── documentation_checker.py
├── exemple_checker
│ └── tests
│  ├── copie de la librairie blockly
│  │ └── ...
│  ├── files
│  │ ├── test01.in # Fichier pris en entrée par le checker
│  │ ├── test01.out # JSON obtenu après exécution du code
│  │ └── test01.solout # Résultat attendu
│  └── gen
│    ├── checker.py # Logique permettant d'évaluer le score et renvoyer le feedback
│    ├── commands.py # Librairie exécutant les commandes
│    ├── livres.txt # Exemple de fichier d'entrée
│    └── solution.py # Contient le code généré par les blocs
├── index.css
├── index.html
├── jsongenerator.js
├── task.js
└── unixfilters.js
```
