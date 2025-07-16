# Ajouter une commande

1. Dans le fichier [commands.py](https://github.com/UnixFilters/checker/blob/main/exemple_checker/tests/gen/commands.py), ajouter la fonction de la commande.

Exemple : Pour ajouter la commande awk

```python
def awk(arguments=None):
    run_command("awk", arguments=arguments)
```
