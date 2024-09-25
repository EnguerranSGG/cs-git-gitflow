### 7.2. Git et inégration continue (CI)

De par sa nature (cf [1.1. Qu'est-ce que Git ?](./doc/markdown-git/1-presentation.md)), Git est étroitement lié à l'intégration continue. Aussi appelée CI pour "Continuous Integration", cette pratique consiste en une automatisation du processus de test, de validation et d'intégration du code.

Concrétement, cela amener les développeurs à intégrer quotidiennement leur code sur une branche partagées. Chacune de ces intégrations va déclancher une processus de vérification du code; que ce soit du point de vue de la stabilité ou de la qualité. De fait, cette pratique permet de maintenir une qualité de code élevée et de repérer vite les erreurs.

#### 7.2.1. Le fonctionnement de la CI

Souvent, la CI est déclanchée par une commande Git comme un push ou une PR; ces actions vont appelé un outil de CI tel que Jenklins, Travis CI etc...

Cette outil va alors prendre le code de la branche concernée pour le compiler ou le construire dans un environemment propre. Si le code est compilé / construit sans erreur, l'outil va alors lancer les tests automatiques pour vérifier que le code entrant n'intègre ni régressions, ni bugs.

Si la compilation ou les tests ne fonctionnent pas, l'outil de CI va le notifier aux développeurs afin qu'il puissent corriger le problèmes rapidement, c'est ce qui permet de maintenir une qualité de code constante.

#### 7.2.2. L'interaction entre la CI et Git

Dans la pratique CI, il est recommandé d'intégrer fréquement les modifictions dans une branche principale. Grâce au fonctionnement par branche de Git, le développement va être isolé jusqu'à ce que les modifications soient prêtent à être fusionnées via, une PR par exemple.

Avant que la branche de développement ne fusionne avec la principale, l'outil de CI va être appelé pour procéder aux tests comme expliqué un peu plus haut. S'il y a le moindre problème, Git va refuser la fusion tant qu'il ne sera pas résolu.

#### 7.2.3. Les outils de CI et Git

Les plateformes CI modernes s'intégrent directement avec Git :

- GitHub Actions : Se déclenche automatiquement à chaque commit ou pull request sur GitHub.
- GitLab CI : Intégré directement dans GitLab, chaque dépôt dispose d'un pipeline CI associé.
- Jenkins : Peut surveiller les dépôts Git et lancer des jobs de CI à chaque modification.### 7.3 Gestion des conflits

# Gestion des Conflits Git - Cheat Sheet

Les conflits Git se produisent lorsque des modifications concurrentes sont effectuées sur les mêmes lignes d'un fichier ou lorsqu'un fichier est supprimé dans une branche et modifié dans une autre. Ce cheat sheet fournit un guide rapide pour identifier, résoudre et prévenir les conflits Git.

---

## Sommaire

- [Identification des Conflits](#identification-des-conflits)
- [Visualisation des Fichiers en Conflit](#visualisation-des-fichiers-en-conflit)
- [Résolution des Conflits](#résolution-des-conflits)
- [Abandonner une Opération en Cours](#abandonner-une-opération-en-cours)
- [Utilisation d'Outils de Fusion](#utilisation-doutils-de-fusion)
- [Prévention des Conflits](#prévention-des-conflits)
- [Commandes Utiles](#commandes-utiles)
- [Astuces](#astuces)

---

## Identification des Conflits

Lors d'une opération `git merge`, `git rebase` ou `git cherry-pick`, Git peut signaler des conflits :

```bash
$ git pull
Auto-merging fichier.txt
CONFLICT (content): Merge conflict in fichier.txt
Automatic merge failed; fix conflicts and then commit the result.
```

## Visualisation des Fichiers en Conflit

Liste des fichiers en conflit :

```bash
$ git status
```

Les fichiers en conflit apparaîtront sous la section **"Unmerged paths"**.

## Résolution des Conflits

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

## Abandonner une Opération en Cours

- **Annuler une fusion** :

  ```bash
  $ git merge --abort
  ```

- **Annuler un rebase** :

  ```bash
  $ git rebase --abort
  ```

## Utilisation d'Outils de Fusion

Configurer un outil de fusion (par exemple, Meld) :

```bash
$ git config --global merge.tool meld
$ git config --global mergetool.meld.path "/chemin/vers/meld"
```

Utiliser l'outil de fusion :

```bash
$ git mergetool
```

## Prévention des Conflits

- **Communication d'équipe** : Informez-vous mutuellement des modifications majeures.
- **Mises à jour fréquentes** : Intégrez régulièrement les changements de la branche principale.
- **Branches de fonctionnalité** : Isolez les travaux en cours pour minimiser les conflits.

## Commandes Utiles

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

## Astuces

- **Commits atomiques** : Des commits petits et spécifiques facilitent la résolution des conflits.
- **Utiliser `git stash`** : Avant de tirer des changements, sauvegardez vos modifications en cours.

---

**Note** : Ce cheat sheet est un guide rapide. Pour des situations complexes, consultez la [documentation officielle de Git](https://git-scm.com/docs).
