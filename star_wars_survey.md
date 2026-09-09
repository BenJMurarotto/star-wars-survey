---
jupyter:
  jupytext:
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.19.5
  kernelspec:
    display_name: base
    language: python
    name: python3
---

```python
import pandas as pd
```

```python
csv_path = "StarWars.csv"

```

```python
df = pd.read_csv(csv_path, encoding="cp1252")
df.head()

```

We need to clean the NaNs in the "Seen" category in columns 3-9

```python
movie_integer_counter = 1
new_columns = df.columns.tolist()
for col in range(3, 9):
    new_columns[col] = f"Has seen Star Wars Movie {movie_integer_counter}?"
    df.iloc[:, col] = df.iloc[:, col].notna()
    movie_integer_counter += 1

df.columns = new_columns
df = df.drop(index=0).reset_index(drop=True)

```

```python
movie_integer_counter = 1
new_columns = df.columns.tolist()
for col in range(9, 15):
    new_columns[col] = f"Ranking of Star Wars Movie{movie_integer_counter}?"
    df.iloc[:, col] = df.iloc[:, col].astype("Int64")
    movie_integer_counter += 1

df.columns = new_columns
df = df.drop(index=0).reset_index(drop=True)
```

```python
favourability_ranking = df["Unnamed: 16"].value_counts().index.tolist()
favourability_ranking
```

```python
from pandas.api.types import CategoricalDtype
```

```python
favourability_order = CategoricalDtype()
```
