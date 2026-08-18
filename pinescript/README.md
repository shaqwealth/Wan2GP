# Indicateur/Stratégie PineScript — Achat Horaire Personnalisé

Script PineScript v5 pour TradingView : `buy-from-hour-strategy.pine`

Achète automatiquement à partir d'une heure personnalisée (7h par défaut), à l'intérieur
d'une plage horaire configurable, avec Stop Loss et Take Profit personnalisés.

> Techniquement il s'agit d'une **strategy** PineScript (et non d'un simple `indicator`),
> car c'est le seul type de script capable de passer des ordres d'achat et de gérer un
> stop/take profit automatiquement via `strategy.entry` / `strategy.exit`. Il s'affiche
> sur le graphique comme un indicateur et peut être testé dans le Strategy Tester de
> TradingView ou converti en alertes pour un bot de trading externe.

## Installation

1. Ouvrir TradingView → **Pine Editor**.
2. Créer un nouveau script, coller le contenu de `buy-from-hour-strategy.pine`.
3. Cliquer sur **Ajouter au graphique**.
4. Ouvrir les paramètres du script (icône ⚙️) pour personnaliser les options ci-dessous.

## Options personnalisables

### Session de trading
- **Heure / minute de début** : heure à partir de laquelle les achats sont autorisés (7h00 par défaut).
- **Heure / minute de fin** : heure limite pour les achats (gère aussi les sessions qui passent minuit).
- **Fuseau horaire** : fuseau utilisé pour calculer l'heure de la session (New York, Paris, UTC, etc.).
- **Clôturer en dehors de la session** : ferme automatiquement la position si le prix sort de la fenêtre horaire.
- **Jours de trading autorisés** : cases à cocher par jour de la semaine.

### Logique d'entrée
- **Ouverture de session** : un seul achat déclenché au tout début de la fenêtre horaire chaque jour.
- **Chaque bougie dans la session** : achète dès qu'aucune position n'est ouverte pendant la fenêtre.
- **Filtre de tendance optionnel** : n'achète que si le prix est au-dessus d'une moyenne mobile configurable.

### Stop Loss / Take Profit
- Activables indépendamment (`useSL` / `useTP`).
- Trois modes disponibles pour chacun : **Pourcentage**, **Points**, ou **multiple d'ATR**.
- **Stop suiveur (trailing stop)** optionnel, en pourcentage du prix d'entrée.

## Alertes

Deux `alertcondition` sont fournies :
- **Début de session** : se déclenche au début de la fenêtre horaire.
- **Signal d'achat** : se déclenche à chaque entrée en position.

Elles peuvent être utilisées pour créer des alertes TradingView (webhook, notification, etc.)
sans devoir utiliser le Strategy Tester.

## Avertissement

Ce script est fourni à titre éducatif. Il ne constitue pas un conseil en investissement.
Toujours backtester et valider en papier-trading avant tout usage en argent réel.
