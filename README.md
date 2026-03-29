# tranco

Subsets of the [Tranco top-1M domain ranking](https://tranco-list.eu/) as plain domain lists.

## Files

| Path | Description |
|------|-------------|
| [data/full/top-1m.csv](data/full/top-1m.csv) | Full Tranco top-1M list (`rank,domain`), ~22 MB |
| [data/index.md](data/index.md) | Subsets (top 200 → 50K) with raw download links |

## Refreshing

```bash
curl -L -o data/top-1m.csv.zip https://tranco-list.eu/top-1m.csv.zip
unzip data/top-1m.csv.zip -d data/full/

for N in 200 500 1000 5000 10000 20000 50000; do
  label=$([ $N -ge 1000 ] && echo "${N%000}K" || echo "$N")
  awk -F',' "NR<=$N {print \$2}" data/full/top-1m.csv > "data/tranco_top_${label}.txt"
done
```
