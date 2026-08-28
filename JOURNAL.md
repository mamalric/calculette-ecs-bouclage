# Journal

<!-- Dernière entrée en haut. Une entrée par session de travail ou par décision. Date au format AAAA-MM-JJ. -->

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
