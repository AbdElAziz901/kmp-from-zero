# TP 3 — FollowMyCrypto : à toi de jouer

Les deux dernières séances sont un **projet en binôme** : vous partez de l'application du TP 2 et vous la faites évoluer. C'est ce travail qui est noté.

| # | Page |
|---|---|
| 1 | [Les évolutions](01-evolutions.md) : ce que vous pouvez ajouter à l'application |
| 2 | [L'évaluation](02-evaluation.md) : la grille de notation et la présentation |

## 🗓️ Le déroulé

**Séance 3 (4h)**

| Durée | Quoi |
|---|---|
| 10 min | Rappel du TP 2 : ViewModel, état de l'interface, repository |
| 15 min | [Étape 7 du TP 2](../tp2/07-explorer-l-api.md) : vous explorez l'API Binance |
| 50 min | [Étapes 8](../tp2/08-bibliotheques.md) et [9](../tp2/09-appel-reseau.md), ensemble : les bibliothèques, puis l'appel réseau |
| 20 min | [Étape 10](../tp2/10-navigation-et-detail.md), en démonstration : la navigation et l'écran de détail |
| 10 min | Pause, récupération du point de départ, formation des binômes |
| 2h15 | Projet |

**Séance 4 (3h)**

| Durée | Quoi |
|---|---|
| 1h30 | Projet |
| 1h30 | Présentations : 8 minutes par binôme |

Vous avez donc **3h45** de projet. Ce n'est pas beaucoup : choisissez vos évolutions en conséquence.

## 🏁 Le point de départ

Tout le monde repart du même code : la fin du TP 2, avec la liste, l'appel à l'API Binance, la navigation et l'écran de détail.

```bash
git stash                      # met ton travail de côté
git fetch --tags --force
git checkout tp2-end
git switch -c projet           # votre branche de travail
```

Pas à l'aise avec Git ? Télécharge le zip de `tp2-end` depuis le [README du dépôt](../../README.md).

Un seul des deux récupère le projet ; l'autre le clone ensuite, ou vous travaillez à deux sur le même poste.

✅ Vous êtes prêts si l'application affiche les vrais cours et qu'un clic sur une crypto ouvre son détail.

## 🧭 Avant d'écrire du code

Prenez dix minutes pour faire le tour de ce que vous avez entre les mains. Pour chaque fichier, vous devez pouvoir dire à quelle couche il appartient :

```
shared/src/commonMain/kotlin/com/bvic/followmycrypto/
├── App.kt                         la navigation
├── model/Crypto.kt                le modèle
├── data/
│   ├── CryptoRepository.kt        le contrat du repository
│   ├── RemoteCryptoRepository.kt  l'implémentation réseau, et le mapper
│   ├── FakeCryptoRepository.kt    l'implémentation de test
│   ├── AppContainer.kt            l'injection de dépendances
│   └── remote/                    l'API et le DTO
└── ui/
    ├── list/                      l'écran liste : composables, ViewModel, état
    ├── detail/                    l'écran de détail : composables, ViewModel, état
    ├── components/                les composables partagés
    └── format/                    l'affichage des nombres
```

Pour chaque évolution, posez-vous la même question avant de commencer : **quelles couches faut-il modifier ?**

## 🤝 Travailler à deux

- **Découpez** : une évolution qui touche la liste et une qui touche le détail peuvent avancer en parallèle.
- **Commitez souvent**, une évolution à la fois. Un commit qui marche vaut mieux qu'une évolution à moitié finie le jour de la présentation.
- **Chacun doit pouvoir expliquer tout le code**, y compris celui écrit par l'autre : c'est vérifié à la présentation.

---

[Les évolutions ➡️](01-evolutions.md)
