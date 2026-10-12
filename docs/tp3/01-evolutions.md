# 1. Les évolutions

Chaque évolution est décrite par son **résultat attendu**, les **couches** qu'elle touche et quelques **pistes**. Il n'y a pas de solution : c'est à vous de chercher, comme au TP 2.

Le nombre d'étoiles indique la difficulté.

| Évolution | Difficulté | Couches |
|---|---|---|
| [0. Le plus haut et le plus bas sur 24h](#0-le-plus-haut-et-le-plus-bas-sur-24h) | **Obligatoire** | API, repository, modèle, interface |
| [1. Trier la liste](#1-trier-la-liste) | ⭐ | ViewModel, interface |
| [2. Rechercher une crypto](#2-rechercher-une-crypto) | ⭐ | ViewModel, interface |
| [3. Suivre d'autres cryptos](#3-suivre-dautres-cryptos) | ⭐ | Repository |
| [4. Choisir le thème clair ou sombre](#4-choisir-le-thème-clair-ou-sombre) | ⭐ | Interface |
| [5. Afficher les logos](#5-afficher-les-logos) | ⭐⭐ | Bibliothèques, modèle, interface |
| [6. Un squelette de chargement](#6-un-squelette-de-chargement) | ⭐⭐ | Interface |
| [7. Faire clignoter le prix qui change](#7-faire-clignoter-le-prix-qui-change) | ⭐⭐ | Interface |
| [8. Rafraîchir en tirant la liste](#8-rafraîchir-en-tirant-la-liste) | ⭐⭐ | ViewModel, état, interface |
| [9. Rafraîchir automatiquement](#9-rafraîchir-automatiquement) | ⭐⭐ | ViewModel |
| [10. Les favoris](#10-les-favoris) | ⭐⭐ | Repository, ViewModel, état, interface |
| [11. Changer de devise](#11-changer-de-devise) | ⭐⭐ | API, repository, ViewModel, interface |
| [12. Des messages d'erreur précis](#12-des-messages-derreur-précis) | ⭐⭐ | Repository, ViewModel, état, interface |
| [13. Garder les favoris après fermeture](#13-garder-les-favoris-après-fermeture) | ⭐⭐⭐ | Bibliothèques, repository |
| [14. Le graphique du prix](#14-le-graphique-du-prix) | ⭐⭐⭐ | API, repository, modèle, ViewModel, interface |
| [15. Deux panneaux sur grand écran](#15-deux-panneaux-sur-grand-écran) | ⭐⭐⭐ | Interface, navigation |
| [16. Tester le ViewModel](#16-tester-le-viewmodel) | ⭐⭐⭐ | Tests, bibliothèques |
| [17. Votre idée](#17-votre-idée) | à valider | – |

> [!TIP]
> Commencez par l'évolution obligatoire, puis par une ⭐ : mieux vaut trois évolutions terminées qu'une ⭐⭐⭐ qui ne fonctionne pas.

---

## 0. Le plus haut et le plus bas sur 24h

**Obligatoire.** C'est la plus petite évolution qui traverse **toutes** les couches : vous refaites seuls le trajet vu en séance.

🎯 L'écran de détail affiche, sous la variation, le prix le plus haut et le prix le plus bas des dernières 24 heures.

📏 Contraintes :

- Les deux valeurs viennent de l'API : regardez la réponse de Binance, elles y sont déjà.
- `Crypto` reste un modèle propre : des `Double`, pas des `String`.
- `FakeCryptoRepository` continue de fonctionner.

💡 Pistes : suivez la donnée dans l'ordre, du JSON jusqu'à l'écran. Quatre fichiers au moins sont concernés.

---

## 1. Trier la liste

🎯 L'utilisateur choisit l'ordre de la liste : par prix, par variation sur 24h ou par nom.

📏 Contraintes :

- Le tri est fait dans le **ViewModel**, pas dans le composable.
- Le tri choisi reste appliqué après un rafraîchissement.

💡 Pistes : une `enum class` pour les tris possibles ; `sortedBy` et `sortedByDescending` ; pour le choix, des [chips](https://developer.android.com/develop/ui/compose/components/chip) ou un [menu](https://developer.android.com/develop/ui/compose/components/menu).

---

## 2. Rechercher une crypto

🎯 Un champ de texte au-dessus de la liste filtre les cryptos par nom ou par symbole, sans tenir compte des majuscules.

📏 Contraintes :

- Le texte saisi et le filtrage sont dans le **ViewModel**.
- Si aucune crypto ne correspond, l'écran le dit au lieu d'afficher une liste vide.

💡 Pistes : [les champs de texte](https://developer.android.com/develop/ui/compose/text/user-input) ; `filter` et `contains(..., ignoreCase = true)`. Où garder la liste complète pendant qu'on affiche la liste filtrée ?

---

## 3. Suivre d'autres cryptos

🎯 La liste contient au moins quinze cryptos.

📏 Contraintes :

- Aucune modification dans `ui`.
- Chaque crypto ajoutée a son vrai nom.

💡 Pistes : cherchez les paires disponibles sur [binance.com](https://www.binance.com/fr/markets/overview). Que se passe-t-il si vous demandez une paire qui n'existe pas ? Comment l'application réagit-elle ?

---

## 4. Choisir le thème clair ou sombre

🎯 Un bouton dans la barre de titre bascule entre le thème clair et le thème sombre, quel que soit le réglage du téléphone.

📏 Contraintes :

- Le choix s'applique aux **deux** écrans.
- Au premier lancement, l'application suit le réglage du système.

💡 Pistes : regardez la signature de `FollowMyCryptoTheme`. Où doit vivre l'état « thème choisi » pour que toute l'application le voie ? C'est une question de hissage d'état, comme au TP 1.

---

## 5. Afficher les logos

🎯 Chaque ligne de la liste, et l'écran de détail, affichent le logo de la crypto.

📦 Fourni : les logos sont disponibles à l'adresse suivante, avec le symbole en minuscules.

```
https://cdn.jsdelivr.net/gh/spothq/cryptocurrency-icons@master/128/color/btc.png
```

Pour charger une image depuis Internet, utilisez la bibliothèque **Coil**. Versions testées pour ce projet :

| Coordonnées | Version |
|---|---|
| `io.coil-kt.coil3:coil-compose` | 3.6.3 |
| `io.coil-kt.coil3:coil-network-ktor3` | 3.6.3 |

📏 Contraintes :

- Les bibliothèques sont déclarées dans le catalogue de versions, comme à l'étape 8 du TP 2.
- Tant que l'image n'est pas chargée, ou si elle n'existe pas, la ligne affiche autre chose qu'un trou : les initiales, par exemple.

💡 Pistes : [Coil et Compose](https://coil-kt.github.io/coil/compose/), [Coil et le réseau](https://coil-kt.github.io/coil/network/). Qui doit construire l'adresse du logo : le composable, ou le modèle ?

---

## 6. Un squelette de chargement

🎯 Pendant le chargement, l'écran n'affiche plus un indicateur qui tourne mais un **squelette** : des lignes grises à la place des cryptos, parcourues par un reflet animé (effet *shimmer*).

📏 Contraintes :

- Le squelette a la même forme que la vraie liste : même hauteur de ligne, des blocs à la place des textes.
- L'animation tourne en boucle tant que dure le chargement.
- Aucune bibliothèque supplémentaire.

💡 Pistes : `rememberInfiniteTransition`, dans [les animations basées sur une valeur](https://developer.android.com/develop/ui/compose/animation/value-based) ; un dégradé qui se déplace, avec [`Brush`](https://developer.android.com/develop/ui/compose/graphics/draw/brush). Commencez par un squelette immobile, puis animez-le. `FakeCryptoRepository` et son `delay` sont parfaits pour l'observer longtemps.

---

## 7. Faire clignoter le prix qui change

🎯 Quand le prix d'une crypto change après un rafraîchissement, il clignote brièvement : en vert s'il a monté, en rouge s'il a baissé.

📏 Contraintes :

- C'est le composable qui compare le nouveau prix à l'ancien : rien à ajouter au ViewModel.
- Un prix inchangé ne clignote pas, et rien ne clignote au premier affichage.

💡 Pistes : `remember` pour garder le prix précédent, `LaunchedEffect(price)` pour réagir au changement, `animateColorAsState` pour la transition. Voir [le guide des animations](https://developer.android.com/develop/ui/compose/animation/quick-guide). Cette évolution est plus agréable à tester avec le rafraîchissement automatique.

---

## 8. Rafraîchir en tirant la liste

🎯 Tirer la liste vers le bas la rafraîchit. Pendant le rafraîchissement, **la liste reste affichée** avec l'indicateur au-dessus : elle n'est pas remplacée par l'écran de chargement.

📏 Contraintes :

- Le premier chargement garde son écran de chargement plein écran.
- L'état de l'interface doit pouvoir dire « j'ai des données **et** je suis en train de rafraîchir ».

💡 Pistes : [Pull to refresh](https://developer.android.com/develop/ui/compose/components/pull-to-refresh). C'est surtout un travail sur `CryptoListUiState` : que faut-il lui ajouter ?

---

## 9. Rafraîchir automatiquement

🎯 Les prix se mettent à jour tout seuls toutes les dix secondes, sans que l'écran clignote.

📏 Contraintes :

- Le rafraîchissement s'arrête quand on quitte l'écran.
- Si un rafraîchissement automatique échoue, la liste déjà affichée reste à l'écran.

💡 Pistes : une boucle et `delay` dans une coroutine du `viewModelScope`. Relisez la note « Pour aller plus loin » de l'[étape 6 du TP 2](../tp2/06-repository-et-etats.md) : c'est ici qu'elle devient utile. Voir aussi [l'annulation des coroutines](https://kotlinlang.org/docs/cancellation-and-timeouts.html).

---

## 10. Les favoris

🎯 Une étoile sur chaque ligne ajoute ou retire la crypto des favoris. Un filtre n'affiche que les favoris. L'étoile est aussi présente, et à jour, sur l'écran de détail.

📏 Contraintes :

- Les favoris sont gérés par un **nouveau repository**, partagé par les deux écrans via `AppContainer`.
- Il expose les favoris dans un `StateFlow` : quand on change un favori dans le détail, la liste est à jour au retour.
- Les favoris peuvent être perdus à la fermeture de l'application (voir l'évolution 13).

💡 Pistes : un `Set<String>` de symboles suffit. Pour fabriquer un état à partir de **deux** flows (les cryptos et les favoris), regardez `combine` dans [la documentation des flows](https://kotlinlang.org/docs/flow.html). Les [boutons icônes](https://developer.android.com/develop/ui/compose/components/icon-button).

---

## 11. Changer de devise

🎯 L'utilisateur choisit d'afficher les prix en dollars ou en euros.

📏 Contraintes :

- Les prix en euros viennent de Binance : les paires `BTCEUR`, `ETHEUR`… existent. On ne convertit pas soi-même.
- Le symbole affiché à côté du prix suit la devise choisie.
- La devise choisie est connue du ViewModel, pas seulement du composable.

💡 Pistes : quelles couches connaissent aujourd'hui « USDT » ? Le contrat du repository doit-il changer ? Et `formatPrice` ?

---

## 12. Des messages d'erreur précis

🎯 L'écran d'erreur ne dit plus toujours « Impossible de charger les cours » : il distingue au moins l'absence de connexion d'une erreur du serveur.

📏 Contraintes :

- Le ViewModel ne connaît pas Ktor : c'est le repository qui traduit les exceptions techniques en erreurs que l'application comprend.
- L'interface choisit le message à partir du **type** d'erreur, pas d'un texte venu du repository.

💡 Pistes : provoquez les deux cas (coupez le Wi-Fi ; demandez une paire qui n'existe pas) et affichez l'exception pour voir ce que Ktor lève. Voir [la validation des réponses](https://ktor.io/docs/client-response-validation.html). Une `sealed interface` peut décrire vos erreurs, comme elle décrit déjà l'état de l'écran.

---

## 13. Garder les favoris après fermeture

Nécessite l'évolution 10.

🎯 Les favoris sont toujours là quand on relance l'application, sur Android comme sur Desktop.

📦 Fourni : la bibliothèque **Multiplatform Settings**, version testée pour ce projet.

| Coordonnées | Version |
|---|---|
| `com.russhwolf:multiplatform-settings-no-arg` | 1.3.0 |

📏 Contraintes :

- Seul le repository des favoris change. Ni les ViewModels ni les composables ne savent où les favoris sont stockés.

💡 Pistes : [Multiplatform Settings](https://github.com/russhwolf/multiplatform-settings). Elle ne stocke que des valeurs simples : comment enregistrer un ensemble de symboles dans une seule `String` ?

---

## 14. Le graphique du prix

🎯 L'écran de détail affiche la courbe du prix sur les dernières 24 heures.

Le dessin de la courbe est **fourni** : le travail de cette évolution est d'aller chercher les données et de les amener jusqu'à l'écran, à travers toutes les couches.

📦 Fourni : l'API des « bougies » de Binance. Ouvrez-la dans le navigateur avant de coder.

```
https://data-api.binance.vision/api/v3/klines?symbol=BTCUSDT&interval=1h&limit=24
```

Chaque élément est un **tableau** : l'heure d'ouverture en millisecondes, puis les prix d'ouverture, le plus haut, le plus bas et de clôture, sous forme de texte.

📦 Fourni aussi : le composable qui trace la courbe, à créer dans `ui/detail/PriceChart.kt`. Il reçoit la liste des prix, du plus ancien au plus récent.

<details>
<summary>📄 <code>ui/detail/PriceChart.kt</code></summary>

```kotlin
package com.bvic.followmycrypto.ui.detail

import androidx.compose.foundation.Canvas
import androidx.compose.foundation.layout.fillMaxWidth
import androidx.compose.foundation.layout.height
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Path
import androidx.compose.ui.graphics.StrokeCap
import androidx.compose.ui.graphics.StrokeJoin
import androidx.compose.ui.graphics.drawscope.Stroke
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import com.bvic.followmycrypto.theme.FollowMyCryptoTheme
import com.bvic.followmycrypto.theme.PriceDown
import com.bvic.followmycrypto.theme.PriceUp

// Trace la courbe d'une suite de prix, du plus ancien au plus récent
@Composable
fun PriceChart(prices: List<Double>, modifier: Modifier = Modifier) {
    if (prices.size < 2) return

    val color = if (prices.last() >= prices.first()) PriceUp else PriceDown
    val min = prices.min()
    val max = prices.max()
    // Évite une division par zéro si tous les prix sont identiques
    val range = if (max > min) max - min else 1.0

    Canvas(modifier = modifier.fillMaxWidth().height(200.dp)) {
        val stepX = size.width / (prices.size - 1)
        val path = Path()
        prices.forEachIndexed { index, price ->
            val x = index * stepX
            // Le prix le plus haut est en haut : dans un Canvas, y = 0 est le bord supérieur
            val y = size.height - ((price - min) / range).toFloat() * size.height
            if (index == 0) path.moveTo(x, y) else path.lineTo(x, y)
        }
        drawPath(
            path = path,
            color = color,
            style = Stroke(width = 2.dp.toPx(), cap = StrokeCap.Round, join = StrokeJoin.Round),
        )
    }
}

@Preview(showBackground = true)
@Composable
fun PriceChartPreview() {
    FollowMyCryptoTheme {
        PriceChart(prices = listOf(100.0, 104.0, 101.0, 108.0, 106.0, 112.0))
    }
}
```

</details>

📏 Contraintes :

- Une nouvelle fonction dans `BinanceApi`, et une nouvelle fonction dans le contrat du repository, qui renvoie les prix de clôture.
- Le graphique a ses propres états de chargement et d'erreur : s'il échoue, le reste de l'écran de détail s'affiche quand même.
- `FakeCryptoRepository` continue de fonctionner.

💡 Pistes : la réponse n'est pas une liste d'objets, donc pas de `data class` pour le DTO : regardez `JsonArray` dans kotlinx.serialization, et comment lire son cinquième élément. Commencez par afficher la courbe avec une liste de prix écrite à la main, puis branchez les vraies données.

Pour aller plus loin : un choix de période (24 heures, 7 jours, 1 mois), ou votre propre version du dessin avec [`Canvas`](https://developer.android.com/develop/ui/compose/graphics/draw/overview).

---

## 15. Deux panneaux sur grand écran

🎯 Sur un écran large (la fenêtre Desktop agrandie, une tablette), la liste et le détail s'affichent **côte à côte**. Sur un écran étroit, rien ne change.

📏 Contraintes :

- La crypto sélectionnée est mise en évidence dans la liste.
- Redimensionner la fenêtre fait passer d'une mise en page à l'autre sans perdre la crypto sélectionnée.

💡 Pistes : [les mises en page adaptatives](https://developer.android.com/develop/ui/compose/layouts/adaptive) ; `BoxWithConstraints` donne la largeur disponible. Les écrans ne connaissent pas le `NavController` : c'est le moment d'en profiter.

---

## 16. Tester le ViewModel

🎯 Des tests automatiques vérifient le comportement de `CryptoListViewModel` : il démarre en chargement, passe en succès quand le repository répond, et en erreur quand il échoue.

📦 Fourni : la bibliothèque de test des coroutines, à ajouter aux dépendances de `commonTest`. Elle a la même version que les coroutines du projet.

```
org.jetbrains.kotlinx:kotlinx-coroutines-test
```

📏 Contraintes :

- Les tests sont dans `shared/src/commonTest` et passent avec `./gradlew :shared:jvmTest`.
- Aucun appel réseau : les tests utilisent un faux repository.
- Un test ne dure pas 1,5 seconde, malgré le `delay` du faux repository.

💡 Pistes : [tester les coroutines](https://developer.android.com/kotlin/coroutines/test) ; `runTest`, `Dispatchers.setMain` et `advanceUntilIdle` dans [kotlinx-coroutines-test](https://kotlinlang.org/api/kotlinx.coroutines/kotlinx-coroutines-test/). Vous voyez maintenant pourquoi le ViewModel **reçoit** son repository : pour le cas d'erreur, écrivez un faux repository qui échoue.

---

## 17. Votre idée

Une alerte quand un prix dépasse un seuil, un convertisseur, un portefeuille fictif, un changement de thème… Proposez-la **avant** de commencer : on fixe ensemble sa difficulté.

---

[⬅️ Sommaire](README.md) · [L'évaluation ➡️](02-evaluation.md)
