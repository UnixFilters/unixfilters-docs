# Ajouter une commande

1. Dans le fichier [`exemple_checker/tests/gen/commands.py`](https://github.com/UnixFilters/checker/blob/main/exemple_checker/tests/gen/commands.py), ajouter la fonction de la commande.

Exemple : Pour ajouter la commande awk

```python title="commands.py"
def awk(arguments=None):
    run_command("awk", arguments=arguments)
```

## Remarque

La fonction doit être associée à un bloc dans l'interface, voir [Ajouter un bloc COMMANDE](./add_command_block.md)
