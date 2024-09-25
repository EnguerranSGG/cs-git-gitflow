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
- Jenkins : Peut surveiller les dépôts Git et lancer des jobs de CI à chaque modification.
