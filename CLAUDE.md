# Tranco Lists

This project maintains subsets of the [Tranco top-1M domain ranking](https://tranco-list.eu/) for use in security research, DNS analysis, and related tooling.

## Project Structure

```
data/
  index.md               # Index of available subset files
  tranco_top_200.txt     # Top 200 domains
  tranco_top_500.txt     # Top 500 domains
  tranco_top_1K.txt      # Top 1,000 domains
  tranco_top_5K.txt      # Top 5,000 domains
  tranco_top_10K.txt     # Top 10,000 domains
  tranco_top_20K.txt     # Top 20,000 domains
  tranco_top_50K.txt     # Top 50,000 domains
```

The raw source files (`top-1m.csv`, `top-1m.csv.zip`) are excluded from git — re-download from `https://tranco-list.eu/top-1m.csv.zip`.

## Refreshing the Data

```bash
curl -L -o data/top-1m.csv.zip https://tranco-list.eu/top-1m.csv.zip
unzip data/top-1m.csv.zip -d data/
```

Then regenerate subsets:

```bash
for N in 200 500 1000 5000 10000 20000 50000; do
  label=$([ $N -ge 1000 ] && echo "${N%000}K" || echo "$N")
  awk -F',' "NR<=$N {print \$2}" data/top-1m.csv > "data/tranco_top_${label}.txt"
done
```
