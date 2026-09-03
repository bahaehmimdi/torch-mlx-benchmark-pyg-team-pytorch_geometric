
> ## ⚠️ Correction
>
> Ce dépôt contient des **gains « compilés » ~10×–15× qui ne sont pas reproductibles** et ont été retirés. Sur une baseline MPS propre et avec `mlx.compile` réellement foré à s'exécuter (entrées fraîches + `mx.eval`), **torch-mlx est en parité avec PyTorch MPS** et `mlx.compile` est une **régression** sur la couche torch-mlx. Voir `bench/README.md` du dépôt torch-mlx et `scripts/bench_status.tsv`.

# pyg-team/pytorch_geometric — Notes de benchmark

**Statut : OK — GCNConv testé**

**`mlx.core.compile`** (mode lazy / compilé) ne fusionne les opérations qu'au niveau du graphe MLX natif. Sur la couche d'adaptation torch-mlx, rappelé via `Function.apply`, le compilateur voit des fonctions opaques : la compilation est mesurée comme une **régression** (~1,5× à ~150× plus lente que l'eager MLX), pas une accélération. Les « gains compilés » parfois publiés provenaient de la constante-folding (entrées identiques à chaque itération, graphe lazy jamais forcé).

## Gaps de compatibilité
pytorch_geometric / GCNConv. 12 gaps (round 356).

## Références
- Dépôt source torch-mlx : https://github.com/bahaehmimdi/torch-mlx
- Discussion générale : https://github.com/bahaehmimdi/torch-mlx-benchmarks-output/discussions/1
