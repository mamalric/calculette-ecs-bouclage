# Calculette ECS et Bouclage

## Idée

# Prompt pour Claude Code — Calculette ECS et Bouclage

## Contexte de travail (à respecter impérativement)

Ce projet est développé dans mon dossier **DevCode**, où chaque projet suit des conventions fixes :

- Chaque projet possède une **FICHE.md** à sa racine, avec au minimum ces champs : `id`, `nom`, `type`, `statut`, `pitch`, `tags`, `stack`, `lancer`. Crée-la dès le démarrage du projet et tiens-la à jour à chaque étape significative.
- Chaque projet possède un **JOURNAL.md** qui trace les décisions prises, les étapes réalisées et les points en suspens. Mets-le à jour au fil de l'avancement, pas seulement à la fin.
- Convention de stack selon le type de projet :
  - Applications de bureau → Python + PySide6 + QML.
  - Petits outils → **une seule page HTML, CSS, JS, sans framework, sans build**.
  - Sites → HTML, CSS, JavaScript, sans build.

Ce projet est un **petit outil** : il doit donc être livré comme une page HTML autonome (HTML/CSS/JS vanilla), sans dépendance de build, utilisable en ouvrant simplement le fichier dans un navigateur.

**Avant de coder, si un point ci-dessous est ambigu, incomplet, ou si tu dois trancher entre plusieurs méthodes de calcul ou hypothèses réglementaires, pose-moi tes questions plutôt que de deviner.** Ce sujet touche à des méthodes techniques normatives (DTU, guides CSTB, etc.) où une hypothèse fausse invalide le résultat.

---

## 1. Objectif et utilisateurs

**Objectif** : fournir une calculette permettant d'estimer le besoin de stockage d'eau chaude sanitaire (ECS) et de dimensionner le bouclage (réseau de recirculation ECS) d'un bâtiment, selon son usage.

**Usage attendu des résultats** : les sorties doivent être directement exploitables par un ingénieur ou un chargé d'affaires (OP = maître d'ouvrage / opérateur du projet) pour :
- consulter un fabricant (ballon ECS, échangeur, pompe de bouclage, etc.) avec des valeurs cibles claires ;
- vérifier la cohérence d'une installation existante (le stockage en place est-il suffisant ? le débit de bouclage est-il cohérent ?).

**Utilisateur principal** : moi-même (ingénieur BET fluides / CVC), en phase d'études ou de vérification, pour un usage rapide en réunion ou en phase de dimensionnement.

**Types de bâtiments à couvrir** (liste non exhaustive, à compléter si besoin) :
- Logement collectif / individuel
- Tertiaire / bureaux
- Hôtellerie
- Restauration (restaurant, cuisine collective)
- Établissements de santé (si pertinent — à confirmer)
- Établissements scolaires (si pertinent — à confirmer)
- Sport / vestiaires collectifs (si pertinent — à confirmer)
- Tout autre usage type ERP avec besoin ECS significatif

---

## 2. Fonctionnalités essentielles

1. **Sélection du type de bâtiment / usage**, avec pour chaque type les paramètres et méthodes de calcul adaptés (les besoins ECS d'un hôtel, d'un logement et d'un restaurant ne se calculent pas de la même façon).
2. **Calcul du besoin de stockage ECS** :
   - Saisie des données d'entrée pertinentes selon le type de bâtiment (nombre de logements/chambres/couverts/employés/m², ratio de consommation, température de puisage, température d'eau froide, etc.).
   - Restitution du volume de stockage recommandé (en litres), avec la méthode de calcul utilisée clairement affichée (nom, référence si applicable).
   - Si plusieurs méthodes de référence existent pour un même usage, permettre de choisir la méthode ou d'afficher les résultats des différentes méthodes à titre de comparaison.
3. **Calcul du bouclage** :
   - Débit de bouclage recommandé.
   - Pertes thermiques du réseau (estimation) et puissance de compensation nécessaire.
   - Diamètre indicatif de la canalisation de retour bouclage, si cela reste raisonnable à intégrer.
4. **Résultats exploitables** :
   - Affichage synthétique et clair (valeurs clés en évidence, pas seulement un résultat brut).
   - Rappel des hypothèses et de la méthode utilisée, pour que je puisse justifier le chiffre auprès d'un fabricant ou d'un client.
   - Possibilité d'imprimer / exporter le résultat (a minima impression navigateur propre, export PDF si simple à faire sans dépendance lourde).
5. **Saisie guidée** : formulaire clair, avec valeurs par défaut réalistes (préremplies) pour chaque type de bâtiment, modifiables par l'utilisateur.

---

## 3. Fonctionnalités secondaires (si le temps/la complexité le permet)

- Comparateur multi-méthodes (afficher côte à côte les résultats de 2-3 méthodes de dimensionnement reconnues, quand elles existent pour un usage donné).
- Mode « vérification d'installation existante » : je saisis le volume de ballon existant et le débit de bouclage existant, l'outil me dit si c'est conforme/suffisant par rapport au calcul théorique, avec un écart en %.
- Sauvegarde locale des derniers calculs (localStorage du navigateur) pour reprendre un calcul en cours.
- Génération d'une fiche de synthèse formatée (à copier-coller ou imprimer) prête à envoyer à un fabricant.
- Gestion de plusieurs bâtiments/scénarios dans une même session (comparer plusieurs hypothèses).

---

## 4. Contraintes et données

- **Rigueur technique avant tout** : les formules et ratios utilisés doivent être identifiables et sourcés (méthode, DTU, guide professionnel, etc.), pas de valeur inventée. Si tu n'as pas de source fiable pour un ratio ou une méthode, dis-le moi explicitement plutôt que d'inventer un chiffre.
- Les méthodes de dimensionnement ECS françaises courantes à considérer (à valider avec moi si doute) : DTU 60.11 (règles de calcul des installations de plomberie sanitaire), guides CSTB, retours d'expérience professionnels (COSTIC, ADEME, fabricants comme les guides techniques disponibles publiquement).
- Les hypothèses par défaut (ratios L/j/personne, températures de référence, etc.) doivent être ajustables : ce sont des valeurs indicatives, pas des vérités figées, et le métier évolue selon les projets.
- Pas de dépendance externe lourde : outil autonome, un seul fichier HTML si possible (CSS et JS inline ou dans le même fichier), fonctionnant hors ligne.
- Interface en français, vocabulaire métier CVC/plomberie cohérent avec mes autres projets (note-cvc, cctp-btp, etc.).
- Pas de collecte de données, pas de dépendance à un serveur : tout calcul se fait côté client.

---

## 5. Stack proposée

- **HTML/CSS/JS vanilla**, une seule page, sans framework, sans étape de build — conformément à ma convention "petits outils".
- Pas de librairie externe sauf si strictement nécessaire et légère (à justifier avant de l'ajouter).
- Structure de fichiers simple à la racine du projet dans DevCode (ex. `index.html`, éventuellement `styles.css` et `script.js` séparés si le fichier devient trop long à maintenir en un seul bloc — à ta discrétion, en gardant l'esprit "sans build").

---

## 6. Étapes de réalisation suggérées

1. **Cadrage** : lister avec moi les types de bâtiments à couvrir en priorité (tous ne sont peut-être pas nécessaires dès la v1) et les méthodes de calcul associées à chacun. Poser les questions nécessaires ici avant toute chose.
2. **Modélisation des données** : définir pour chaque type de bâtiment les paramètres d'entrée, les formules de calcul du stockage ECS, et les formules de calcul du bouclage.
3. **Maquette de l'interface** : structure du formulaire (sélection du type de bâtiment → champs dynamiques → résultats), en respectant une hiérarchie visuelle claire (résultats mis en avant).
4. **Développement** : implémentation du calcul et de l'interface, en une page HTML autonome.
5. **Vérification croisée** : tester les résultats sur 2-3 cas types (ex. un hôtel de 50 chambres, un immeuble de logements, un restaurant) et comparer aux ordres de grandeur usuels du métier, avec moi si besoin.
6. **Finalisation** : rédaction de la FICHE.md et mise à jour du JOURNAL.md, avec le mode de lancement (ouverture du fichier HTML).

---

## 7. Critères de réussite

- Un utilisateur (moi) peut, en moins de 2 minutes, sélectionner un type de bâtiment, saisir les données de base, et obtenir un volume de stockage ECS et un débit de bouclage exploitables.
- Chaque résultat est accompagné de la méthode et des hypothèses utilisées, de façon suffisamment claire pour être présenté tel quel à un fabricant ou intégré dans une note technique.
- L'outil couvre a minima les usages suivants dès la v1 : logement, tertiaire/bureau, hôtel, restaurant (les autres usages pouvant être ajoutés en v2 si le temps manque — à confirmer avec moi).
- Le fichier fonctionne sans connexion internet, sans installation, en ouvrant simplement le HTML dans un navigateur.
- La FICHE.md et le JOURNAL.md sont créés et à jour en fin de session.
- Aucune formule ou ratio n'est utilisé sans que sa source ou son origine soit indiquée quelque part (dans le code, l'interface, ou la documentation du projet).

---

## Rappel final pour Claude Code

Avant de commencer à coder, pose-moi toutes les questions nécessaires sur :
- les types de bâtiments à prioriser pour la v1,
- les méthodes de calcul à utiliser si plusieurs existent pour un même usage,
- les valeurs par défaut (ratios, températures) si tu n'as pas de source fiable.

N'improvise pas de valeur technique sans me le signaler clairement.

## Prompt

# Prompt pour Claude Code — Calculette ECS et Bouclage

## Contexte de travail (à respecter impérativement)

Ce projet est développé dans mon dossier **DevCode**, où chaque projet suit des conventions fixes :

- Chaque projet possède une **FICHE.md** à sa racine, avec au minimum ces champs : `id`, `nom`, `type`, `statut`, `pitch`, `tags`, `stack`, `lancer`. Crée-la dès le démarrage du projet et tiens-la à jour à chaque étape significative.
- Chaque projet possède un **JOURNAL.md** qui trace les décisions prises, les étapes réalisées et les points en suspens. Mets-le à jour au fil de l'avancement, pas seulement à la fin.
- Convention de stack selon le type de projet :
  - Applications de bureau → Python + PySide6 + QML.
  - Petits outils → **une seule page HTML, CSS, JS, sans framework, sans build**.
  - Sites → HTML, CSS, JavaScript, sans build.

Ce projet est un **petit outil** : il doit donc être livré comme une page HTML autonome (HTML/CSS/JS vanilla), sans dépendance de build, utilisable en ouvrant simplement le fichier dans un navigateur.

**Avant de coder, si un point ci-dessous est ambigu, incomplet, ou si tu dois trancher entre plusieurs méthodes de calcul ou hypothèses réglementaires, pose-moi tes questions plutôt que de deviner.** Ce sujet touche à des méthodes techniques normatives (DTU, guides CSTB, etc.) où une hypothèse fausse invalide le résultat.

---

## 1. Objectif et utilisateurs

**Objectif** : fournir une calculette permettant d'estimer le besoin de stockage d'eau chaude sanitaire (ECS) et de dimensionner le bouclage (réseau de recirculation ECS) d'un bâtiment, selon son usage.

**Usage attendu des résultats** : les sorties doivent être directement exploitables par un ingénieur ou un chargé d'affaires (OP = maître d'ouvrage / opérateur du projet) pour :
- consulter un fabricant (ballon ECS, échangeur, pompe de bouclage, etc.) avec des valeurs cibles claires ;
- vérifier la cohérence d'une installation existante (le stockage en place est-il suffisant ? le débit de bouclage est-il cohérent ?).

**Utilisateur principal** : moi-même (ingénieur BET fluides / CVC), en phase d'études ou de vérification, pour un usage rapide en réunion ou en phase de dimensionnement.

**Types de bâtiments à couvrir** (liste non exhaustive, à compléter si besoin) :
- Logement collectif / individuel
- Tertiaire / bureaux
- Hôtellerie
- Restauration (restaurant, cuisine collective)
- Établissements de santé (si pertinent — à confirmer)
- Établissements scolaires (si pertinent — à confirmer)
- Sport / vestiaires collectifs (si pertinent — à confirmer)
- Tout autre usage type ERP avec besoin ECS significatif

---

## 2. Fonctionnalités essentielles

1. **Sélection du type de bâtiment / usage**, avec pour chaque type les paramètres et méthodes de calcul adaptés (les besoins ECS d'un hôtel, d'un logement et d'un restaurant ne se calculent pas de la même façon).
2. **Calcul du besoin de stockage ECS** :
   - Saisie des données d'entrée pertinentes selon le type de bâtiment (nombre de logements/chambres/couverts/employés/m², ratio de consommation, température de puisage, température d'eau froide, etc.).
   - Restitution du volume de stockage recommandé (en litres), avec la méthode de calcul utilisée clairement affichée (nom, référence si applicable).
   - Si plusieurs méthodes de référence existent pour un même usage, permettre de choisir la méthode ou d'afficher les résultats des différentes méthodes à titre de comparaison.
3. **Calcul du bouclage** :
   - Débit de bouclage recommandé.
   - Pertes thermiques du réseau (estimation) et puissance de compensation nécessaire.
   - Diamètre indicatif de la canalisation de retour bouclage, si cela reste raisonnable à intégrer.
4. **Résultats exploitables** :
   - Affichage synthétique et clair (valeurs clés en évidence, pas seulement un résultat brut).
   - Rappel des hypothèses et de la méthode utilisée, pour que je puisse justifier le chiffre auprès d'un fabricant ou d'un client.
   - Possibilité d'imprimer / exporter le résultat (a minima impression navigateur propre, export PDF si simple à faire sans dépendance lourde).
5. **Saisie guidée** : formulaire clair, avec valeurs par défaut réalistes (préremplies) pour chaque type de bâtiment, modifiables par l'utilisateur.

---

## 3. Fonctionnalités secondaires (si le temps/la complexité le permet)

- Comparateur multi-méthodes (afficher côte à côte les résultats de 2-3 méthodes de dimensionnement reconnues, quand elles existent pour un usage donné).
- Mode « vérification d'installation existante » : je saisis le volume de ballon existant et le débit de bouclage existant, l'outil me dit si c'est conforme/suffisant par rapport au calcul théorique, avec un écart en %.
- Sauvegarde locale des derniers calculs (localStorage du navigateur) pour reprendre un calcul en cours.
- Génération d'une fiche de synthèse formatée (à copier-coller ou imprimer) prête à envoyer à un fabricant.
- Gestion de plusieurs bâtiments/scénarios dans une même session (comparer plusieurs hypothèses).

---

## 4. Contraintes et données

- **Rigueur technique avant tout** : les formules et ratios utilisés doivent être identifiables et sourcés (méthode, DTU, guide professionnel, etc.), pas de valeur inventée. Si tu n'as pas de source fiable pour un ratio ou une méthode, dis-le moi explicitement plutôt que d'inventer un chiffre.
- Les méthodes de dimensionnement ECS françaises courantes à considérer (à valider avec moi si doute) : DTU 60.11 (règles de calcul des installations de plomberie sanitaire), guides CSTB, retours d'expérience professionnels (COSTIC, ADEME, fabricants comme les guides techniques disponibles publiquement).
- Les hypothèses par défaut (ratios L/j/personne, températures de référence, etc.) doivent être ajustables : ce sont des valeurs indicatives, pas des vérités figées, et le métier évolue selon les projets.
- Pas de dépendance externe lourde : outil autonome, un seul fichier HTML si possible (CSS et JS inline ou dans le même fichier), fonctionnant hors ligne.
- Interface en français, vocabulaire métier CVC/plomberie cohérent avec mes autres projets (note-cvc, cctp-btp, etc.).
- Pas de collecte de données, pas de dépendance à un serveur : tout calcul se fait côté client.

---

## 5. Stack proposée

- **HTML/CSS/JS vanilla**, une seule page, sans framework, sans étape de build — conformément à ma convention "petits outils".
- Pas de librairie externe sauf si strictement nécessaire et légère (à justifier avant de l'ajouter).
- Structure de fichiers simple à la racine du projet dans DevCode (ex. `index.html`, éventuellement `styles.css` et `script.js` séparés si le fichier devient trop long à maintenir en un seul bloc — à ta discrétion, en gardant l'esprit "sans build").

---

## 6. Étapes de réalisation suggérées

1. **Cadrage** : lister avec moi les types de bâtiments à couvrir en priorité (tous ne sont peut-être pas nécessaires dès la v1) et les méthodes de calcul associées à chacun. Poser les questions nécessaires ici avant toute chose.
2. **Modélisation des données** : définir pour chaque type de bâtiment les paramètres d'entrée, les formules de calcul du stockage ECS, et les formules de calcul du bouclage.
3. **Maquette de l'interface** : structure du formulaire (sélection du type de bâtiment → champs dynamiques → résultats), en respectant une hiérarchie visuelle claire (résultats mis en avant).
4. **Développement** : implémentation du calcul et de l'interface, en une page HTML autonome.
5. **Vérification croisée** : tester les résultats sur 2-3 cas types (ex. un hôtel de 50 chambres, un immeuble de logements, un restaurant) et comparer aux ordres de grandeur usuels du métier, avec moi si besoin.
6. **Finalisation** : rédaction de la FICHE.md et mise à jour du JOURNAL.md, avec le mode de lancement (ouverture du fichier HTML).

---

## 7. Critères de réussite

- Un utilisateur (moi) peut, en moins de 2 minutes, sélectionner un type de bâtiment, saisir les données de base, et obtenir un volume de stockage ECS et un débit de bouclage exploitables.
- Chaque résultat est accompagné de la méthode et des hypothèses utilisées, de façon suffisamment claire pour être présenté tel quel à un fabricant ou intégré dans une note technique.
- L'outil couvre a minima les usages suivants dès la v1 : logement, tertiaire/bureau, hôtel, restaurant (les autres usages pouvant être ajoutés en v2 si le temps manque — à confirmer avec moi).
- Le fichier fonctionne sans connexion internet, sans installation, en ouvrant simplement le HTML dans un navigateur.
- La FICHE.md et le JOURNAL.md sont créés et à jour en fin de session.
- Aucune formule ou ratio n'est utilisé sans que sa source ou son origine soit indiquée quelque part (dans le code, l'interface, ou la documentation du projet).

---

## Rappel final pour Claude Code

Avant de commencer à coder, pose-moi toutes les questions nécessaires sur :
- les types de bâtiments à prioriser pour la v1,
- les méthodes de calcul à utiliser si plusieurs existent pour un même usage,
- les valeurs par défaut (ratios, températures) si tu n'as pas de source fiable.

N'improvise pas de valeur technique sans me le signaler clairement.
