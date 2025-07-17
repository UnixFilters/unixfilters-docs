# Créer une catégorie

Actuellement, il existe 4 types de catégorie :

- Catégorie **Redirections** : Contient les différents symboles de redirection (<, >, >>)
- Catégorie **Entrée** : Contient un bloc d'entrée de texte
- Catégorie **Noop** : Contient les blocs no-operation, qui sont utilisés pour complèter chaque bloc lors du lancement de la commande
- Catégorie de **commande** : Il en existe autant qu'il existe de commande. Chaque catégorie contient la commande du même nom, ainsi que les options compatibles

Les catégories sont attribuées dès la création d'un bloc. Lorsque vous ajoutez une option, une commande, un noop, ou un symbole, sa catégorie est attribuée automatiquement lors de sa création.

Pour créer une nouvelle catégorie, dans le fichier [`public/blocklyUnixFilters_lib.js`](https://github.com/UnixFilters/unixfilters-franceIOI/blob/main/public/blocklyUnixFilters_lib.js), il faut :

## Ajouter la catégorie dans le contexte

Dans la variable localLanguageStrings, il faut ajouter le nom de la catégorie ainsi que le nom qui sera affiché dans l'interface.

**Exemple :**
Pour créer la catégorie test :

```javascript title="blocklyUnixFilters_lib.js"  hl_lines="5"
var getContext = function (display, infos, curLevel) {
  var localLanguageStrings = {
    fr: {
      categories: {
        test: "TEST",
```

Dans l'interface, la catégorie aura le nom `TEST`.

## Ajouter la catégorie dans `customBlocks`

Dans le namespace unixfilters, ajouter la catégorie.
Si la catégorie est remplie via une autre fonction, laisser un tableau vide. Sinon, ajouter le bloc à l'intérieur.

**Exemple :**

```javascript title="blocklyUnixFilters_lib.js" hl_lines="4 26"
context.customBlocks = {
  unixfilters: {
    // La catégorie test contient le block_test
    test: [
      {
        name: "block_test",
        blocklyJson: {
          message0: `%1 %2`,
          args0: [
            {
              type: "field_input",
              name: "PARAM_1",
              text: "a-z",
            },
            {
              type: "input_value",
              name: "PARAM_0",
            },
          ],
          output: null,
          colour: 165,
        },
      },
    ],
    // OU la catégorie test ne contient rien / est remplie lors de la création des blocs via une fonction
    test: [],
  },
};
```

## Ajouter une couleur de catégorie

**Exemple :**

```javascript title="blocklyUnixFilters_lib.js" hl_lines="4"
context.provideBlocklyColours = function () {
  return {
    categories: {
      test: 200,
    },
  };
};
```
