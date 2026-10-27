# Fiche de cadrage : Ordonnances incomplètes en pharmacie

> Remplir chaque rubrique en une à trois phrases. Les rubriques marquées (obligatoire) sont vérifiées par `pytest`.

## Besoin en une phrase (obligatoire)

Détecter automatiquement, à la réception, les ordonnances incomplètes afin que le pharmacien ne valide que des ordonnances complètes et conformes.

## Utilisateur final (obligatoire)

Le pharmacien et son préparateur, qui contrôlent chaque ordonnance avant délivrance.

## Approche retenue (obligatoire)

Cocher une seule case :

- [x] Règles métier
- [ ] Machine learning
- [ ] RAG
- [ ] Modèle génératif seul

## Justification (obligatoire, citer au moins deux critères de la grille : (a) données étiquetées, (b) vérifiabilité, (c) coût par requête, (d) conséquence d'une erreur)

Les champs obligatoires d'une ordonnance sont connus et stables (médecin, patient, date, posologie, signature) : aucune donnée étiquetée n'est nécessaire (a) et une règle déterministe suffit. Une ordonnance validée à tort peut avoir une conséquence médicale grave (d), donc on préfère une décision explicite et auditable, facile à vérifier (b), plutôt qu'un modèle probabiliste. Le coût par requête (c) est quasi nul avec des règles.

## Données nécessaires et leur origine (obligatoire)

Champs obligatoires définis par la réglementation pharmaceutique, saisis dans le logiciel de la pharmacie ; aucune donnée de santé n'est envoyée à un service externe.

## Métrique de succès et seuil d'acceptation (obligatoire)

Taux de détection des ordonnances réellement incomplètes (rappel) ≥ 0,95 et taux de fausses alertes ≤ 0,05 sur un échantillon contrôlé par le pharmacien.

## Conséquence d'une erreur et validation humaine prévue (obligatoire)

Une ordonnance incomplète non détectée peut entraîner un risque médical ; toute alerte est confirmée par le pharmacien, qui garde la décision finale.

## Risques éthiques ou de confidentialité (obligatoire)

Données de santé sensibles : traitement local, pas d'envoi à un service tiers, accès limité au personnel habilité.

## Approche écartée et pourquoi (facultatif)

Machine learning : pas de corpus étiqueté disponible et la logique est déterministe, un modèle apporterait de l'opacité sans gain.