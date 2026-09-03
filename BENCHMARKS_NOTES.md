# pyg-team/pytorch_geometric — Notes de benchmark

**Statut : OK — GCNConv testé**

Un point central : **`mlx.core.compile` en mode lazy / compilé** attend de connaître toute la séquence d'opérations avant de lancer les calculs. C'est particulièrement important pour les **opérations de batching** : au lieu d'exécuter chaque petite opération GPU séparément (avec son overhead de dispatch/lancement à chaque itération), le mode compilé lazy construit d'abord le graphe d'opérations de tout le batch, le fusionne en kernels optimisés, puis l'exécute d'un seul coup. Pour un batch de N échantillons, l'overhead est amorti une seule fois au lieu de N fois — d'où des gains typiques de plusieurs fois (jusqu'à ~15×) dès que le travail par étape est suffisant.

## Gaps de compatibilité
pytorch_geometric / GCNConv. 12 gaps (round 356).

## Références
- Dépôt source torch-mlx : https://github.com/bahaehmimdi/torch-mlx
- Discussion générale : https://github.com/bahaehmimdi/torch-mlx-benchmarks-output/discussions/1
