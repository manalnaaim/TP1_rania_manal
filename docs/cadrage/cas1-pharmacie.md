# Fiche de cadrage : Ordonnances incomplètes en pharmacie

> Remplir chaque rubrique en une à trois phrases. Les rubriques marquées (obligatoire) sont vérifiées par `pytest`.

## Besoin en une phrase (obligatoire)
Détecter automatiquement les ordonnances qui manquent d'un champ obligatoire (posologie, durée, signature) avant leur saisie, pour éviter au pharmacien de les repérer à la main.

## Utilisateur final (obligatoire)
Le pharmacien ou le préparateur en officine, qui contrôle l'ordonnance au comptoir avant de délivrer le médicament.


## Approche retenue (obligatoire)

Cocher une seule case :

- [x] Règles métier
- [ ] Machine learning
- [ ] RAG
- [ ] Modèle génératif seul

## Justification (obligatoire, citer au moins deux critères de la grille : (a) données étiquetées, (b) vérifiabilité, (c) coût par requête, (d) conséquence d'une erreur)
Les champs obligatoires d'une ordonnance sont connus et fixés par la réglementation, donc une logique de règles est stable et suffisante (b : vérifiabilité — chaque alerte cite le champ manquant). Le coût par requête est quasi nul puisqu'aucun modèle n'est appelé (c). Enfin, une ordonnance validée à tort peut mettre le patient en danger (d), ce qui plaide pour une règle transparente et auditable plutôt qu'un modèle opaque.


## Données nécessaires et leur origine (obligatoire)
Aucune donnée d'entraînement : il suffit de la liste officielle des champs obligatoires (posologie, durée, signature, identification du prescripteur) issue de la réglementation. Les ordonnances réelles restent dans le système de l'officine et ne sortent pas.


## Métrique de succès et seuil d'acceptation (obligatoire)
Taux de détection des ordonnances réellement incomplètes ≥ 95 %, et taux de fausses alertes ≤ 5 % sur un échantillon de 200 ordonnances relues par le pharmacien.



## Conséquence d'une erreur et validation humaine prévue (obligatoire)
Une ordonnance incomplète non détectée peut conduire à une délivrance dangereuse (d). L'outil ne bloque jamais : il affiche une alerte que le pharmacien confirme ou ignore, et la décision finale reste humaine.



## Risques éthiques ou de confidentialité (obligatoire)
Les ordonnances contiennent des données de santé personnelles : elles ne doivent pas quitter l'officine, et l'outil ne doit conserver aucun contenu au-delà du contrôle. Un biais est possible si le format des ordonnances varie selon les prescripteurs.


## Approche écartée et pourquoi (facultatif)
Le machine learning a été écarté : il faudrait des milliers d'ordonnances étiquetées « incomplète / complète », coûteuses à obtenir, alors que la règle métier est déjà fiable, vérifiable et gratuite à l'usage.