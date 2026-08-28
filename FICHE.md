---
id: 2026-08-28-calculette-ecs-et-bouclage     # AAAA-MM-JJ-slug, écrit une fois, jamais modifié (même si le dossier bouge)
nom: Calculette ECS et Bouclage               # nom affiché
type: application                             # application | outil | documentation | travail | affaire
statut: actif                                 # idee | actif | pause | termine | abandonne
pitch: Calculette web pour estimer le stockage ECS et dimensionner le bouclage d'un bâtiment selon son usage.  # une phrase sur une seule ligne, 120 caractères maximum
cree: 2026-08-28                              # AAAA-MM-JJ
maj: 2026-08-28                               # AAAA-MM-JJ, mis à jour par Claude Code en fin de session
tags: [cvc, plomberie, ecs, bouclage, calculette]  # exemple : [cvc, reglementation]
stack: HTML + CSS + JS vanilla, une seule page, sans build
lancer: ouvrir index.html dans un navigateur
depot: https://github.com/mamalric/calculette-ecs-bouclage
---

# Calculette ECS et Bouclage

## Objectif
Estimer le besoin de stockage ECS d'un bâtiment (logement, bureaux, hôtel, restaurant, etc.) et dimensionner son bouclage (débit, pertes thermiques, puissance de compensation, diamètre indicatif du retour). Outil de travail pour ingénieur BET fluides / CVC, avec méthodes et hypothèses sourcées (DTU 60.11, COSTIC, guides professionnels) affichées avec chaque résultat.

## État actuel
Version v0 validée et étiquetée sur `main` (le développement continue sur la branche `dev`). 7 usages (logement, bureaux, hôtel, restaurant, santé, scolaire, sport), stockage par méthode COSTIC (logement) ou bilan de pointe avec choix du mode de production et comparatif des quatre modes (tertiaire), bouclage complet (pertes, débit en m³/h, diamètre retour, puissance), multi-scénarios, vérification d'existant, impression, thème clair/sombre et panneau "À propos" (rouage) repris du Sélectionneur de radiateurs. Toutes les valeurs sont sourcées (docs/methodes.md) ; les hypothèses non normées sont signalées dans l'interface. Vérifiée sur les 7 usages et les 4 modes dans le navigateur.

## Prochaine étape
Confronter les résultats à un projet BET réel et ajuster les hypothèses signalées (fractions de pointe et fenêtres de recharge en tertiaire, ratio hôtel 1-2 étoiles) ; v2 possible : pertes annuelles de bouclage en kWh, export JSON des scénarios.

## Utilisation
Aucun prérequis : ouvrir index.html dans un navigateur (fichier autonome, une seule page, fonctionne hors ligne). Les scénarios sont conservés localement (localStorage).
