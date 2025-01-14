# Gestion des DataFrames en Python avec Pandas

## Introduction
Pandas est une bibliothèque Python puissante et flexible, largement utilisée pour l'analyse et la manipulation de données. Les DataFrames sont une structure de données clé de Pandas, conçue pour représenter des données tabulaires similaires aux tables des bases de données ou aux feuilles de calcul Excel.

---

## Importation de Pandas
```python
import pandas as pd
```

---

## Création d'un DataFrame

### A partir d’un dictionnaire :
```python
data = {
    'Nom': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'Ville': ['Paris', 'Lyon', 'Marseille']
}
df = pd.DataFrame(data)
```

### A partir d’une liste de listes :
```python
data = [
    ['Alice', 25, 'Paris'],
    ['Bob', 30, 'Lyon'],
    ['Charlie', 35, 'Marseille']
]
df = pd.DataFrame(data, columns=['Nom', 'Age', 'Ville'])
```

### Lecture d’un fichier CSV :
```python
df = pd.read_csv('fichier.csv')
```

### Lecture d’un fichier JSON :
```python
df = pd.read_json("fichier.json", lines=True)
# OR
df = pd.read_json("fichier.jsonl", lines=True)
```

### Lecture d’un fichier ZIP/CSV :
```python
df = pd.read_csv('fichier.csv.gz', compression='gzip')
```

## Exploration d’un DataFrame

### Aperçu des premières lignes :
```python
print(df.head())
```

### Aperçu des dernières lignes :
```python
print(df.tail())
```

### Dimensions du DataFrame :
```python
print(df.shape)  # (lines, columns)
```

### Informations générales :
```python
print(df.info())
```

### Statistiques descriptives :
```python
print(df.describe())
```

---

## Accès aux données

### Accès aux colonnes :
```python
print(df['Nom'])  # Select a column
```

### Accès à une ligne (par index) :
```python
print(df.iloc[0])  # First line
```

### Accès à une valeur spécifique :
```python
print(df.at[0, 'Nom'])  # Line 0, column 'Nom'
```

### Accès à une columns après un groupby :
```python
# Few examples
df.groupby(["TGT"]).SRC.count().mean()
df.groupby(["YEA"]).TGT.nunique() # Can be used with sum() or count() too
tmp = df.groupby(["YEA", "TGT"]).VOT
tmp_a = tmp.count().reset_index().groupby("YEA").VOT.count()
tmp_b = df.groupby(["YEA"]).VOT.apply(lambda x: np.mean(x > 0))
tmp_c = tmp.count().reset_index().groupby("YEA").VOT.mean()
```

---

## Manipulation des données

### Changer le type d'une colonne (bool to int par exemple) :
```python
full_df["int"] = full_df["bool"].astype(int)
# OR
full_df["int1"] = (full_df["int2"] == 1).values.astype(int) # Here (...) is a bool column
```

### Filtrer les lignes :
```python
filtre = df['Age'] > 30
print(df[filtre])
```

### Ajouter une colonne :
```python
df['Score'] = [90, 85, 88]
# OR
df['fraction'] = df['number1'] / df['number2']
```

### Supprimer une colonne :
```python
df = df.drop('Score', axis=1)
# OR
df.drop(columns=["col1", "col2", "col3"], , inplace=True)
# OR
df = df.drop(columns=["col1", "col2"])
```

### Supprimer des lignes :
```python
df = df.drop(0)  # Supprime la première ligne
```

### Renommer les colonnes :
```python
df = df.rename(columns={'Nom': 'Prénom'})
# OR
df.columns = ['col_name1', 'col_name2', 'col_name3', 'col_name4']
```

---

## Gestion des valeurs manquantes

### Identifier les valeurs manquantes :
```python
print(df.isnull())
print(df.isnull().sum())
```

### Supprimer les valeurs manquantes :
```python
df = df.dropna()
```

### Remplir les valeurs manquantes :
```python
df = df.fillna(0)  # Remplace les NaN par 0
```

---

## Opérations avancées

### Unique value in columns:
```python
num_distinct_value_in_columns = df['columns'].nunique()
```

### Sum of the columns:
```python
sum_of_column_values = df['columns'].sum()
```

### Mean of the columns:
```python
mean_of_column_values = df['columns'].mean()
```

### Groupement :
```python
groupe = df.groupby('Ville')['Age'].mean()
```

### Fusion de DataFrames :
```python
df1 = pd.DataFrame({'ID': [1, 2], 'Nom': ['Alice', 'Bob']})
df2 = pd.DataFrame({'ID': [1, 2], 'Score': [90, 85]})
merge = pd.merge(df1, df2, on='ID')
```

### Reindexation
```python
df = df.reindex([2, 0, 1])  # Réorganise les lignes
```

### Application de fonctions personnalisées
```python
df['Age carré'] = df['Age'].apply(lambda x: x**2)
```

---

## Traitement de dates

### Conversion en type datetime
```python
df['Date'] = pd.to_datetime(df['Date'])
print(df['Date'].dt.year)
```

### Filtrage par date
```python
filtre = (df['Date'] > '2023-01-01') & (df['Date'] <= '2023-12-31')
print(df[filtre])
```

---

## Combinaisons et jointures

### Concaténation
```python
df_concat = pd.concat([df1, df2], axis=0)  # Verticale
```

### Jointures avancées
```python
df_merge = pd.merge(df1, df2, on='ID', how='outer')
```

---

## Tri et classement

### Trier les valeurs
```python
df = df.sort_values(by='Age', ascending=False)
```

### Trier par index
```python
df = df.sort_index()
```

---

## Sauvegarde d’un DataFrame

### Sauvegarde au format CSV :
```python
df.to_csv('resultat.csv', index=False)
```

### Sauvegarde au format Excel :
```python
df.to_excel('resultat.xlsx', index=False)
```

---

## Conclusion
Ce guide fournit une base solide pour gérer les DataFrames avec Pandas. En combinant ces opérations de base avec des opérations plus avancées, vous serez capable d’analyser et de manipuler efficacement vos données en Python.
