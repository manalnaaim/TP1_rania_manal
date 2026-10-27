# Démarche à suivre pour le test

Ce dépôt se vérifie de deux façons, qui contrôlent les mêmes choses : `scripts/check_setup.py` parle aux humains (lignes OK, ATTENTION, ERREUR) et `pytest` parle à la machine (38 tests, repris par la CI et par la notation).

Suivez les six étapes dans l'ordre. Chaque étape donne le résultat attendu : si vous obtenez autre chose, la section « Lire un échec » à la fin dit quoi corriger.

## Étape 0. Ce que donne le kit fraîchement décompressé

Avant toute installation, dans le dossier `sentiment-app` :

```bash
python -m venv .venv
source .venv/bin/activate          # Windows PowerShell : .venv\Scripts\Activate.ps1
pip install pandas scikit-learn pytest
pytest -q
```

Résultat attendu : **3 failed, 31 passed, 4 skipped**.

C'est normal, et c'est le point de départ du TP :

- les 3 échecs sont dans `tests/test_cadrage.py` : les fiches de cadrage sont vides (partie A) ;
- les 4 tests ignorés attendent un dépôt Git : 3 dans `tests/test_git_history.py`, 1 dans `tests/test_environment.py` (`test_no_real_env_file_committed`) ;
- les 31 tests verts confirment que la structure, les paquets et le `.gitignore` sont en place.

## Étape 1. Installer l'environnement complet

```bash
bash scripts/setup.sh                                          # Linux, macOS, Git Bash
powershell -ExecutionPolicy Bypass -File scripts\setup.ps1     # Windows
```

Le script vérifie Python, crée `.venv`, installe `requirements.txt`, écrit `requirements.lock`, puis lance le diagnostic. Comptez 5 à 10 minutes la première fois.

## Étape 2. Lire le diagnostic

```bash
python scripts/check_setup.py
```

Le script imprime cinq blocs : Python, Paquets, Structure du dépôt, Git, Fiches de cadrage, puis un résumé `N erreur(s), M avertissement(s)`. Il renvoie le code de sortie 1 s'il reste une erreur.

| Ligne | Sens |
| --- | --- |
| `OK` | rien à faire |
| `ATTENTION` | ne bloque pas, mais doit disparaître avant la fin de la séance (fiches vides, un seul auteur de commits) |
| `ERREUR` | bloque : venv non activé, paquet absent, dossier manquant, pas de dépôt Git, `.venv/` suivi par Git |

Objectif à la fin du TP : `0 erreur(s), 0 avertissement(s)`. Sur une version de Python autre que 3.11, un avertissement de version subsiste : c'est le seul toléré.

## Étape 3. Tester la partie A, les fiches de cadrage

```bash
pytest tests/test_cadrage.py -q
```

Résultat attendu une fois les trois fiches remplies : **12 passed**. Les quatre contrôles sont :

1. trois fichiers `docs/cadrage/cas*.md` existent ;
2. les huit rubriques obligatoires sont présentes dans chaque fiche ;
3. chaque rubrique contient au moins une phrase (20 caractères hors consigne et cases à cocher) ;
4. exactement une case `- [x]` est cochée, et la justification cite au moins deux critères parmi `(a)`, `(b)`, `(c)`, `(d)`.

## Étape 4. Tester la partie B, l'environnement et le dépôt

```bash
pytest tests/test_environment.py -q     # attendu : 23 passed
pytest tests/test_git_history.py -q     # attendu : 3 passed
```

`test_git_history.py` exige deux auteurs de commits distincts, un par membre du binôme. Tant qu'un seul membre a commité :

```text
1 auteur(s) de commits, 2 attendus (un par membre du binôme) : ['Membre A']
```

Vérifiez qui a commité avec `git shortlog -sn --all`. Si les deux noms sont identiques, chacun corrige son identité avec `git config --global user.name "Prénom Nom"` puis refait un commit.

## Étape 5. Tout lancer, comme la CI

```bash
pytest -q
```

Résultat attendu en fin de TP : **38 passed** (23 + 12 + 3). Poussez, puis ouvrez l'onglet Actions sur GitHub : le workflow `.github/workflows/ci.yml` rejoue exactement ces 38 tests sur une machine neuve, en Python 3.11. Une CI verte veut dire que le dépôt tient debout ailleurs que sur vos deux portables.

## Étape 6. Refaire le test de l'enseignant

La note se joue sur un clone frais : reproduisez-le avant de partir, dans un autre dossier.

```bash
cd /tmp
git clone https://github.com/<organisation>/sentiment-app.git verif
cd verif
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python scripts/check_setup.py
pytest -q
```

Si cette suite passe sans intervention manuelle, le TP est rendu. Supprimez ensuite le dossier `verif`.

## Lire un échec

| Message | Cause | Correction |
| --- | --- | --- |
| `test_virtualenv_active` échoue | pytest lancé hors du venv | activer le venv, ou `.venv/bin/python -m pytest` |
| `ModuleNotFoundError: pandas` | venv non activé, ou pip d'un autre Python | `which python`, puis `python -m pip install -r requirements.txt` |
| `rubriques vides ou trop courtes : cas2-reglement.md / Justification` | rubrique laissée vide | remplir la rubrique nommée dans le message |
| `cocher exactement une approche` | zéro ou deux cases `- [x]` | une seule approche par fiche |
| `la justification doit citer au moins deux critères` | justification sans les lettres de la grille | écrire explicitement `(a)`, `(c)`, etc. |
| `auteur(s) de commits, 2 attendus` | un seul membre a commité, ou même `user.name` | `git config --global user.name`, puis un vrai commit par membre |
| `.venv/ a été commité au moins une fois` | `.venv/` est entré dans l'historique | `git rm -r --cached .venv`, commit ; si l'historique est pollué, recommencer le dépôt |
| `4 skipped` alors que le dépôt est sur GitHub | les tests tournent hors du dossier du dépôt, ou `.git/` absent | lancer pytest depuis la racine du dépôt cloné |

## Résumé des trois états

| État | check_setup.py | pytest |
| --- | --- | --- |
| Kit décompressé, pas de dépôt Git, fiches vides | 1 erreur, 3 avertissements | 3 failed, 31 passed, 4 skipped |
| Dépôt Git initialisé, un seul auteur, fiches vides | 0 erreur, 4 avertissements | 4 failed, 34 passed |
| Fin du TP : fiches remplies, deux auteurs | 0 erreur, 0 avertissement | 38 passed |
