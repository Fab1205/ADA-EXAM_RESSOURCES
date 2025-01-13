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
print(df)
```

### A partir d’une liste de listes :
```python
data = [
    ['Alice', 25, 'Paris'],
    ['Bob', 30, 'Lyon'],
    ['Charlie', 35, 'Marseille']
]
df = pd.DataFrame(data, columns=['Nom', 'Age', 'Ville'])
print(df)
```

### Lecture d’un fichier CSV :
```python
df = pd.read_csv('fichier.csv')
```

---

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
print(df.shape)  # (lignes, colonnes)
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
print(df['Nom'])  # Sélection d'une colonne
```

### Accès à une ligne (par index) :
```python
print(df.iloc[0])  # Première ligne
```

### Accès à une valeur spécifique :
```python
print(df.at[0, 'Nom'])  # Ligne 0, colonne 'Nom'
```

---

## Manipulation des données

### Filtrer les lignes :
```python
filtre = df['Age'] > 30
print(df[filtre])
```

### Ajouter une colonne :
```python
df['Score'] = [90, 85, 88]
print(df)
```

### Supprimer une colonne :
```python
df = df.drop('Score', axis=1)
print(df)
```

### Supprimer des lignes :
```python
df = df.drop(0)  # Supprime la première ligne
print(df)
```

### Renommer les colonnes :
```python
df = df.rename(columns={'Nom': 'Prénom'})
print(df)
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

### Groupement :
```python
groupe = df.groupby('Ville')['Age'].mean()
print(groupe)
```

### Fusion de DataFrames :
```python
df1 = pd.DataFrame({'ID': [1, 2], 'Nom': ['Alice', 'Bob']})
df2 = pd.DataFrame({'ID': [1, 2], 'Score': [90, 85]})
merge = pd.merge(df1, df2, on='ID')
print(merge)
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