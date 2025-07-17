# Ajouter un bloc OPTION

Chaque option (comme `-c`, `-b`…) génère un bloc à partir d’une structure définie dans [`unixfilters.js`](https://github.com/UnixFilters/unixfilters-franceIOI/blob/main/public/unixfilters.js#L375).

Lorsque vous ajoutez une option, vous devez spécifier un **type**.

| Type          | Description                                                              | Exemple                                    |
| ------------- | ------------------------------------------------------------------------ | ------------------------------------------ |
| `flag`        | Pas de paramètre à remplir, juste un bloc avec une entrée et une sortie. | ![](../img/option_flag_example.png)        |
| `field_index` | Affiche un **input** pour saisir un numéro de champ ou un délimiteur.    | ![](../img/option_field_index_example.png) |

## 1. Générer le bloc

Pour que la librairie puisse générer ce bloc, il faut :

Dans le fichier `unixfilters.js`, ajouter l’option sous la commande dans [`optionTooltips`](https://github.com/UnixFilters/unixfilters-franceIOI/blob/main/public/unixfilters.js#L375).

**Exemple :** Pour ajouter l'option _inventée_ -x\[FIELD_INDEX\], il faut ajouter sa lettre (x), son type (field index) et son tooltip (indication qui sera affichée lorsqu'on passe la souris sur le bloc) avec la commande correspondante, on prend l'exemple de tail ici.

```javascript title="unixfilters.js"
const optionTooltips = {
  // Autres commandes
  tail: {
    n: {
      field_index: "tail : afficher les n dernières lignes (par défaut : 10)",
    },
    c: { field_index: "tail : afficher les n derniers octets" },
    x: { field_index: "tail : affiche x" }, // Ajout de la nouvelle option x
  },
};
```

Le bloc sera créé automatiquement grâce à la fonction [`makeOptionBlock`](https://github.com/UnixFilters/unixfilters-franceIOI/blob/main/public/blocklyUnixFilters_lib.js#L343).

## 2. Ajouter le bloc à la tâche

Pour que le bloc soit affiché dans la tâche, il faut dans le fichier [`task.js`](https://github.com/UnixFilters/unixfilters-franceIOI/blob/main/public/task.js), ajouter le nom du bloc.

Le bloc sera nommé ainsi : `option_<lettre>_<type>`où le type peut être flag/field_index.

**Exemple :**

```javascript title="task.js"
function initTask(subTask) {
    includeBlocks: {
        generatedBlocks: {
            unixfilters: [
                "option_x_field_index"
            ],
        },
...
```

## Catégorie

- Lorsque la boîte à outils est triée par catégorie : chaque option est affichée dans la catégorie de sa commande correspondante dans [`optionTooltips`](https://github.com/UnixFilters/unixfilters-franceIOI/blob/main/public/unixfilters.js#L375).

- Sinon : l'ordre du fichier correspond à l'ordre des blocs dans la boîte à outils.

## Remarque

Pour un bloc OPTION, il ne faut pas ajouter de label, de catégorie, de fonction de génération de code.
