# Guide pour Créer des Graphiques en Python avec Matplotlib

Ce guide présente les bases de la création de graphiques en Python en utilisant la bibliothèque populaire **Matplotlib**.

---

## 1. Introduction à Matplotlib avec des DataFrames

### 1.1. Création d'un Graphique Simple

Matplotlib est une bibliothèque puissante pour créer des visualisations de base et avancées. Voici un exemple de graphique simple utilisant un DataFrame :

```python
import matplotlib.pyplot as plt
import pandas as pd

# Données sous forme de DataFrame
data = pd.DataFrame({
    'X': [1, 2, 3, 4, 5],
    'Y': [10, 20, 25, 30, 35]
})

# Création du graphique
plt.plot(data['X'], data['Y'], label='Ligne 1', color='blue', marker='o')

# Ajout de titres et de légende
plt.title('Exemple de Graphique Simple')
plt.xlabel('Axe X')
plt.ylabel('Axe Y')
plt.legend()

# Affichage
plt.show()
```

### 1.2. Ajout de Styles

Matplotlib permet d'appliquer des styles prédéfinis pour améliorer l’esthétique du graphique :

```python
plt.style.use('ggplot')  # Exemple de style
plt.plot(data['X'], data['Y'], label='Ligne stylisée', color='green')
plt.legend()
plt.show()
```

---

## 2. Différents Types de Graphiques

### 2.1. Histogramme

Les histogrammes sont utiles pour visualiser la distribution d'une variable :

```python
# Exemple de données
data = pd.DataFrame({
    'Valeurs': [1, 1, 2, 3, 3, 3, 4, 5, 6]
})

# Création de l'histogramme
plt.hist(data['Valeurs'], bins=5, color='purple')
plt.title('Histogramme')
plt.xlabel('Valeurs')
plt.ylabel('Fréquence')
plt.show()
```

### 2.2. Diagramme en Barres

Le diagramme en barres est utile pour comparer des catégories :

```python
# Exemple de données
data = pd.DataFrame({
    'Catégorie': ['A', 'B', 'C', 'D'],
    'Valeurs': [5, 7, 3, 8]
})

# Création du diagramme en barres
plt.bar(data['Catégorie'], data['Valeurs'], color='orange')
plt.title('Diagramme en Barres')
plt.xlabel('Catégories')
plt.ylabel('Valeurs')
plt.show()
```

### 2.3. Nuage de Points

Un nuage de points montre la relation entre deux variables :

```python
# Exemple de données
data = pd.DataFrame({
    'X': [1, 2, 3, 4, 5],
    'Y': [10, 15, 20, 25, 30]
})

# Création du nuage de points
plt.scatter(data['X'], data['Y'], color='red')
plt.title('Nuage de Points')
plt.xlabel('X')
plt.ylabel('Y')
plt.show()
```

### 2.4. Boxplot

Un boxplot est utile pour visualiser la distribution et les outliers :

```python
# Exemple de données
data = pd.DataFrame({
    'Catégorie': ['A', 'A', 'B', 'B', 'C', 'C'],
    'Valeurs': [10, 15, 20, 25, 30, 35]
})

# Création du boxplot
plt.boxplot([data[data['Catégorie'] == 'A']['Valeurs'],
             data[data['Catégorie'] == 'B']['Valeurs'],
             data[data['Catégorie'] == 'C']['Valeurs']],
            labels=['A', 'B', 'C'])
plt.title('Boxplot')
plt.ylabel('Valeurs')
plt.show()
```

### 2.5. Graphique en Secteurs

Un graphique en secteurs (camembert) est idéal pour représenter des proportions :

```python
# Exemple de données
data = pd.DataFrame({
    'Catégorie': ['A', 'B', 'C', 'D'],
    'Valeurs': [15, 30, 45, 10]
})

# Création du graphique en secteurs
plt.pie(data['Valeurs'], labels=data['Catégorie'], autopct='%1.1f%%', startangle=90, colors=['blue', 'green', 'red', 'orange'])
plt.title('Graphique en Secteurs')
plt.show()
```

### 2.6. Graphique en Aire

Les graphiques en aires sont utiles pour montrer l'évolution d'une variable :

```python
# Exemple de données
data = pd.DataFrame({
    'X': [1, 2, 3, 4, 5],
    'Y': [10, 20, 30, 40, 50]
})

# Création du graphique en aire
plt.fill_between(data['X'], data['Y'], color='skyblue', alpha=0.4)
plt.plot(data['X'], data['Y'], color='Slateblue', alpha=0.7)
plt.title('Graphique en Aire')
plt.xlabel('X')
plt.ylabel('Y')
plt.show()
```

---

## 3. Fonctionnalités Avancées

### 3.1. Changer la Taille du Graphique

Vous pouvez modifier la taille de votre graphique en utilisant l'argument `figsize` lors de la création de la figure :

```python
# Exemple de données
data = pd.DataFrame({
    'X': [1, 2, 3, 4, 5],
    'Y': [10, 20, 25, 30, 35]
})

# Changer la taille du graphique
plt.figure(figsize=(10, 6))  # Largeur = 10, Hauteur = 6
plt.plot(data['X'], data['Y'], label='Ligne 1', color='blue', marker='o')
plt.title('Graphique avec Taille Personnalisée')
plt.xlabel('Axe X')
plt.ylabel('Axe Y')
plt.legend()
plt.show()
```

### 3.2. Créer des Subplots (Graphiques Multiples)

Les subplots permettent d'afficher plusieurs graphiques dans une même figure :

```python
# Exemple de données
data = pd.DataFrame({
    'X': [1, 2, 3, 4, 5],
    'Y1': [10, 20, 25, 30, 35],
    'Y2': [15, 25, 30, 35, 40]
})

# Création de subplots
fig, axes = plt.subplots(1, 2, figsize=(12, 5))  # 1 ligne, 2 colonnes

# Premier subplot
axes[0].plot(data['X'], data['Y1'], color='blue', marker='o')
axes[0].set_title('Graphique 1')
axes[0].set_xlabel('X')
axes[0].set_ylabel('Y1')

# Deuxième subplot
axes[1].plot(data['X'], data['Y2'], color='green', linestyle='--')
axes[1].set_title('Graphique 2')
axes[1].set_xlabel('X')
axes[1].set_ylabel('Y2')

# Ajustement des espaces entre les subplots
plt.tight_layout()
plt.show()
```