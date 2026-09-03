
> ## ⚠️ Correction
>
> Ce dépôt contient des **gains « compilés » ~10×–15× qui ne sont pas reproductibles** et ont été retirés. Sur une baseline MPS propre et avec `mlx.compile` réellement foré à s'exécuter (entrées fraîches + `mx.eval`), **torch-mlx est en parité avec PyTorch MPS** et `mlx.compile` est une **régression** sur la couche torch-mlx. Voir `bench/README.md` du dépôt torch-mlx et `scripts/bench_status.tsv`.

# pyg-team/pytorch_geometric — Benchmark torch-mlx sur Mac

Résultats de test de **torch-mlx** (API PyTorch basée sur le moteur **MLX**
d'Apple Silicon) appliqués à **pyg-team/pytorch_geometric**.

**Statut : OK — GCNConv testé**

**torch-mlx** est une reimplementation de l'API PyTorch basée sur le moteur **MLX d'Apple Silicon**. Sur les modèles non modifiés mesurés (voir `bench/` + `scripts/bench_status.tsv` du dépôt torch-mlx), torch-mlx est en **parité** avec PyTorch MPS (rapport MLX/MPS ~0,1×–0,96×). Les gains « compilés » ~10×–15× précédemment publiés ne sont **pas reproductibles** et ont été corrigés.

**`mlx.core.compile`** (mode lazy / compilé) ne fusionne les opérations qu'au niveau du graphe MLX natif. Sur la couche d'adaptation torch-mlx, rappelé via `Function.apply`, le compilateur voit des fonctions opaques : la compilation est mesurée comme une **régression** (~1,5× à ~150× plus lente que l'eager MLX), pas une accélération. Les « gains compilés » parfois publiés provenaient de la constante-folding (entrées identiques à chaque itération, graphe lazy jamais forcé).

## Compatibilité trouvée
pytorch_geometric / GCNConv. 12 gaps (round 356).

## Discussion
Une discussion dédiée sur les résultats d'optimisation est ouverte dans ce dépôt.
