# Notes de sécurité : actions tierces

## Relevé sur actions/setup-node
- Créateur vérifié : (à compléter avec ce que tu vois sur la page Marketplace)
- Étoiles : 5.0k
- Dossier du code source : `src/` (code compilé dans `dist/`)

## Q3. Pourquoi faut-il épingler une version (@v4) plutôt que @main ?

`@main` pointe vers la dernière version de la branche principale de l'action : son code peut changer à tout moment, sans que je le sache ni que je l'aie relu. Un changement qui casse le workflow, une régression, ou un code malveillant (compte d'un mainteneur compromis, dépendance piégée) s'exécuterait automatiquement dans mes pipelines, avec accès au code du dépôt et aux secrets. Épingler `@v4` rend le comportement reproductible et limite les changements à ceux de la v4, censés être compatibles. Pour une sécurité maximale, on peut épingler un SHA de commit complet, car un tag comme `v4` peut être déplacé par le mainteneur.

## Q4. Le badge « créateur vérifié » garantit-il qu'une action est sûre ?

Non. Le badge indique seulement que GitHub a vérifié l'identité de l'organisation ou de l'éditeur. Il ne garantit ni l'absence de vulnérabilités, ni la qualité du code, ni que le compte ne sera jamais compromis. Une action vérifiée peut contenir un bug ou être attaquée via ses dépendances. Il faut donc aussi relire le code source, épingler une version (idéalement un SHA), limiter les permissions du `GITHUB_TOKEN` et surveiller les mises à jour.