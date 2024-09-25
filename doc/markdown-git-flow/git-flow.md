# Git Flow : Workflow avancé de gestion des branches

## 1. Introduction à Git Flow
Git Flow est une méthodologie de gestion de branches conçue pour organiser le développement logiciel de manière claire et structurée. Elle est particulièrement adaptée aux projets avec plusieurs contributeurs et des versions régulières. Git Flow propose plusieurs types de branches pour différents rôles dans le cycle de développement : développement de fonctionnalités, préparation des versions, correctifs urgents, etc.

## 2. Installation de Git Flow

#### Sur macOS :
Installez Git Flow via Homebrew :
```bash
brew install git-flow-avh
```

#### Sur Linux (Ubuntu/Debian) :
Utilisez la commande apt-get pour installer Git Flow :
```bash
sudo apt-get install git-flow
```

#### Sur Windows :
Git Flow peut être installé via **Git for Windows** ou **Scoop** :
- **Via Git for Windows** : Téléchargez et installez [Git for Windows](https://gitforwindows.org/), qui inclut une option pour installer Git Flow.
- **Via Scoop** :
  ```bash
  scoop install git-flow
  ```

## 3. Initialisation de Git Flow
Une fois que Git Flow est installé, vous devez l'initialiser dans votre dépôt Git existant. Cette étape configure les branches principales (`main` et `develop`) et définit les conventions de nommage pour les autres types de branches.

- **Initialiser Git Flow** :
  ```bash
  git flow init
  ```
  Lors de l'initialisation, Git Flow vous demandera de confirmer les noms des branches (`main`, `develop`, etc.) et vous proposera des valeurs par défaut que vous pouvez accepter ou personnaliser.

## 4. Les branches principales dans Git Flow

1. **`main` (ou `master`)** :  
   Cette branche contient le code en production, qui doit toujours être stable. Les nouvelles versions sont fusionnées dans `main` via des branches de release ou de hotfix.

2. **`develop`** :  
   Cette branche est utilisée pour intégrer toutes les nouvelles fonctionnalités. C'est l'environnement où le code est testé avant d'être prêt pour la production.

## 5. Les branches de support

1. **Feature branches** (`feature/`) :
   - Utilisées pour le développement de nouvelles fonctionnalités.
   - Créées à partir de `develop` et fusionnées dans `develop` une fois la fonctionnalité terminée.
   - Convention de nommage : `feature/<nom_fonctionnalité>`

   **Exemples de commandes** :
   - **Créer une feature branch** :
     ```bash
     git checkout develop
     git checkout -b feature/<nom_fonctionnalité>
     ```
   - **Fusionner une feature branch dans develop** :
     ```bash
     git checkout develop
     git merge feature/<nom_fonctionnalité>
     git branch -d feature/<nom_fonctionnalité>
     ```

2. **Release branches** (`release/`) :
   - Utilisées pour préparer une nouvelle version.
   - Créées à partir de `develop`, puis fusionnées dans `main` et `develop` une fois la version prête pour la production.
   - Convention de nommage : `release/<version>`

   **Exemples de commandes** :
   - **Créer une release branch** :
     ```bash
     git checkout develop
     git checkout -b release/<version>
     ```
   - **Fusionner une release branch dans main et develop** :
     ```bash
     git checkout main
     git merge release/<version>
     git tag <version>  # Taguer la nouvelle version
     git checkout develop
     git merge release/<version>
     git branch -d release/<version>
     ```

3. **Hotfix branches** (`hotfix/`) :
   - Utilisées pour corriger rapidement des bugs critiques en production.
   - Créées à partir de `main`, puis fusionnées à la fois dans `main` et `develop` (ou `release` si une release est en préparation).
   - Convention de nommage : `hotfix/<description_bug>`

   **Exemples de commandes** :
   - **Créer une hotfix branch** :
     ```bash
     git checkout main
     git checkout -b hotfix/<description_bug>
     ```
   - **Fusionner une hotfix branch dans main et develop** :
     ```bash
     git checkout main
     git merge hotfix/<description_bug>
     git tag <version_hotfix>
     git checkout develop
     git merge hotfix/<description_bug>
     git branch -d hotfix/<description_bug>
     ```
