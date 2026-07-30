# Conventions du dépôt

## Messages de commit

Format [Conventional Commits](https://www.conventionalcommits.org/fr/) : un type, une portée optionnelle, un sujet à l'impératif.

```
type(portée): sujet en minuscule, sans point final

Corps facultatif : ce que ça change et pourquoi, pas comment.
Les chiffres avant/après sont plus utiles qu'un adjectif.

Refs #12
```

### Types

| Type | Usage |
|---|---|
| `feat` | Nouvelle fonctionnalité, nouvel écran, nouveau champ |
| `fix` | Correction d'un défaut de comportement |
| `data` | Ajout ou correction de contenu du catalogue, sans changement de code |
| `refactor` | Réécriture sans changement de comportement observable |
| `test` | Ajout ou correction de vérifications |
| `docs` | README, ce fichier, commentaires de fond |
| `chore` | Outillage, configuration, tâches d'entretien |

`data` n'est pas dans la spécification d'origine. Il est ajouté ici parce que l'essentiel du travail sur ce projet consiste à écrire des entrées de catalogue, et que les confondre avec `feat` rendrait l'historique illisible.

### Portées

`catalogue`, `moteur`, `interface`, `audit`, `stockage`, `profil`.

### Exemples

```
data(catalogue): ajoute 40 documentaires pour le registre apprendre
feat(interface): affiche les distinctions et le repère sur la fiche
fix(moteur): aligne le battement du sablier sur l'entracte affiché
test(audit): couvre les douze natures d'anomalie
docs: consigne la convention de commits
```

### Rupture de compatibilité

Un `!` après le type, et un paragraphe `BREAKING CHANGE:` dans le corps. Sur ce projet, cela concerne surtout le schéma de stockage : toute évolution de `VERSION_SCHEMA` doit être accompagnée d'une migration dans `migrer()`.

## Branches

Une branche par intention, nommée en français avec des tirets : `lot-documentaires-et-apprendre`, `outil-de-validation-du-catalogue`. Jamais de commit direct sur `main` : `main` est publié automatiquement sur GitHub Pages.

## Avant d'ouvrir une pull request

1. Ouvrir l'application et vérifier que le script se charge — une entrée de catalogue mal formée casse tout le fichier, silencieusement.
2. Passer par **Données → Vérifier le catalogue**. Aucune anomalie « bloquant » ni « sérieux » ne doit apparaître, et aucun signal ne doit concerner les entrées ajoutées.
3. Décrire dans la PR ce qui a été vérifié, et signaler ce qui reste approximatif.

## Écrire une entrée de catalogue

Voir les règles de saisie dans l'issue #6.

### Valeurs contraintes

Ces champs n'acceptent qu'une liste fermée. Toute autre valeur est refusée par `valider_oeuvre` et remonte en « bloquant » dans l'audit.

| Champ | Valeurs |
|---|---|
| `f` — format | `film` `serie` `doc` |
| `c` — climat | `soleil` `pluie` `ville` `ailleurs` |
| `e` — époque | `passe` `present` `imaginaire` |
| `fin` | `sombre` `douce` `ouverte` |
| `g` — registres | `eblouissement` `tension` `refuge` `rire` `apprendre` |
| `x` — exigence | `1` `2` `3` |

Le piège le plus fréquent est de mettre une **étiquette** dans un de ces champs : `foret` ou `mer` dans `c`, `aventure` dans `g`. Les étiquettes vont dans `tg`, et nulle part ailleurs.

### Contrôler un lot avant de le livrer

L'application contient son propre validateur. Il faut s'en servir **avant** de committer, pas après :

1. Insérer le lot dans le tableau `CATALOGUE`.
2. Ouvrir le fichier dans un navigateur. Si l'application ne s'affiche pas, une entrée est mal formée et casse tout le script.
3. Aller dans **Données → Vérifier le catalogue**.
4. Corriger jusqu'à **zéro « bloquant » et zéro « sérieux »**, et zéro signal portant sur les entrées ajoutées.

Ce que l'audit attrape et qu'une relecture rate : valeurs hors liste, clés en double, voisins pointant sur l'œuvre elle-même, voisins absents du catalogue, doublons probables (même année et même réalisateur), titres suffixés, distinctions sans millésime.

### Pièges connus

- **La dernière entrée du tableau `CATALOGUE` n'a pas de virgule finale.** Insérer après elle sans l'ajouter casse tout le script, alors que chaque entrée reste valide isolément.
- **Ne pas créer d'étiquette nouvelle sans nécessité.** Le vocabulaire fait tenir les cycles et les fils rouges ; un synonyme involontaire les vide en silence.
- **Ne jamais ajouter une variante d'un titre déjà présent** — `restauré`, `saison 2`, `version longue`, `(reprise)`. C'est un doublon, pas une œuvre. L'audit les signale, mais mieux vaut ne pas les écrire.
- **Supprimer une entrée pendant la préparation d'un lot casse les voisins qui la citaient.** Refaire l'audit après toute suppression.
- **Un guillemet double dans un champ texte casse la ligne entière.** Utiliser les guillemets français « … ».
