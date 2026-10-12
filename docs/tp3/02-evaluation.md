# 2. L'évaluation

Le projet est noté **par binôme**, sur 20.

## 📊 La grille

| Critère | Points |
|---|---|
| L'évolution obligatoire fonctionne | 4 |
| Les évolutions au choix | 8 |
| Le respect de l'architecture | 4 |
| La présentation | 4 |

### Les évolutions au choix (8 points)

Sont pris en compte :

- **le nombre** d'évolutions terminées ;
- **leur difficulté** : une ⭐⭐⭐ compte davantage qu'une ⭐ ;
- **leur finition** : une évolution est terminée quand elle fonctionne pendant la démonstration **et** qu'elle respecte ses contraintes.

Mieux vaut deux évolutions terminées que quatre à moitié faites.

### Le respect de l'architecture (4 points)

C'est ce que vous avez appris au TP 2, appliqué à votre code :

- Chaque chose est dans **sa couche** : pas d'appel réseau dans un ViewModel, pas de tri ni de filtre dans un composable.
- L'écran est décrit par un **état de l'interface**, exposé en lecture seule par le ViewModel.
- Les composables reçoivent des **données** et remontent des **événements** ; ceux qui affichent du contenu ont un aperçu.
- Les erreurs sont **gérées** : l'application ne plante pas sans réseau.
- L'application **se lance sur Android et sur Desktop**.

### La présentation (4 points)

Voir ci-dessous.

## 🎤 La présentation

**8 minutes par binôme**, à la deuxième moitié de la dernière séance.

| Durée | Quoi |
|---|---|
| 3 min | **Démonstration** de l'application : ce que vous avez ajouté |
| 3 min | **Le code d'une évolution**, au choix : vous suivez la donnée à travers les couches, du clic ou de l'API jusqu'à l'écran |
| 2 min | **Questions** |

Ce qui est attendu :

- Les **deux** membres du binôme parlent.
- Chacun peut être interrogé sur **n'importe quelle partie** du code, y compris celle écrite par l'autre.
- Vous dites ce qui **ne marche pas** ou ce que vous n'avez pas eu le temps de finir : c'est mieux vu qu'une démonstration qui évite le problème.

Quelques questions que vous pouvez préparer :

- Quelles couches cette évolution a-t-elle touchées, et pourquoi pas les autres ?
- Qu'est-ce qui a été le plus difficile ? Comment avez-vous trouvé la solution ?
- Si l'API changeait demain, que faudrait-il modifier ?
- Qu'auriez-vous fait avec deux heures de plus ?

## 📦 Le rendu

À la fin de la dernière séance, le code est poussé sur un dépôt Git (ou envoyé en zip), avec dans le `README` :

- les noms des deux membres du binôme ;
- la liste des évolutions réalisées, et leur état : terminée, partielle, abandonnée.

---

[⬅️ Les évolutions](01-evolutions.md) · [📚 Sommaire](README.md)
