# Méthodes de calcul et sources

Ce document trace l'origine de chaque valeur et de chaque formule utilisée par la calculette. Règle du projet : aucune valeur sans source identifiée. Les niveaux de confiance indiqués sont : haute (document institutionnel consulté directement), moyenne (valeur de seconde main concordante entre plusieurs sources), faible (source unique ou non institutionnelle, à faire valider).

## Sources principales

- [G1] ADEME/COSTIC, "Les besoins d'eau chaude sanitaire en habitat individuel et collectif", guide technique réf. 8809, mai 2016. https://www.precarite-energie.org/IMG/pdf/besoin-eau-chaude-sanitaire-habitat-individuel-et-collectif-8809.pdf (aussi sur costic.com et ademe.fr)
- [G2] COSTIC sous l'égide de GRDF et de l'ADEME, "Vers une meilleure connaissance des besoins d'eau chaude sanitaire en tertiaire", septembre 2020. https://www.mapes-pdl.fr/wp-content/uploads/2020/10/ECS-ADEME-COSTIC-Besoins-ECS-tertiaire.pdf
- [G3] SOCOL (Enerplan, avec ADEME, GRDF, INES, TECSOL), "Fiche technique : ratios des besoins en ECS pour le dimensionnement des installations en solaire thermique collectif", 2021. https://www.solaire-collectif.fr/photo/img/2021/OUTILS/210209_Fiche-ratios-de-dimensionnement_21_VF.pdf (fourchettes volontairement basses, pensées pour le solaire)
- [G4] Energie+ (UCLouvain, Belgique), "Consommation d'eau chaude sanitaire". https://energieplus-lesite.be/donnees/consommations2/consommation-d-eau-chaude-sanitaire/ (valeurs belges, confiance moyenne, utilisées en recoupement seulement)

## 0. Conversions et constantes

- Capacité thermique volumique de l'eau : c = 1,163 Wh/(L.K).
- Conversion d'un volume entre températures de référence (équivalence énergétique), [G1] p. 23 : V(T2) = V(T1) x (T1 - Tef) / (T2 - Tef), avec Tef la température d'eau froide.
- Températures d'eau froide mesurées sur 100 sites ([G1]) : 16 °C en moyenne annuelle (plus ou moins 2), 21 °C en juillet-août (plus ou moins 3), 9 °C en moyenne au minimum hivernal. La valeur 9 °C sert au dimensionnement de pointe.
- Attention aux références : les valeurs ADEME/COSTIC récentes sont exprimées en litres à 40 °C, les anciennes valeurs conventionnelles et les fiches solaires en litres à 60 °C. Toute comparaison passe par la formule de conversion ci-dessus.

## 1. Besoins journaliers par usage

### 1.1 Logement collectif / individuel ([G1], confiance haute)

Valeurs mesurées, absences comprises, incluant une part des pertes de distribution.

- Moyenne tous ménages : 56 L/j/personne à 40 °C (écart-type 23). Soit 35 L/j/personne à 55 °C pour Tef 16 °C.
- Par taille de ménage (L/j/personne à 40 °C) : 1 pers : 80 ; 2 pers : 60 ; 3 pers : 50 ; 4-5 pers : 45 ([G1] p. 7).
- Échelle immeuble : 125 L/j/logement standard à 40 °C, soit 70 L/j/logement standard à 60 °C (Tef 16 °C) ([G1] p. 14). Le logement standard est un T3 du parc social occupé par 2,1 personnes.
- Par typologie, échelle logement (L/j à 40 °C, [G1] fig. 5) : T1 : 75 ; T2 : 80 ; T3 : 100 (privé) à 110 (social) ; T4 : 110 (privé) à 145 (social) ; T5 : 140 (privé) à 190 (social).
- Occupation conventionnelle et coefficient d'équivalence "logement standard" Ns ([G1] fig. 13 et 29, source USH-DEEF/INSEE) :

| Type | Occupants (privé) | Coeff. Ns (privé) | Occupants (social) | Coeff. Ns (social) |
|---|---|---|---|---|
| T1 | 1,2 | 0,6 | 1,2 | 0,6 |
| T2 | 1,4 | 0,7 | 1,4 | 0,7 |
| T3 | 1,9 | 0,9 | 2,1 | 1,0 |
| T4 | 2,3 | 1,1 | 3,0 | 1,4 |
| T5 | 2,7 | 1,3 | 3,7 | 1,8 |
| T6+ | 2,9 | 1,4 | 3,9 | 1,9 |

- Besoins de pointe pour le dimensionnement (échelle immeuble, litres à 60 °C, Tef 9 °C, [G1] fig. 30) :

| Durée | Formule | Validité |
|---|---|---|
| 10 min | V = 61 x n^0,503 (n = nombre de logements) | n > 10 |
| 1 h | V = 83 x Ns^0,708 (Ns = logements standards) | Ns > 10 |
| 2 h | V = 108 x Ns^0,773 | Ns > 20 |
| 3 h | V = 116 x Ns^0,815 | Ns > 20 |
| 4 h | V = 162 x Ns^0,789 | Ns > 20 |
| 5 h | V = 189 x Ns^0,784 | Ns > 20 |
| 6 h | V = 241 x Ns^0,758 | Ns > 20 |
| 7 h | V = 277 x Ns^0,75 | Ns > 20 |
| 8 h | V = 294 x Ns^0,762 | Ns > 20 |

- Coefficients saisonniers ([G3]) : janvier-mai 1,1 ; juin 0,85 ; juillet-août 0,75 ; septembre 0,9 ; octobre 1,05 ; novembre-décembre 1,1.
- Ancienne base conventionnelle de dimensionnement : environ 120 L/j/logement à 60 °C (Cegibat GRDF, "Évolution des besoins d'ECS en résidentiel", confiance moyenne). Les pointes plurihoraires COSTIC récentes sont en moyenne trois fois plus faibles que celles de la recommandation AICVF 02-2004 (FFB). La recommandation AICVF est payante et non reproduite ici.

### 1.2 Bureaux / tertiaire ([G2], confiance haute)

- 5 à 10 L/employé/jour ouvré à 40 °C (hors douches de salle de sport et hors restaurant d'entreprise), [G2] fig. 144.
- 0,1 à 0,3 L/m²/jour ouvré à 40 °C, [G2] p. 150.
- Recoupement [G4] : 2 à 6 L/pers/j à 60 °C (confiance moyenne).

### 1.3 Hôtellerie ([G2], confiance haute sauf mention)

- Hôtels 3 étoiles (37 hôtels-restaurants, 2 800 relevés mensuels, hors lingerie) : 78 L/nuitée à 40 °C (écart-type 21).
- Hôtels 4 étoiles (42 hôtels, hors lingerie) : 108 L/nuitée à 40 °C (écart-type 31).
- Hôtels 5 étoiles : environ 3 fois la valeur 3 étoiles, soit de l'ordre de 230 L/nuitée à 40 °C (échantillon de 4 hôtels seulement, confiance moyenne).
- Environ 1,6 client par chambre occupée ; taux d'occupation moyens 54 à 69 % selon classement (INSEE/DGE, cités dans [G2]).
- Fourchettes basses solaire à 60 °C ([G3]) : éco 30, 1-2 étoiles 45, 3-4 étoiles 60, 5 étoiles 80 L/chambre/j.
- Valeurs Cegibat 2017 par étoile (60 à 180 L/chambre/j à 40 °C plus supplément repas) : non vérifiées finement, confiance faible à moyenne, non codées.

### 1.4 Restauration ([G2] fig. 144 et section 3.3, confiance haute pour les mesures, moyenne pour la synthèse bibliographique)

Litres par repas à 40 °C :

- Collective, liaison froide, lave-vaisselle en eau froide : 2 à 3.
- Collective, liaison froide, lave-vaisselle en ECS : 5 à 10.
- Collective, préparation sur place, lave-vaisselle eau froide : 5 à 15.
- Collective, préparation sur place, lave-vaisselle en ECS : 10 à 25.
- Restauration rapide et self-service : 7 à 14 (biblio).
- Restauration traditionnelle : 15 à 35 (biblio).
- Restauration gastronomique : 22 à 40 (biblio).
- Petit-déjeuner : 4 à 7 (confiance moyenne).

### 1.5 Santé ([G2] fig. 144, confiance haute sauf mention)

Litres par lit et par jour à 40 °C :

- EHPAD sans restauration ni lingerie (69 sites) : 10 à 20.
- EHPAD, liaison froide + lave-vaisselle ECS, sans lingerie : 20 à 40.
- EHPAD, liaison froide + lave-vaisselle ECS + lingerie ECS : 30 à 65.
- EHPAD, cuisine sur place + lave-vaisselle ECS + lingerie ECS : 40 à 95.
- Hôpitaux (7 sites, services variés) : 15 à 90. Valeur de référence citée par Cegibat : 80 à 100 (confiance moyenne).
- Cliniques : pas de valeur spécifique trouvée, utiliser la fourchette hôpitaux.
- Lingerie : 4 à 8 L/kg de linge (valeur type 6) ; 2 à 4 kg de linge/lit/j en EHPAD.
- Pointe 10 min EHPAD : moins de 8 L/lit à 40 °C (5 EHPAD instrumentés, Cegibat, confiance moyenne).

### 1.6 Scolaire ([G2] fig. 144, confiance haute)

Litres par élève et par jour de classe à 40 °C :

- Externat sans restauration (52 sites) : 2 à 4.
- Demi-pension liaison froide : 4 à 7 (lave-vaisselle eau froide) ; 7 à 12 (lave-vaisselle ECS).
- Demi-pension cuisine sur place : 7 à 14 (lave-vaisselle eau froide) ; 12 à 21 (lave-vaisselle ECS).
- Lycées avec internat (5 à 50 % d'internes, liaison froide, 29 sites) : 6 à 44.
- Lycées avec internat, cuisine sur place + lave-vaisselle ECS : 14 à 64.
- Internat, hébergement seul : 30 à 40 L/lit/j à 60 °C ([G4], confiance moyenne).

### 1.7 Sport / vestiaires ([G2] fig. 114, confiance haute pour la source, moyenne pour les valeurs issues de sa synthèse bibliographique)

- Gymnases, sports en salle : 45 à 50 L/pratiquant à 40 °C.
- Vestiaires de stade (football/rugby) : 65 à 75 L/pratiquant à 40 °C.
- Piscines : 10 à 30 L/baigneur à 40 °C (4 sites).
- Débit de douche : 6 L/min en robinetterie temporisée (temporisation 30 s), 8 à 10 L/min en robinetterie ancienne ; une douche de vestiaire représente 45 à 75 L à 40 °C soit 6 à 12 minutes.
- Attention : très forte dépendance à la fréquentation réelle (mesuré 9 L/poste de douche/j sur un stade contre 168 en bibliographie). La calculette prend la fréquentation en entrée plutôt qu'une constante par poste de douche.
- Les besoins journaliers d'un stade peuvent atteindre 5 fois la moyenne annuelle ([G2] section 4.2).

## 2. Dimensionnement du stockage

Sources spécifiques :

- [S1] ADEME/EDF/GRDF/COSTIC, "Le dimensionnement des systèmes de production d'eau chaude sanitaire en habitat individuel et collectif", juin 2019, ADEME réf. 010888, ISBN 978-2-36301-015-5. PDF : https://cegibat.grdf.fr/pdf/7984/3090 (aussi sur costic.com)
- [S2] ThermExcel, "Programme ECSTHERM - Dimensionnement de la production ECS" (J.-Y. Messe, 2014). https://www.thermexcel.com/french/divers/ThermExcel%20-%20Production%20ECS.pdf (source professionnelle non normative)
- [S3] Cegibat GRDF, dossiers "Le besoin d'ECS dans les établissements de santé" et "dans les établissements hôteliers" (études COSTIC/GRDF). https://cegibat.grdf.fr/dossier-techniques/besoin-eau-chaude-sanitaire-etablissements-sante et https://cegibat.grdf.fr/dossier-techniques/besoin-eau-chaude-sanitaire-etablissements-hoteliers
- [S4] Livret SOCOL "Eau technique", 2021. https://www.solaire-collectif.fr/photo/img/Livreteautechnique/210208_Livret-SOCOL-Eau-Technique_VF.pdf

### 2.1 Habitat collectif : méthode COSTIC ([G1] et [S1], confiance haute)

La base de besoins du guide 2019 est exprimée à 60 °C avec eau froide 10 °C ; la pointe 10 minutes y vaut V10min = 60 x n^0,503 (n = nombre de logements). Les pointes plurihoraires du guide 2016 (tableau en section 1.1) sont établies pour eau froide 9 °C.

Modes de production et formules exactes ([S1]) :

- Instantané pur (déconseillé par le guide sans stockage primaire) : débit de pointe instantané = 1,3 x débit de pointe 10 minutes, soit qmax = 468 x n^0,503 L/h à 60 °C ; P = qmax x 1,16 x (60 - 10) / 1000.
- Échangeur + ballon, circulation (charge) permanente : P (kW par logement standard, régime 10/60 °C) = 14 x V^-0,365, avec V le volume total de stockage en litres. Validité : au moins 10 logements standards, différentiel de régulation inférieur ou égal à 5 K, plages de volume de la fig. 26 (exemple 10 logements : 300 à 750 L).
- Échangeur + ballon, avec arrêts de la circulation : P (kW/logement standard) = 17 x V^-0,385. Volume minimal ([S1] p. 23) : Vl = V10min x (2,4 + 0,18 x Pboucle) = n^0,503 x (144 + 10,8 x Pboucle), Vl en litres, Pboucle en kW (0 si le bouclage n'est pas réchauffé par la production).
- Accumulation pure (reconstitution nocturne) : capacité supérieure ou égale aux besoins journaliers maximaux, pris égaux à 2 fois les besoins moyens ([S1] fig. 70, valeurs par typologie parc social : T1 90, T2 105, T3 150, T4 210, T5 270, T6+ 285 L/j à 60 °C). Puissance = reconstitution en 6 à 8 h : P = 1,163e-3 x V x (60 - 10) / tr.
- Réchauffage du bouclage par la production : puissance supplémentaire = 2,5 x pertes du bouclage ([S1] p. 41). Le guide bouclage 2021 ([B1] fig. 82) donne 3 à 5 fois les pertes selon le point de raccordement du retour sur un ballon à échangeur : la calculette affiche 2,5 x en valeur de base et rappelle la fourchette.
- Ratio pointe 1 h / besoin moyen journalier = 0,6 x Ns^-0,23 ([S1] fig. 19).
- Le guide COSTIC n'utilise aucun coefficient explicite de stratification : il est intégré dans les abaques. La fourchette "0,7 à 0,9" parfois citée n'a pas de source publique identifiée et n'est pas utilisée.

### 2.2 Tertiaire : méthode des besoins par profil de puisage ([S2], confiance haute pour la lecture, source non normative)

Pour les usages hors habitat, la calculette applique la méthode classique du bilan sur la période de pointe :

- Énergie de la pointe : E_pointe = 1,163e-3 x V_pointe x (Tref - Tef), avec V_pointe le volume puisé pendant la pointe à sa température de référence.
- Bilan pendant la pointe de durée tp : E_pointe = R x V_stock x (Tsto - Tef) x 1,163e-3 + P x tp. R est le coefficient d'efficacité du stockage (stratification) : 0,80 à 0,95 selon [S2] ("de mauvaise à bonne stratification"), 0,5 à 0,8 pour un ballon à échangeur incorporé selon Energie+.
- Reconstitution du stock pendant la fenêtre de recharge tr : P x tr supérieur ou égal à R x V_stock x (Tsto - Tef) x 1,163e-3.
- La puissance requise pour un volume donné est le maximum des contraintes ; la calculette présente la gamme de volumes standards avec la puissance associée, jusqu'au palier au-delà duquel agrandir le ballon n'apporte plus rien.

#### Modes de production en tertiaire

COSTIC ne publie pas d'abaques volume/puissance par mode hors habitat : la méthode reste le bilan sur la pointe, identique quel que soit le mode. Le mode ne change donc pas la physique, il désigne le point de fonctionnement visé sur la courbe volume/puissance et l'efficacité de stockage de la technologie associée. La calculette affiche les quatre modes en comparatif, chacun avec ses propres hypothèses.

| Mode | Volume visé | Efficacité R par défaut | Fenêtre de recharge |
|---|---|---|---|
| Instantané | aucun stockage, P = E_pointe / tp | sans objet (0,90 affiché) | sans objet |
| Semi-instantané | stock couvrant 25 % de l'énergie de pointe | 0,90 (ballon stratifié sur échangeur externe, [S2] 0,80-0,95) | 4 h |
| Semi-accumulation | volume au palier de puissance | 0,85 (ballon stratifié chargé par un échangeur externe, [S2] 0,80-0,95) | 4 h |
| Accumulation | stock couvrant le besoin journalier | 0,90 (ballon de stockage stratifié, [S2]) | fenêtre par usage, voir ci-dessous |

Les cibles de 25 % pour le semi-instantané et le choix d'associer une technologie à chaque mode sont des conventions de l'outil, pas des valeurs publiées : elles positionnent des points de repère sur une courbe qui, elle, est calculée. L'efficacité reste modifiable pour coller au matériel réel.

Cas de l'instantané : la puissance affichée est la moyenne sur la durée de la pointe. Le débit de pointe instantané est supérieur (facteur 1,3 sur la pointe 10 minutes en habitat, [S1]) : la valeur est à recaler sur le foisonnement réel des puisages. Le guide COSTIC déconseille par ailleurs l'instantané pur sans stockage.

#### Fenêtre de recharge

Hors accumulation, la fenêtre est fixée à 4 heures : on ne dimensionne pas un semi-accumulateur sur le temps disponible avant la pointe suivante mais sur un temps de remontée en température visé, sinon le ballon grossit sans fin pour un gain de puissance négligeable.

En accumulation, la fenêtre est le temps réellement disponible avant la pointe suivante, déduit du profil journalier de l'usage. HYPOTHÈSES DE TRAVAIL NON NORMÉES, signalées comme telles dans l'interface, car ce sont elles qui fixent la puissance en accumulation : bureaux 8 h, hôtel 20 h (une seule pointe le matin), restauration 5 h (deux services), santé 10 h, scolaire 18 h, sport 3 h (créneaux successifs).

Conséquence utile : sur les usages à pointes rapprochées (restauration, sport), l'accumulation demande à la fois plus de volume et plus de puissance que la semi-accumulation, et n'a donc aucun intérêt. La calculette le signale automatiquement.

Profils de pointe par défaut par usage (modifiables dans l'interface) :

- Hôtel : pointe 2 h = 60 % de la consommation journalière (hôtels de tourisme, [S2] p. 22 ; pointe du matin dominante confirmée par [S3], pointe 10 min = 10 à 35 % du besoin journalier). Confiance moyenne.
- Restaurant : pointe structurelle = repas du service de pointe x ratio par repas, sur la durée du service (pas de coefficient inventé).
- Santé : pointe 10 min = 61 x n^0,503 L à 60 °C avec n = nombre de lits, n > 10 ([S4] p. 5, citant COSTIC/GRDF, confiance haute) ; pic dominant 8 h - 10 h, pointe 10 min inférieure à 8 L/lit à 40 °C et jusqu'à 20 % du besoin journalier en EHPAD ([S3], confiance moyenne). Fraction de pointe 2 h par défaut : 40 %, hypothèse de travail non normée, signalée dans l'interface.
- Sport/vestiaires : pointe structurelle = douches du créneau de pointe (pratiquants du créneau x litres par douche) sur la durée du créneau de douches.
- Bureaux : fraction de pointe 1 h par défaut 25 %, hypothèse de travail non normée, signalée dans l'interface.
- Scolaire : pointe par défaut = service de midi (50 % du besoin sur 1,5 h), hypothèse de travail non normée, signalée dans l'interface.

### 2.3 Cadre réglementaire température ([B3] et [S1], confiance haute sauf mention)

- Stockage total supérieur ou égal à 400 L : eau en permanence à 55 °C au moins en sortie des équipements, ou montée quotidienne à température suffisante (barème annexe 1 de l'arrêté : 2 min à 70 °C, ou 4 min à 65 °C, ou 60 min à 60 °C ; annexe non reproduite sur Légifrance, valeurs concordantes chez Cegibat, confiance moyenne).
- Distribution : 50 °C minimum en tout point si le volume entre production et puisage le plus éloigné dépasse 3 L ; antennes non bouclées 3 L maximum (et 8 m maximum selon NF DTU 60.11 P1-2).
- Points de puisage : 50 °C maximum dans les pièces destinées à la toilette, 60 °C maximum dans les autres pièces ; dans les cuisines et buanderies des ERP, jusqu'à 90 °C possible en des points signalés.
- Surveillance légionelles (ERP, santé, hôtels...) : arrêté du 1er février 2010 modifié (seuil Legionella pneumophila 1000 UFC/L aux points d'usage), complété par les arrêtés du 30 décembre 2022.

### 2.4 Hors périmètre chiffré (pas de source publique suffisante)

- Recommandation AICVF 02-2004 : document payant, coefficients non reproduits.
- Valeurs Cegibat par étoile d'hôtel (60 à 180 L/chambre/j à 60 °C) : non recoupées finement, utilisées seulement pour l'option "1-2 étoiles" avec signalement de confiance faible dans l'interface.
- Hôtels 1-2 étoiles et 5 étoiles : échantillons mesurés COSTIC trop faibles ; l'interface le signale.

## 3. Bouclage

Sources spécifiques :

- [B1] COSTIC, "La conception des réseaux bouclés d'eau chaude sanitaire", guide technique ADEME/EDF, février 2021, 116 p., ISBN 978-2-36301-017-9. https://cegibat.grdf.fr/sites/default/files/assets/GUIDE%20bouclage-Fev%202021-FF.pdf (aussi sur librairie.ademe.fr et costic.com). Référence publique la plus complète, dérivée du NF DTU 60.11 P1-2 (août 2013).
- [B2] Programme RAGE/PACTE, "Installations d'eau chaude sanitaire - Confort, prévention des risques et maîtrise des consommations", novembre 2014. https://www.programmepacte.fr/sites/default/files/pdf/guide-rage-installations-eau-chaude-sanitaire-2014-11_0.pdf
- [B3] Article 36 de l'arrêté du 23 juin 1978 modifié par l'arrêté du 30 novembre 2005. https://www.legifrance.gouv.fr/loda/article_lc/LEGIARTI000006828036
- [B4] Caleffi, "Réussir l'équilibrage du bouclage", 2015. https://www.caleffi.com/sites/default/files/media/external-file/08615_FR.pdf
- [B5] ThermExcel, "Bouclages eau chaude sanitaire". https://www.thermexcel.com/french/ressourc/plomberie_bouclage_eau_chaude_sanitaire_ecs.htm

Nota : les valeurs issues du NF DTU 60.11 P1-2 et du NF DTU 60.1 (documents AFNOR payants) sont citées de seconde main via [B1], [B2] et [B4], concordantes entre elles. Une vérification sur le texte AFNOR reste souhaitable pour un livrable contractuel.

### 3.1 Cadre réglementaire ([B3], confiance haute)

- Température supérieure ou égale à 50 °C en tout point du système de distribution (hors tubes finaux d'alimentation) dès que le volume entre production et point de puisage le plus éloigné dépasse 3 litres.
- Stockage de plus de 400 L : au moins 55 °C en sortie de stockage en permanence, ou montée en température quotidienne.
- Aux points de puisage : 50 °C maximum dans les pièces destinées à la toilette, 60 °C maximum ailleurs.
- Consigne de production recommandée : 60 °C ([B1] p. 9 ; 55 °C en consigne ne permet généralement pas de tenir 50 °C au bouclage).

### 3.1 bis Mode de maintien en température

Le couple aller plus retour ne vaut que pour un réseau bouclé. Trois modes sont proposés, qui ne se calculent pas de la même façon :

- Réseau bouclé (aller + retour + circulateur) : c'est le cas traité par [B1] et le NF DTU 60.11. Pertes = aller + retour, débit de recirculation, diamètre de retour, puissance de compensation.
- Traçage électrique (ruban ou cordon chauffant) : pas de canalisation de retour ni de circulateur, un cordon posé le long de l'aller compense les pertes en ligne. Il n'y a donc ni débit ni diamètre de retour, et les pertes valent environ la moitié de celles d'un réseau bouclé de même tracé. Ordre de grandeur publié : environ 7 W/m avec un calorifuge correct (Energie+, https://energieplus-lesite.be/concevoir/eau-chaude-sanitaire3/concevoir-globalement-ecs/choisir-le-reseau-d-eau-chaude-sanitaire/), et une consommation d'environ 60 % de celle d'une boucle, mais en électricité directe. Limite d'emploi : plus de circulation en période de non-puisage et panne de cordon difficile à détecter, d'où un risque légionelles accru (Batirama, https://www.batirama.com/article/1512-reseaux-d-eau-chaude-bouclage-ou-cordon-chauffant.html). Confiance moyenne sur la valeur de 7 W/m, source non normative.
- Sans maintien en température : ni retour ni traçage. Admis seulement si le volume entre production et point de puisage le plus éloigné reste inférieur ou égal à 3 litres ([B3]) et si l'antenne ne dépasse pas 8 m (NF DTU 60.11 P1-2). Aucune puissance de compensation.

Conséquence sur le reste du calcul : seul le réseau bouclé alimente la surpuissance de production (section 2.1). Un traçage est électrique et indépendant de la production ECS.

### 3.1 ter Architecture du bouclage ([B1] fig. 15 p. 18-20 et fig. 16 p. 21, confiance haute)

Le guide compare plusieurs architectures et publie leurs écarts de longueurs et de pertes thermiques, calculés sur l'immeuble de référence de 12 logements, par rapport à une distribution traditionnelle en colonnes montantes. Il précise que les écarts de longueurs en pourcentage correspondent pratiquement aux écarts de pertes, l'influence des diamètres étant limitée à niveau d'isolation identique : appliquer le pourcentage aux pertes est donc légitime.

| Architecture | Écart de pertes | Remarque |
|---|---|---|
| Colonnes montantes (traditionnel) | référence | Distribution verticale, colonnes en gaines techniques |
| Distribution horizontale par étage | +5 % | Écart très variable selon le bâtiment : 5 % sur l'immeuble R+2 de référence, jusqu'à 30 % sur un EHPAD R+3 (fig. 16). Recommandée en santé, pour permettre les coupures par service |
| Parapluie, collecteur aller vertical commun | -7 % | Longueurs -9 %, mais collecteur d'alimentation plus long |
| Parapluie, collecteur retour vertical commun | -9 % | Longueurs -9 %. Risque de retours inverses si les clapets défaillent |
| Parapluie, première colonne commune | -17 % | Longueurs -20 %. Première colonne de plus gros diamètre |
| Colonnes en U inversé | -16 % | Longueurs -18 %. Divise par deux le nombre de boucles et réduit le débit total |
| Horizontale avec retours plus courts | -17 % | Longueurs -21 %. Plus onéreuse, multiplie les coudes sensibles à la corrosion-érosion en cuivre |

Le coefficient n'est à utiliser qu'en avant-projet, sur des longueurs estimées pour un tracé traditionnel. Si les longueurs saisies sont celles du réseau réellement tracé, garder l'architecture de référence, qui n'applique aucune correction.

### 3.1 quater Nombre de boucles

Un réseau réel se découpe en plusieurs boucles, chacune avec son retour raccordé sur un collecteur ([B1] fig. 1, définitions du NF DTU 60.11 P1-2). Le débit total se répartit entre les boucles : chaque retour est dimensionné pour sa part, le collecteur pour le total. Modéliser un long réseau en une seule boucle conduit à un diamètre de retour démesuré, sans rapport avec la pratique.

Le guide proscrit à l'inverse le multibouclage ([B1] p. 16) : un nombre de boucles élevé est ingérable à l'exploitation et impose des débits de bouclage très élevés, puisque chaque retour doit conserver au moins 0,2 m/s. La calculette reproduit cet effet et le signale quand le plancher de vitesse impose un débit supérieur à celui qu'exigent les pertes.

Solutions publiées pour éviter le multibouclage ([B1] p. 16) : regrouper les points de puisage, rapprocher le réseau par des dévoiements plutôt que créer une boucle, différencier les parcours aller et retour pour desservir plus de points par boucle, recourir à plusieurs productions ou sous-stations, ou traiter en production décentralisée les points trop éloignés (au-delà d'environ 15 m).

### 3.2 Débit de bouclage ([B1] p. 51-61, confiance haute)

- Formule : Q (L/h) = P (W) / (1,16 x deltaT), avec P les pertes thermiques du réseau bouclé et deltaT la chute de température admissible entre sortie de production et point le plus défavorisé.
- Chute maximale : 5 K (jusqu'à 7 K si la sortie de production ne descend jamais sous 57 °C ; ne pas viser moins de 5 K, surdébits inutiles), [B1] p. 51-52.
- Méthode NF DTU 60.11 P1-2 (via [B1]) : le débit de chaque boucle est d'abord fixé au minimum satisfaisant v = 0,2 m/s, puis la chute de température est vérifiée tronçon par tronçon ; le débit n'est augmenté que si la chute dépasse la limite. La calculette applique : débit retenu = max(débit issu des pertes ; débit assurant 0,2 m/s dans le retour).

### 3.3 Pertes thermiques ([B1] p. 33-36 et annexe 1, confiance haute)

- Formule : P = k x L x (Tecs - Tamb), avec k en W/(m.K) le coefficient de pertes du tube calorifugé, Tamb la température ambiante minimale des locaux traversés (dimensionnement).
- Classes d'isolation NF EN 12828 (k maximal en W/(m.K), d = diamètre extérieur du tube nu en mètres) : classe 1 : 3,3d + 0,22 ; classe 2 : 2,6d + 0,20 ; classe 3 : 2,0d + 0,18 ; classe 4 : 1,5d + 0,16 ; classe 5 : 1,1d + 0,14 ; classe 6 : 0,8d + 0,12.
- Ordre de grandeur : 7 à 10 W/m en classe 4 pour des tubes De 14 à 64, eau 60 °C, ambiance 20 °C ([B1] fig. 28 p. 34). Ratio RAGE : environ 10 W/m en classe 2 et 5 W/m en classe 6 ([B2] fig. 45 p. 56).
- Extrait cuivre / laine minérale 0,035 revêtue alu (k en W/(m.K), [B1] annexe 1) : épaisseur 30 mm : De 14 : 0,12 ; De 16 : 0,13 ; De 18 : 0,13 ; De 22 : 0,15 ; De 28 : 0,17 ; De 35 : 0,19 ; De 42 : 0,21 ; De 54 : 0,25 ; De 64 : 0,28.
- Ambiance 10 °C au lieu de 20 °C : environ 20 % de pertes en plus. Ambiances usuelles : sous-sol 10 °C, gaines techniques 20 °C ([B1] p. 35 et 58).
- Tube non calorifugé : de l'ordre de 26 à 85 W/m selon matériau et diamètre ([B1] fig. 29, appariement diamètre/valeur à confirmer visuellement, confiance moyenne).

### 3.4 Vitesses et diamètres ([B1] p. 45-55, [B2] p. 100, confiance haute)

- Retour de bouclage : vitesse entre 0,2 m/s (minimum NF DTU 60.11, turbulence, limite biofilm) et 0,5 m/s. Cuivre : moins de 0,3 m/s conseillé en régime permanent (corrosion-érosion).
- Aller : 1,5 m/s maximum en colonnes et logements, 2 m/s en sous-sol ; collecteur de retour 1 m/s maximum.
- Diamètre minimal du retour : cuivre 12/14, PVC-C 12,4/16, PEX/PB 13/16, autres matériaux 12 mm intérieur. Acier galvanisé à proscrire en bouclage ([B1] p. 67) et jamais en aval de cuivre.
#### Matériaux et diamètres commerciaux

Le matériau se choisit séparément pour l'aller et pour le retour. En pratique une boucle est posée dans un seul matériau, aller et retour étant tirés ensemble : le matériau du retour reprend donc par défaut celui de l'aller, la distinction ne servant qu'aux rénovations partielles. Le matériau de l'aller détermine les diamètres proposés et, par son diamètre extérieur, le coefficient de pertes de la classe d'isolation. Le matériau du retour détermine en plus la vitesse limite de dimensionnement.

Débits correspondant aux vitesses de 0,2 m/s (minimum) et à la vitesse maximale retenue, [B1] fig. 45 p. 55. Le diamètre intérieur minimal d'un retour est de 12 mm.

Cuivre, débits en L/h à 0,2 / 0,3 / 0,5 m/s. La vitesse de dimensionnement retenue est 0,3 m/s, conseillée en permanent pour limiter la corrosion-érosion aux tés et raccords :

| di/de | 0,2 m/s | 0,3 m/s | 0,5 m/s |
|---|---|---|---|
| 12/14 | 85 | 120 | 200 |
| 13/15 | 100 | 140 | 235 |
| 14/16 | 115 | 165 | 275 |
| 16/18 | 145 | 215 | 360 |
| 20/22 | 230 | 335 | 565 |
| 26/28 | 385 | 570 | 955 |
| 33/35 | 620 | 920 | 1535 |
| 38/40 | 820 | 1220 | 2040 |
| 40/42 | 905 | 1355 | 2260 |
| 51/54 | 1475 | 2205 | 3675 |
| 52/54 | 1530 | 2290 | 3820 |
| 60/64 | 2040 | 3050 | 5085 |

PVC-C, débits en L/h à 0,2 / 0,5 m/s. PN25 : 12,4/16 : 90 / 215 ; 15,4/20 : 135 / 335 ; 19,4/25 : 215 / 530 ; 24,8/32 : 350 / 865 ; 31/40 : 545 / 1355 ; 38,8/50 : 855 / 2125 ; 48,8/63 : 1350 / 3365. PN16 : 21,2/25 : 255 / 635 ; 27,2/32 : 420 / 1045 ; 34/40 : 655 / 1630 ; 42,6/50 : 1030 / 2565 ; 53,6/63 : 1625 / 4060 ; 63,8/75 : 2305 / 5750.

Multicouche : le guide donne les diamètres extérieurs en annexe 1 (16, 18, 20, 26, 32, 40, 50, 63 mm) avec leurs coefficients de pertes par classe d'isolation, mais **aucune table de débits**. Les débits sont donc calculés par Q = v x pi x di² / 4 sur des diamètres intérieurs commerciaux courants (12/16, 14/18, 16/20, 20/26, 26/32, 33/40, 42/50, 54/63), qui varient d'un fabricant à l'autre. CONFIANCE FAIBLE sur ces diamètres intérieurs, signalée dans l'interface : les vérifier sur la documentation du produit retenu.

Nota : les valeurs publiées pour le cuivre et le PVC-C sont reprises telles quelles et non recalculées, le guide arrondissant ses débits (85 L/h annoncés contre 81 calculés pour un di de 12 mm, par exemple).

Acier galvanisé : à proscrire en bouclage ([B1] p. 67) et jamais en aval d'éléments en cuivre (NF DTU 60.1). Il n'est donc pas proposé.

Nota d'affichage : les tables sources sont en L/h, mais l'interface exprime tous les débits en m³/h (division par 1000, trois décimales), unité de travail de l'utilisateur.

- Débits par diamètre cuivre ([B1] fig. 45 p. 55), en L/h à 0,2 / 0,3 / 0,5 m/s : 12/14 : 85 / 120 / 200 ; 14/16 : 115 / 165 / 275 ; 16/18 : 145 / 215 / 360 ; 20/22 : 230 / 335 / 565 ; 26/28 : 385 / 570 / 955 ; 33/35 : 620 / 920 / 1535 ; 40/42 : 905 / 1355 / 2260 ; 52/54 : 1530 / 2290 / 3820 ; 60/64 : 2040 / 3050 / 5085.
- Débit plancher de fait par boucle : 85 à 90 L/h (v = 0,2 m/s dans le diamètre minimal). Aucune source normative publique n'impose un forfait "50 ou 60 L/h par boucle".
- Antenne non bouclée : 8 m maximum (NF DTU 60.11 P1-2) et 3 L maximum entre production et puisage ([B3]).

### 3.5 Puissance de compensation ([B1] p. 54, 96 et 102, confiance haute)

- Pertes du bouclage = somme aller + retour du réseau bouclé, calculées sans soutirage, aux ambiances minimales. Exemple [B1] : 12 logements, 1 kW total (0,6 kW aller + 0,4 kW retour) pour 360 L/h.
- Réchauffeur de boucle dédié : puissance = pertes thermiques maximales du bouclage.
- Réchauffage par la production (ballon à échangeur) : la puissance supplémentaire à prévoir vaut environ 3 fois les pertes (retour raccordé au niveau du serpentin) à 5 fois les pertes (retour au-dessus de l'échangeur), [B1] fig. 82 p. 96.

### 3.6 Équilibrage (rappels affichés, non calculés)

- Ouverture supérieure ou égale à 1 mm des organes d'équilibrage (NF DTU 60.11 P1-2).
- Perte de charge minimale de la vanne d'équilibrage : 200 mmCE (300 mmCE si mesure de débit par prises de pression), [B1] p. 61.
- Perte de charge totale du circuit le plus défavorisé, production incluse : 5 mCE maximum ; échangeur ECS : moins de 2 mCE.

## 4. Conventions du schéma de principe

Le schéma qui accompagne les résultats n'entre dans aucun calcul : il illustre l'architecture, le mode de maintien et le mode de production retenus, pour rendre visible une différence que le tableau chiffré ne montre pas. Le tracé des réseaux suit [B1] fig. 15 p. 18-20 ; les conventions de fluides ci-dessous sont propres à l'outil.

Trois fluides, trois couleurs, et surtout deux circuits qui ne communiquent jamais.

- **Eau froide sanitaire** : arrive du réseau de ville, en pied de ballon, ou au piquage bas du secondaire de l'échangeur en production instantanée.
- **ECS et retour de bouclage** : le circuit sanitaire proprement dit, puisé en haut du ballon, repris en pied.
- **Primaire** : le fluide chauffant. Sur tous les modes disposant d'un ballon, le secondaire de l'échangeur à plaques est une **boucle fermée non potable** qui alimente le serpentin du ballon. Ce fluide ne rencontre nulle part l'eau sanitaire : l'échange se fait à travers la paroi du serpentin.

Le serpentin est toujours dessiné dans la partie basse du ballon, à hauteur constante, et raccordé par ses deux extrémités basses. C'est là qu'il réchauffe l'eau la plus froide sans brasser la stratification, dont le maintien conditionne l'efficacité R retenue au 2.2.

**Exception de l'instantané.** Produire de l'ECS sans stockage suppose un échange direct vers l'eau sanitaire : il n'existe pas de variante à boucle fermée. Sur ce mode l'échangeur dessiné est donc l'échangeur ECS lui-même, l'eau froide entrant à son piquage bas et l'ECS sortant au piquage haut, le primaire restant cantonné aux deux piquages de gauche. En réseau bouclé, le retour se mélange à l'eau froide en amont de l'échangeur. La séparation des fluides reste assurée par les plaques, comme sur tout échangeur ECS.

En accumulation, il n'y a pas d'échangeur externe : le primaire alimente directement le serpentin.
