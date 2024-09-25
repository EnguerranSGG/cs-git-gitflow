## 7.1. Rédiger des messages de commit clairs

Rédiger des messages de commit clairs est crucial pour maintenir un historique Git lisible et utile pour toute l'équipe. Voici quelques bonnes pratiques à suivre pour écrire des messages de commit efficaces :

### 1. **Utilisez l'impératif pour le titre du commit**
Le titre doit être court (50 caractères maximum) et formulé à l'impératif. Cela décrit ce que fait le commit, pas ce qu'il a fait. Par exemple :
- ✅ `Fix login issue`
- ✅ `Add user authentication`
- ❌ `Fixed login issue`
- ❌ `Adding user authentication`

### 2. **Utilisez des préfixes pour indiquer le type de modification**
Pour améliorer la lisibilité et standardiser les messages de commit, utilisez les préfixes suivants :
- **`feat:`** (nouvelle fonctionnalité pour l'utilisateur, pas une fonctionnalité liée au build script)  
  Exemple : `feat: Add user registration feature`
  
- **`fix:`** (correction de bug pour l'utilisateur, pas un correctif pour le build script)  
  Exemple : `fix: Resolve issue with form validation`

- **`docs:`** (modifications apportées à la documentation)  
  Exemple : `docs: Update installation guide in README`

- **`style:`** (formatage, points-virgules manquants, etc. ; pas de changement dans le code de production)  
  Exemple : `style: Fix indentation and remove extra spaces`

- **`refactor:`** (refactorisation du code de production, ex. renommer une variable)  
  Exemple : `refactor: Rename 'userData' to 'userProfile' for clarity`

- **`test:`** (ajout de tests manquants ou refactorisation des tests ; pas de changement dans le code de production)  
  Exemple : `test: Add unit tests for login functionality`

- **`chore:`** (mise à jour de tâches de build, de configurations, etc. ; pas de changement dans le code de production)  
  Exemple : `chore: Update Grunt tasks for build process`

### 3. **Soyez concis, mais descriptif**
Le titre doit suffire à comprendre l'objectif du commit sans avoir à lire les détails du code. Un bon message de commit doit donner une idée immédiate de ce qui a changé.

### 4. **Ajoutez une description si nécessaire**
Pour les changements plus complexes, ajoutez une description sous le titre. Séparez le titre et la description par une ligne vide. La description doit expliquer pourquoi le changement a été effectué, quels problèmes il résout, ou toute autre information importante.
Exemple :
```plaintext
feat: Add validation for email input

This ensures that users cannot submit the form without a valid email address, which reduces errors and improves data quality.
```

### 5. **Mentionnez les issues ou tickets**
Si le commit est lié à une issue ou un ticket, mentionnez-le dans le message avec un lien ou une référence. Cela permet de retracer facilement les changements liés à une tâche ou à un bug précis.
Exemple :
```plaintext
fix: Resolve broken image link in the homepage

Resolves #123
```

### 6. **Commits atomiques**
Un commit doit être atomique, c'est-à-dire qu'il doit représenter une seule modification ou un ensemble de changements cohérents et relatifs à une seule tâche. N'essayez pas de faire plusieurs choses dans un seul commit.

### 7. **Exemples de bons messages de commit**
- `feat: Refactor user authentication logic`
- `docs: Update README with installation instructions`
- `fix: Correct typo in settings page`
- `style: Improve formatting in search function`
- `test: Add unit tests for payment gateway`
- `chore: Update npm dependencies`

---

Cette section avec les préfixes normalisés aidera à maintenir une meilleure structure dans l'historique des commits, facilitant ainsi la navigation et la compréhension des changements.

## 7.2. Git et inégration continue (CI)

De par sa nature (cf [1.1. Qu'est-ce que Git ?](./doc/markdown-git/1-presentation.md)), Git est étroitement lié à l'intégration continue. Aussi appelée CI pour "Continuous Integration", cette pratique consiste en une automatisation du processus de test, de validation et d'intégration du code.

Concrétement, cela amener les développeurs à intégrer quotidiennement leur code sur une branche partagées. Chacune de ces intégrations va déclancher une processus de vérification du code; que ce soit du point de vue de la stabilité ou de la qualité. De fait, cette pratique permet de maintenir une qualité de code élevée et de repérer vite les erreurs.

### 7.2.1. Le fonctionnement de la CI

Souvent, la CI est déclanchée par une commande Git comme un push ou une PR; ces actions vont appelé un outil de CI tel que Jenklins, Travis CI etc...

Cette outil va alors prendre le code de la branche concernée pour le compiler ou le construire dans un environemment propre. Si le code est compilé / construit sans erreur, l'outil va alors lancer les tests automatiques pour vérifier que le code entrant n'intègre ni régressions, ni bugs.

Si la compilation ou les tests ne fonctionnent pas, l'outil de CI va le notifier aux développeurs afin qu'il puissent corriger le problèmes rapidement, c'est ce qui permet de maintenir une qualité de code constante.

### 7.2.2. L'interaction entre la CI et Git

Dans la pratique CI, il est recommandé d'intégrer fréquement les modifictions dans une branche principale. Grâce au fonctionnement par branche de Git, le développement va être isolé jusqu'à ce que les modifications soient prêtent à être fusionnées via, une PR par exemple.

Avant que la branche de développement ne fusionne avec la principale, l'outil de CI va être appelé pour procéder aux tests comme expliqué un peu plus haut. S'il y a le moindre problème, Git va refuser la fusion tant qu'il ne sera pas résolu.

### 7.2.3. Les outils de CI et Git

Les plateformes CI modernes s'intégrent directement avec Git :

- GitHub Actions : Se déclenche automatiquement à chaque commit ou pull request sur GitHub.
- GitLab CI : Intégré directement dans GitLab, chaque dépôt dispose d'un pipeline CI associé.
- Jenkins : Peut surveiller les dépôts Git et lancer des jobs de CI à chaque modification.### 7.3 Gestion des conflits

## 7.3 Gestion des conflits

Les conflits Git se produisent lorsque des modifications concurrentes sont effectuées sur les mêmes lignes d'un fichier ou lorsqu'un fichier est supprimé dans une branche et modifié dans une autre. Ce cheat sheet fournit un guide rapide pour identifier, résoudre et prévenir les conflits Git.

---

### Sommaire

- [Identification des Conflits](#identification-des-conflits)
- [Visualisation des Fichiers en Conflit](#visualisation-des-fichiers-en-conflit)
- [Résolution des Conflits](#résolution-des-conflits)
- [Abandonner une Opération en Cours](#abandonner-une-opération-en-cours)
- [Utilisation d'Outils de Fusion](#utilisation-doutils-de-fusion)
- [Prévention des Conflits](#prévention-des-conflits)
- [Commandes Utiles](#commandes-utiles)
- [Astuces](#astuces)

---

### Identification des Conflits

Lors d'une opération `git merge`, `git rebase` ou `git cherry-pick`, Git peut signaler des conflits :

```bash
$ git pull
Auto-merging fichier.txt
CONFLICT (content): Merge conflict in fichier.txt
Automatic merge failed; fix conflicts and then commit the result.
```

### Visualisation des Fichiers en Conflit

Liste des fichiers en conflit :

```bash
$ git status
```

Les fichiers en conflit apparaîtront sous la section **"Unmerged paths"**.

### Résolution des Conflits

1. **Ouvrir les fichiers en conflit** : Les marqueurs de conflit ressemblent à ceci :

   ```diff
   <<<<<<< HEAD
   Contenu de la branche actuelle.
   =======
   Contenu de la branche fusionnée.
   >>>>>>> nom-de-la-branche
   ```

2. **Éditer les fichiers** : Choisissez quelles modifications conserver ou combinez-les.

3. **Marquer les conflits comme résolus** :

   ```bash
   $ git add fichier.txt
   ```

4. **Valider les modifications** :

   ```bash
   $ git commit -m "Résolution des conflits sur fichier.txt"
   ```

### Abandonner une Opération en Cours

- **Annuler une fusion** :

  ```bash
  $ git merge --abort
  ```

- **Annuler un rebase** :

  ```bash
  $ git rebase --abort
  ```

### Utilisation d'Outils de Fusion

Configurer un outil de fusion (par exemple, Meld) :

```bash
$ git config --global merge.tool meld
$ git config --global mergetool.meld.path "/chemin/vers/meld"
```

Utiliser l'outil de fusion :

```bash
$ git mergetool
```

### Prévention des Conflits

- **Communication d'équipe** : Informez-vous mutuellement des modifications majeures.
- **Mises à jour fréquentes** : Intégrez régulièrement les changements de la branche principale.
- **Branches de fonctionnalité** : Isolez les travaux en cours pour minimiser les conflits.

### Commandes Utiles

- **Voir les conflits restants** :

  ```bash
  $ git diff --name-only --diff-filter=U
  ```

- **Afficher les différences** :

  ```bash
  $ git diff
  ```

- **Afficher les marqueurs de conflit** :

  ```bash
  $ git diff --merge
  ```

### Astuces

- **Commits atomiques** : Des commits petits et spécifiques facilitent la résolution des conflits.
- **Utiliser `git stash`** : Avant de tirer des changements, sauvegardez vos modifications en cours.

---

**Note** : Ce cheat sheet est un guide rapide. Pour des situations complexes, consultez la [documentation officielle de Git](https://git-scm.com/docs).

## 7.4. Ne jamais committer des fichiers sensibles (utiliser .gitignore)

Il est primordial de **ne jamais committer des fichiers sensibles** dans un dépôt Git. Les fichiers sensibles peuvent contenir des informations confidentielles comme :

- Des mots de passe
- Des clés API
- Des certificats SSL
- Des configurations spécifiques à l'environnement de développement ou de production

Une fois qu'un fichier sensible est committé dans l'historique Git, il est difficile de le supprimer de façon sécurisée. Ces informations pourraient être exposées, même si elles sont supprimées par la suite.

### Utilisation de `.gitignore`

Pour éviter d'inclure ces fichiers sensibles dans votre dépôt Git, il est recommandé d'utiliser un fichier `.gitignore`. Ce fichier permet de spécifier les fichiers ou répertoires que Git doit ignorer lors du commit.

#### Exemple d'utilisation de `.gitignore`

Voici un exemple de contenu d'un fichier `.gitignore` :

```bash
# Ignorer les fichiers de configuration sensibles
.env
config/*.json

# Ignorer les clés privées
*.key
*.pem

# Ignorer les répertoires contenant des données temporaires
/tmp/
```

Ce fichier `.gitignore` empêchera Git de suivre les fichiers listés, évitant ainsi leur inclusion dans l'historique des commits.

#### Bonnes pratiques

- **Ne pas inclure d'informations sensibles dans le code** : si possible, utilisez des variables d'environnement pour stocker les informations sensibles.
- **Vérifier avant de committer** : assurez-vous que les fichiers contenant des informations sensibles sont correctement exclus via `.gitignore`.
- **Utiliser des outils spécialisés** : il existe des outils comme [Git-crypt](https://github.com/AGWA/git-crypt) ou [BlackBox](https://github.com/StackExchange/blackbox) pour chiffrer des fichiers sensibles tout en les stockant dans Git.

En suivant ces pratiques, vous limiterez les risques d'exposer des données confidentielles et contribuerez à la sécurité de votre projet.