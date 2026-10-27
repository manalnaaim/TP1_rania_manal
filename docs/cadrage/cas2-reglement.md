# Fiche de cadrage : Questions sur le règlement intérieur

> Remplir chaque rubrique en une à trois phrases. Les rubriques marquées (obligatoire) sont vérifiées par `pytest`.

## Besoin en une phrase (obligatoire)
Permettre aux étudiants de poser une question en langage naturel sur le règlement intérieur et obtenir une réponse précise, tirée du document officiel et accompagnée de l'article correspondant.


## Utilisateur final (obligatoire)
L'étudiant ou le personnel administratif de l'école, qui consulte le règlement sans avoir à le lire en entier ni à solliciter le secrétariat.


## Approche retenue (obligatoire)

Cocher une seule case :

- [ ] Règles métier
- [ ] Machine learning
- [x] RAG
- [ ] Modèle génératif seul

## Justification (obligatoire, citer au moins deux critères de la grille : (a) données étiquetées, (b) vérifiabilité, (c) coût par requête, (d) conséquence d'une erreur)
Les documents existent déjà sous forme de texte, et aucune question étiquetée n'est disponible au départ : le RAG s'appuie directement sur les articles sans nécessiter de corpus annoté (a). Chaque réponse doit pouvoir être rattachée à un article précis du règlement, ce que le RAG permet en citant le passage source (b). Enfin, une erreur sur une règle (date limite, sanction) a des conséquences réelles pour l'étudiant (d), ce qui rend la traçabilité de la réponse indispensable.


## Données nécessaires et leur origine (obligatoire)
Le texte intégral du règlement intérieur, fourni par l'administration, découpé en passages (articles ou paragraphes) puis indexé dans une base vectorielle. Aucune donnée d'entraînement supplémentaire n'est requise.


## Métrique de succès et seuil d'acceptation (obligatoire)
Sur un jeu de 50 questions types rédigées par l'administration, au moins 90 % des réponses doivent citer le bon article, et aucune réponse ne doit inventer une règle absente du document.


## Conséquence d'une erreur et validation humaine prévue (obligatoire)
Une réponse fausse sur une règle (date, obligation, sanction) peut induire l'étudiant en erreur (d). L'outil affiche toujours l'article source et un avertissement invitant à vérifier auprès du secrétariat en cas de doute ; aucune réponse n'est présentée comme définitive.


## Risques éthiques ou de confidentialité (obligatoire)
Le règlement intérieur est public, donc le risque de fuite de données est faible. Le risque principal est l'hallucination : le modèle pourrait inventer une règle, d'où l'obligation de citer la source et de limiter les réponses aux passages retrouvés.


## Approche écartée et pourquoi (facultatif)
Le modèle génératif seul a été écarté : sans document source, il peut inventer des règles, ce qui est inacceptable pour un règlement officiel. Les règles métier ne conviennent pas non plus, car les questions sont ouvertes et le vocabulaire varie.