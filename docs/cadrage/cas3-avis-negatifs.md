# Fiche de cadrage : Priorisation des avis négatifs

> Remplir chaque rubrique en une à trois phrases. Les rubriques marquées (obligatoire) sont vérifiées par `pytest`.

## Besoin en une phrase (obligatoire)
Classer automatiquement les avis clients selon leur tonalité (négative, neutre, positive) afin que l'équipe support traite en priorité les avis négatifs.


## Utilisateur final (obligatoire)
L'équipe support client et les responsables qualité du site e-commerce, qui trient et traitent les avis chaque jour.


## Approche retenue (obligatoire)

Cocher une seule case :

- [ ] Règles métier
- [x] Machine learning
- [ ] RAG
- [ ] Modèle génératif seul

## Justification (obligatoire, citer au moins deux critères de la grille : (a) données étiquetées, (b) vérifiabilité, (c) coût par requête, (d) conséquence d'une erreur)
Le site dispose de milliers d'avis, et l'équipe peut en annoter quelques centaines en positif/négatif pour entraîner un modèle supervisé (a). Une fois entraîné, le modèle classe un avis en quelques millisecondes, avec un coût par requête négligeable même à grande échelle (c). La conséquence d'une erreur reste modérée : un avis mal classé est simplement traité plus tard, sans danger pour l'utilisateur (d).


## Données nécessaires et leur origine (obligatoire)
Les avis clients déjà stockés sur le site, dont un échantillon de quelques centaines à un millier est annoté manuellement par l'équipe support. Les avis non annotés servent ensuite à l'évaluation.


## Métrique de succès et seuil d'acceptation (obligatoire)
Sur un jeu de test annoté, une exactitude (accuracy) d'au moins 85 % et un rappel d'au moins 90 % sur la classe « négatif », car ce sont les avis négatifs que l'on veut surtout ne pas manquer.


## Conséquence d'une erreur et validation humaine prévue (obligatoire)
Un avis négatif mal classé peut retarder la prise en charge d'un client mécontent, mais sans conséquence grave (d). Les avis classés « négatifs » par le modèle sont relus par un opérateur avant toute action, et les cas ambigus sont signalés pour annotation.

## Risques éthiques ou de confidentialité (obligatoire)
Les avis peuvent contenir des données personnelles (nom, commande) : ils doivent être anonymisés avant entraînement. Un biais est possible si le modèle apprend à classer selon le vocabulaire d'un type de client, d'où la nécessité d'un jeu d'annotation varié et d'une évaluation par catégorie.

## Approche écartée et pourquoi (facultatif)
Les règles métier (listes de mots négatifs) ont été écartées : elles ne capturent ni la négation ni le sarcasme et demandent une maintenance constante. Le RAG ne s'applique pas, car il n'y a pas de document de référence à citer pour classer un avis.