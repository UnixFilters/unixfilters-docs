# Documentation du fichier `blocklyUnixFilters_lib.js`

## Description générale

Ce fichier définit les **blocs Blockly** pour simuler des **commandes Unix** (filtres) dans un environnement visuel, utilisé notamment avec `quickAlgo`. Il gère la configuration du contexte Blockly, les traductions locales, les blocs de commandes, les redirections et les options disponibles dans un style visuel éducatif.

---

## Sommaire

- [Fonction principale : `getContext`](#fonction-principale--getcontext)
- [Langues supportées](#langues-supportées)
- [Blocs de commandes Unix](#blocs-de-commandes-unix)
- [Blocs spéciaux](#blocs-spéciaux)

  - [Redirections (symbols)](#redirections-symbols)
  - [Noop (placeholders)](#noop-placeholders)
  - [Entrées](#entrées)

- [Création dynamique de blocs](#création-dynamique-de-blocs)

  - [`makeCommandBlock`](#makecommandblock)
  - [`makeGrepBlock`](#makegrepblock)
  - [`makeOptionBlock`](#makeoptionblock)
  - [`makeSymbolBlock`](#makesymbolblock)
  - [`makeNoopBlock`](#makenoopblock)

- [Utilitaires et comportement du contexte](#utilitaires-et-comportement-du-contexte)
- [Enregistrement de la librairie](#enregistrement-de-la-librairie)

---

## Fonction principale : `getContext`

Cette fonction initialise le **contexte Blockly** pour les filtres Unix.

### Responsabilités :

- Définir les blocs disponibles (cat, grep, sort, etc.)
- Gérer les traductions (actuellement uniquement le français)
- Gérer les événements d’affichage et le redimensionnement
- Nettoyer les blocs inutiles (`noop`) lors du survol de la souris

---

## Langues supportées

Actuellement, seul le **français** est configuré via `localLanguageStrings`. Les éléments traduits incluent :

- Les catégories (e.g. `cat`, `sort`)
- Les étiquettes de blocs
- Les messages de validation ou d’erreurs

---

## Blocs de commandes Unix

Définis dans la constante `COMMANDS`, chaque bloc correspond à une commande Unix courante :

| Commande | Description                                      | Format                         |
| -------- | ------------------------------------------------ | ------------------------------ |
| `cat`    | Concatène et affiche le contenu d'un fichier     | `cat [options] fichier`        |
| `sort`   | Trie les lignes d'un fichier                     | `sort [options] fichier`       |
| `head`   | Affiche les premières lignes d'un fichier        | `head [options] fichier`       |
| `cut`    | Extrait des colonnes spécifiques                 | `cut [options] fichier`        |
| `tail`   | Affiche les dernières lignes d'un fichier        | `tail [options] fichier`       |
| `tee`    | Duplique la sortie vers un fichier et la console | `tee [options] fichier`        |
| `tr`     | Remplace ou supprime des caractères              | `tr [options]`                 |
| `uniq`   | Supprime les lignes dupliquées adjacentes        | `uniq [options] fichier`       |
| `wc`     | Compte lignes, mots et caractères                | `wc [options] fichier`         |
| `sed`    | Éditeur de flux pour transformer du texte        | `sed [options] script fichier` |

---

## Blocs spéciaux

### Redirections (symbols)

Définis dans la constante `SYMBOL_NAMES` :

| Symbole                           | Couleur | Description                                     |
| --------------------------------- | ------- | ----------------------------------------------- |
| `>` (`symbol_greater_than`)       | 25      | Redirige la sortie vers un fichier              |
| `>>` (`symbol_even_greater_than`) | 90      | Ajoute la sortie à la fin d’un fichier existant |
| `<` (`symbol_less_than`)          | 50      | Lit les entrées depuis un fichier               |

### Noop (placeholders)

Définis dans `NOOP_NAMES`, utilisés comme blocs temporaires/inactifs :

- `noop_option_flag`
- `noop_option_field_index`
- `noop_command`
- `noop_text`

### Entrées

Un bloc de type texte (`text_input`) est défini pour injecter du texte brut ou un motif (regex, plage de caractères, etc.).

---

## Création dynamique de blocs

### `makeCommandBlock(commandArray)`

Crée dynamiquement les blocs pour chaque commande listée dans `COMMANDS`. Génère les blocs avec :

- `args0`: zone d’entrée
- `tooltip` : info-bulle avec usage
- Générateur de code pour Python et JavaScript

---

### `makeGrepBlock()`

Blocs personnalisés pour la commande `grep` :

- Contient un champ texte (`pattern`) et une entrée (`fichier`)
- Génère du code `grep(["pattern", ...args])`

---

### `makeOptionBlock(flag, type)`

Crée les blocs d’options pour les commandes, selon le type :

- `flag` → Option booléenne simple (`-n`, `-v`, etc.)
- `field_index` → Option avec argument (`-f 2`)

Les options sont associées aux commandes compatibles.

---

### `makeSymbolBlock(symbolArray)`

Crée les blocs de redirection (`<`, `>`, `>>`) avec une couleur et une info-bulle.

---

### `makeNoopBlock(noopArray)`

Crée des blocs "vides" (no-op) utilisés comme espace réservé ou suppression automatique par le système.

---

## Utilitaires et comportement du contexte

- `context.reset(taskInfos)` : réinitialise l’état de la simulation
- `context.resetDisplay()` : réinitialise l’affichage
- `context.updateScale()` : met à jour l’échelle (zoom) visuel
- `context.unload()` : nettoyage lors du changement de contexte
- `context.onChange()` : détection de changements dans l’interface Blockly
- `context.provideBlocklyColours()` : fournit les couleurs des catégories

---

## Enregistrement de la librairie

À la fin du fichier :

- Si `quickAlgoLibraries` est défini → enregistre la librairie via `quickAlgoLibraries.register("unixfilters", getContext)`
- Sinon → ajoute à `window.quickAlgoLibrariesList` pour enregistrement ultérieur

---

## Annexe : Types de blocs supportés

- Blocs de **commandes Unix**
- Blocs **symboliques** (redirection)
- Blocs **d’options** (`-n`, `-f`, etc.)
- Blocs **noop** (temporaires ou inactifs)
- Bloc **texte d’entrée**
