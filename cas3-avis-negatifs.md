# Fiche de cadrage : Priorisation des avis négatifs

> Remplir chaque rubrique en une à trois phrases. Les rubriques marquées (obligatoire) sont vérifiées par `pytest`.

## Besoin en une phrase (obligatoire)

Prioriser automatiquement les avis négatifs d'un site e-commerce afin que le service client les traite en premier.

## Utilisateur final (obligatoire)

Les conseillers du service client, qui reçoivent une file d'avis déjà triée par niveau de négativité.

## Approche retenue (obligatoire)

Cocher une seule case :

- [ ] Règles métier
- [x] Machine learning
- [ ] RAG
- [ ] Modèle génératif seul

## Justification (obligatoire, citer au moins deux critères de la grille : (a) données étiquetées, (b) vérifiabilité, (c) coût par requête, (d) conséquence d'une erreur)

Des milliers d'avis sont disponibles et peuvent être étiquetés positif/négatif via les notes basses puis annotation manuelle d'un échantillon : les données étiquetées existent en quantité (a). Le langage naturel est varié, donc une règle simple ne suffit pas, ce qui justifie un modèle ML. Un avis mal classé a une conséquence limitée (d) : au pire un avis négatif traité un peu plus tard, sans risque grave, et le score reste vérifiable (b) par le conseiller. Le coût par requête (c) est faible une fois le modèle entraîné (inférence locale).

## Données nécessaires et leur origine (obligatoire)

Avis texte et notes attribuées par les clients, extraits de la base du site ; étiquetage par seuil sur les notes basses (1–2 étoiles), affiné par annotation manuelle sur un échantillon.

## Métrique de succès et seuil d'acceptation (obligatoire)

F1 macro sur un jeu de test tenu à l'écart ≥ 0,85, avec un rappel d'au moins 0,90 sur la classe « négatif » (la plus utile au service client).

## Conséquence d'une erreur et validation humaine prévue (obligatoire)

Un avis négatif mal classé est traité plus tard ; le conseiller peut reprioriser manuellement et ce retour alimente le réentraînement.

## Risques éthiques ou de confidentialité (obligatoire)

Les avis contiennent des données personnelles : anonymisation avant stockage, modèle hébergé en interne, pas d'envoi à un service tiers ; surveiller les biais de vocabulaire.

## Approche écartée et pourquoi (facultatif)

Règles par mots-clés : trop de formulations imprévues, un simple lexique négatif rate les avis ironiques ou implicites.