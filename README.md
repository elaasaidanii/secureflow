# SecureFlow

Pipeline DevSecOps réutilisable pour GitHub Actions. Un dépôt l'appelle en quelques lignes de YAML et obtient les contrôles de sécurité centralisés.

**Statut : en cours de développement.**

## Contrôles disponibles

| Workflow | Rôle |
|---|---|
| `scan-secrets.yml` | Détecte les secrets dans tout l'historique Git (Gitleaks) |
| `hello.yml` | Workflow d'exemple pour tester la réutilisation |

## Utilisation

```yaml
jobs:
  secrets:
    uses: elaasaidanii/secureflow/.github/workflows/scan-secrets.yml@main
```

Paramètre optionnel : `gitleaks-version`.

## Documentation

- [Leçons apprises](docs/lessons-learned.md)
