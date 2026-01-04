# Contributing to Security Bank Faker 🏦

Merci de l'intérêt que vous portez à la sécurisation de notre infrastructure bancaire ! Pour maintenir un niveau de sécurité "Enterprise", nous suivons des règles strictes.

## 🛠️ Workflow de Développement
1. Forkez le projet.
2. Créez une branche thématique (`feat/`, `fix/`, `security/`).
3. Assurez-vous que votre code respecte les standards Symfony.
4. Soumettez une Pull Request (PR).

## 📝 Standards de Code
- **PHP 8.4+** : Utilisez les propriétés en lecture seule (`readonly`), les types stricts et les attributs.
- [cite_start]**Sécurité** : Toute nouvelle fonctionnalité doit utiliser le `SecurityBundle`  et être testée contre les failles OWASP.
- **Tests** : Les tests unitaires et d'intégration sont obligatoires pour tout changement dans le `Firewall` ou les `Voters`.

## 🔒 Règles de Sécurité Critiques
- [cite_start]Ne modifiez jamais les paramètres de hachage (`password_hashers`) vers un algorithme moins sûr que `auto`[cite: 8].
- Ne commitez JAMAIS de données sensibles.
- Si vous trouvez une faille, référez-vous au fichier [SECURITY.md](./SECURITY.md).

## 💬 Style de Commit
Nous utilisons les **Conventional Commits** :
- `feat: ...` (nouvelle fonctionnalité)
- `fix: ...` (correction de bug)
- `docs: ...` (documentation)
- `refactor: ...` (amélioration du code sans changement fonctionnel)
