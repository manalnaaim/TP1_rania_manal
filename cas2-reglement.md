# Fiche de cadrage : Questions sur le règlement intérieur

> Remplir chaque rubrique en une à trois phrases. Les rubriques marquées (obligatoire) sont vérifiées par `pytest`.

## Besoin en une phrase (obligatoire)

Répondre aux questions des étudiants sur le règlement intérieur en s'appuyant sur les documents officiels de l'école.

## Utilisateur final (obligatoire)

Les étudiants, qui posent leurs questions en libre-service, et le personnel administratif qui vérifie les réponses litigieuses.

## Approche retenue (obligatoire)

Cocher une seule case :

- [ ] Règles métier
- [ ] Machine learning
- [x] RAG
- [ ] Modèle génératif seul

## Justification (obligatoire, citer au moins deux critères de la grille : (a) données étiquetées, (b) vérifiabilité, (c) coût par requête, (d) conséquence d'une erreur)

Les documents existent déjà (règlement intérieur) et la réponse doit être tirée de ces documents pour être vérifiable (b) : le RAG retrouve le passage pertinent puis génère une réponse ancrée avec citation de la source. On ne dispose pas de questions étiquetées en quantité (a), ce qui exclut le ML. Une réponse inventée aurait une conséquence disciplinaire réelle pour l'étudiant (d), ce qui écarte le génératif seul. Le coût par requête (c) reste modéré (recherche + génération courte).

## Données nécessaires et leur origine (obligatoire)

Le règlement intérieur officiel de l'école (PDF/DOCX), découpé en sections indexées, avec la date de version de chaque document.

## Métrique de succès et seuil d'acceptation (obligatoire)

Taux de réponses correctes sur un jeu de 50 questions de référence ≥ 0,90, avec citation de la source présente dans 100 % des réponses.

## Conséquence d'une erreur et validation humaine prévue (obligatoire)

Une réponse fausse peut induire l'étudiant en erreur sur une règle disciplinaire ; la source est toujours affichée et le personnel administratif peut corriger une réponse signalée.

## Risques éthiques ou de confidentialité (obligatoire)

Les questions peuvent contenir des données personnelles ; éviter de les stocker en clair et anonymiser les journaux.

## Approche écartée et pourquoi (facultatif)

Modèle génératif seul : il peut inventer une règle inexistante, avec un risque disciplinaire réel pour l'étudiant.