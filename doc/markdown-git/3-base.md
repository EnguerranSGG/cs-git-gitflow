# 3. Les bases de Git

Ce guide présente les principales commandes Git utilisées dans la gestion de version et le suivi de projets.

## 3.1. Initialiser un dépôt Git (git init)

La commande `git init` permet d'initialiser un nouveau dépôt Git dans un répertoire existant. Elle crée un répertoire `.git` qui contient toutes les informations nécessaires à la gestion de version pour ce projet.

### Exemple :
```bash
git init
```

Après cette commande, Git commence à suivre les modifications dans ce dossier.

## 3.2. Cloner un dépôt (`git clone`)

`git clone` est utilisé pour copier un dépôt Git existant (local ou distant) vers votre machine. Cela inclut tout l'historique et les fichiers actuels du projet.

### Exemple :
```bash
git clone https://github.com/utilisateur/nom-du-repo.git
```

Cela crée un dossier local contenant les fichiers du dépôt, ainsi que son historique.

## 3.3. Suivi des fichiers (`git add`)

La commande `git add` permet d'ajouter des modifications dans la "staging area", c’est-à-dire de préparer les fichiers pour un commit. Vous pouvez ajouter des fichiers individuels ou tous les fichiers modifiés.

### Ajouter un fichier spécifique :
```bash
git add monfichier.txt
```

### Ajouter tous les fichiers modifiés :
```bash
git add .
```

## 3.4. Committer des changements (`git commit`)

Une fois que les modifications sont ajoutées à la staging area avec `git add`, vous pouvez utiliser `git commit` pour enregistrer ces changements dans l'historique du projet. Chaque commit doit inclure un message descriptif.

### Exemple :
```bash
git commit -m "Ajout de la fonctionnalité X"
```

Cela enregistre un instantané des fichiers suivis dans Git avec le message fourni.

## 3.5. Vérifier l'état du dépôt (`git status`)

La commande `git status` montre l'état actuel du projet. Elle liste les fichiers modifiés, non suivis, ou en attente de commit, et donne un aperçu de ce qui se passe dans votre dépôt.

### Exemple :
```bash
git status
```

Cela vous aide à savoir quels fichiers sont prêts à être commités, lesquels ne sont pas encore suivis, et s'il y a des conflits à résoudre.

## 3.6. Voir l'historique des commits (`git log`)

La commande `git log` permet de voir l'historique des commits dans le dépôt, avec les messages de commit, l'auteur, la date et l'identifiant unique (SHA) de chaque commit.

### Exemple :
```bash
git log
```

### Pour une vue simplifiée :
```bash
git log --oneline
```

Cela affiche les commits avec seulement l'ID abrégé et le message de commit.

## 3.7. Annuler des modifications (`git checkout`, `git reset`)

##### Annuler des changements dans un fichier spécifique (avant `git add`) :
```bash
git checkout -- monfichier.txt
```

Cette commande restaure le fichier dans l'état du dernier commit, annulant ainsi toutes les modifications locales non ajoutées.

##### Annuler des modifications ajoutées à la staging area (`git reset`) :
```bash
git reset monfichier.txt
```

Cela retire le fichier de la staging area mais conserve les modifications locales.

##### Annuler un commit local (`git reset --soft`, `git reset --hard`) :
- **`git reset --soft`** : annule le dernier commit, mais conserve les modifications dans la staging area.
- **`git reset --hard`** : annule le commit et toutes les modifications locales, en réinitialisant l'état du dépôt au dernier commit.

### Exemple :
```bash
git reset --hard HEAD~1
```

Cela réinitialise le dépôt à l'état du commit précédent, en supprimant toutes les modifications locales.

---

## Conclusion

Ce README vous offre un aperçu des principales commandes Git que vous utiliserez fréquemment. En maîtrisant ces commandes, vous serez en mesure de gérer efficacement les versions de votre code, collaborer avec d'autres développeurs, et mieux contrôler l'évolution de votre projet.

N'hésitez pas à consulter la documentation officielle de Git pour des détails supplémentaires et des options avancées : [Git Documentation](https://git-scm.com/doc).
