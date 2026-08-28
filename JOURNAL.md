# Journal

<!-- Dernière entrée en haut. Une entrée par session de travail ou par décision. Date au format AAAA-MM-JJ. -->

## 2026-08-28 (mise en ligne)
- L'utilisateur a déployé la page sur GitHub Pages : https://mamalric.github.io/calculette-ecs-bouclage/, servie depuis `main` à la racine, HTTPS forcé, build en succès. C'est donc la v0 étiquetée qui est en ligne.
- Le dépôt est passé de privé à public à cette occasion (condition des Pages gratuites). Tout le contenu du dépôt est désormais lisible publiquement : `idee-origine.md`, `JOURNAL.md`, `FICHE.md` et `CLAUDE.md` compris. Rien de confidentiel ne s'y trouve (aucune donnée client, aucun secret), mais les conventions de travail et les autres projets cités y sont visibles.
- Vérification de la page en ligne : titre, version v0, 7 usages, 9 sources et rouage présents, aucune erreur console. Le `localStorage` fonctionne réellement sur l'origine https, contrairement à l'aperçu local en `file://` où il lève une SecurityError. Les scénarios enregistrés sur le site et ceux du fichier local sont donc deux stocks distincts.
- Conséquence pour la suite : les Pages servent `main`, le travail sur `dev` n'apparaîtra en ligne qu'après fusion.

## 2026-08-28 (v0)
- Ajout du panneau "À propos" ouvert par le rouage en haut à droite, repris du Sélectionneur de radiateurs (même `<dialog>`, mêmes styles, mêmes icônes Lucide inlinées). Contenu : version, périmètre couvert, registre des sources, scénario en cours, informations techniques.
- Le registre des sources est devenu une donnée (`SOURCES`) au lieu d'un commentaire : les codes [G1], [B1], etc. employés dans les aides et les résultats renvoient à cette liste unique, que le panneau affiche avec les liens. Impossible désormais que la liste diverge de ce que l'outil utilise.
- Tous les compteurs du panneau sont calculés à l'ouverture (7 usages, 54 champs, 4 modes, 9 diamètres cuivre, 6 classes d'isolation, 13 Ko de données de référence) et non recopiés : ils ne peuvent pas mentir après un ajout.
- Les icônes du thème ont été fusionnées dans un dictionnaire de tracés commun avec une fonction `ico()`, comme dans le projet radiateurs.
- Version v0 validée : étiquette `v0` posée sur `main`, branche `dev` créée pour la suite.
- Constat de test : le stockage local est inaccessible dans l'aperçu intégré (SecurityError sur file://), le code le gère déjà par try/catch et le panneau affiche maintenant "inaccessible ici" au lieu d'un trompeur "0 octet". Corollaire : le scénario que je croyais avoir écrasé dans la session précédente ne l'a jamais été, l'aperçu n'ayant aucun accès au localStorage du navigateur de l'utilisateur.

## 2026-08-28 (suite)
- Débits affichés en m³/h partout (cartes, notes, vérification d'existant, synthèse) : le L/h des tables COSTIC ne parle pas à l'utilisateur. Le calcul reste en L/h en interne, conversion à l'affichage sur trois décimales pour ne rien perdre sur les petites boucles (0,085 m³/h à 0,2 m/s dans un cuivre 12/14). Le champ de saisie de l'existant a changé d'identifiant (`vDebitM3`) pour qu'un scénario enregistré en L/h ne soit pas relu dans la mauvaise unité.
- Ajout d'un sélecteur de mode de production en tertiaire (instantané, semi-instantané, semi-accumulation, accumulation), en réponse à la question de l'utilisateur. Le mode ne change pas la méthode (le bilan de pointe reste valable pour tous) : il fixe le point visé sur la courbe volume/puissance et l'efficacité de stockage de la technologie associée. Un comparatif des quatre modes est affiché, chacun avec ses propres hypothèses, le mode retenu surligné.
- L'efficacité de stockage est désormais préremplie par le mode (0,90 ballon stratifié sur échangeur externe selon ThermExcel, 0,75 ballon à échangeur incorporé selon Energie+ 0,5-0,8), au lieu d'un 0,85 global sans justification. Reste modifiable.
- Correction d'un défaut de fond : la puissance plafonnait artificiellement (26,2 kW quel que soit le volume au-delà de 2 500 L sur un hôtel) parce que la fenêtre de recharge valait 4 h pour tous les usages, ce qui suppose plusieurs pointes par jour. L'accumulation était donc inatteignable. La fenêtre est maintenant celle du profil journalier réel de l'usage en mode accumulation (hôtel 20 h, restauration 5 h, sport 3 h, etc.) et reste à 4 h hors accumulation, un semi-accumulateur se dimensionnant sur un temps de remontée visé et non sur le temps disponible. Ces fenêtres sont des hypothèses non normées, signalées comme telles dans l'interface et dans docs/methodes.md.
- Nouveau signal automatique : sur les usages à pointes rapprochées (restauration, sport), l'accumulation demande plus de volume ET plus de puissance que la semi-accumulation ; l'outil le dit explicitement au lieu de laisser lire un tableau trompeur.
- Vérification : 7 usages x 4 modes passés au banc, aucune erreur, aucun NaN, dans le rendu comme dans la synthèse. Hôtel 70 chambres à 80 % : instantané 78,6 kW sans stockage, semi-instantané 1 000 L / 52,4 kW, semi-accumulation 2 500 L / 26,2 kW, accumulation 6 000 L / 13,1 kW.
- Écart signalé à l'utilisateur : un test a écrasé son scénario "Hotel Ibis" en localStorage, restauré ensuite.

## 2026-08-28
- Cadrage validé par l'utilisateur : 7 usages dès la v1 (logement, bureaux, hôtel, restaurant, sport/vestiaires, santé, scolaire), méthode COSTIC/ADEME pour le stockage, bouclage par pertes thermiques, et les 4 fonctionnalités secondaires (vérification d'existant, impression propre, localStorage, multi-scénarios).
- Recherche documentaire (3 agents web) : guide ADEME/COSTIC 2016 (besoins habitat, formules de pointe), guide ADEME/EDF/GRDF/COSTIC 2019 (couples volume/puissance P = 14.V^-0,365 et 17.V^-0,385, volume minimal, surpuissance bouclage 2,5x), étude COSTIC/GRDF/ADEME 2020 (ratios tertiaire à 40 °C), guide COSTIC/ADEME 2021 bouclage (débit, pertes, vitesses, diamètres cuivre), arrêté du 30/11/2005 vérifié sur Légifrance. Tout est consigné avec sources et niveaux de confiance dans docs/methodes.md.
- Développement de index.html : une page autonome, moteur de calcul pur (méthode COSTIC en logement, bilan de pointe type ThermExcel en tertiaire, bouclage NF DTU 60.11 via guide 2021), formulaires par usage avec défauts sourcés et bouton "défaut", multi-scénarios en onglets (localStorage), vérification d'existant avec badges d'écart, impression A4 propre, copie de synthèse texte.
- Thème repris du Sélectionneur de radiateurs (2026-07-07) à la demande de l'utilisateur : palette papier/encre, primaire olive, clair/sombre via data-theme + réglage système, police Inter sans requête externe, impression forcée en clair.
- Vérification croisée dans le navigateur : 48 T3 social -> 3 360 L/j à 60 °C, pointe 1 h 1 286 L, 1 000 L -> 54 kW ; hôtel 50 chambres 3 ét. -> 6 240 L/j à 40 °C, recommandation 2 000 L / 21,8 kW ; restaurant traditionnel 200 repas -> 5 000 L/j à 40 °C, 1 500 L / 17,4 kW ; bouclage 100 m De28 classe 4 -> 1 481 W, 255 L/h, retour cuivre 20/22. Ordres de grandeur conformes au métier.
- Hypothèses signalées comme non sourcées ou fragiles (à valider en usage réel) : fractions de pointe bureaux/santé/scolaire, ratio hôtel 1-2 étoiles, ratio internat (source belge), barème annexe 1 de l'arrêté de 2005 (non reproduit sur Légifrance).
- Reste à faire : v2 possible (pertes annuelles du bouclage en kWh, comparateur multi-méthodes côte à côte, export JSON des scénarios) ; confrontation des résultats à un vrai projet BET.
- Création du projet à partir du modèle `application`, depuis le gestionnaire.
- Idée d'origine déplacée depuis dev/_ideas/ (fichier idee-origine.md).
- Installation de GitHub CLI (gh 2.98.0) via winget, connexion au compte GitHub mamalric (compte professionnel, à ne pas confondre avec Marckuss).
- Création du dépôt privé https://github.com/mamalric/calculette-ecs-bouclage et premier push.
- FICHE.md renseignée (pitch, tags, stack, lancer, depot).
- Décision : stack HTML/CSS/JS vanilla en une page autonome, conformément à la convention "petits outils" (le champ type reste `application`, valeur posée par le gestionnaire).
- En attente : validation du cadrage (types de bâtiments v1, méthodes de calcul, hypothèses par défaut) avant tout développement.
