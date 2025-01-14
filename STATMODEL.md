# Utilisation du module `statsmodels` pour les prédictions : Régression Logistique et OLS

Le module `statsmodels` est une bibliothèque Python populaire pour effectuer des analyses statistiques. Dans ce guide, nous allons couvrir deux techniques de régression : la régression logistique (logit) et la régression linéaire ordinaire (OLS).

## 2. Régression Logistique (Logit)
La régression logistique est souvent utilisée pour prédire des variables binaires (0 ou 1). Nous utiliserons l'exemple du dataset Pima Indians Diabetes Dataset.

### 2.1 Exemple de régression logistique avec Logit

```python
import statsmodels.api as sm
import pandas as pd

# Charger les données (remplacer par un fichier local ou une URL)
url = 'https://raw.githubusercontent.com/jbrownlee/Datasets/master/pima-indians-diabetes.data.csv'
columns = ['Pregnancies', 'Glucose', 'BloodPressure', 'SkinThickness', 'Insulin', 'BMI', 'DiabetesPedigreeFunction', 'Age', 'Outcome']
data = pd.read_csv(url, header=None, names=columns)

# Définir les variables explicatives (X) et la variable cible (y)
X = data.drop('Outcome', axis=1)
y = data['Outcome']

# Ajouter une constante à X pour l'ordonnée à l'origine
X = sm.add_constant(X)

# Créer le modèle logit
model = sm.Logit(y, X)

# Ajuster le modèle
result = model.fit()

# Résumé du modèle
print(result.summary())

# Prédictions avec le modèle ajusté
predictions = result.predict(X)
print(predictions.head())
```

### 2.2 Explication du code
1. sm.Logit(y, X): Crée un modèle logistique avec X comme variables explicatives et y comme variable cible.
2. model.fit(): Ajuste le modèle aux données.
3. result.summary(): Affiche un résumé détaillé des résultats du modèle.
4. result.predict(X): Effectue des prédictions sur les données X d'entrée.

## 3. Régression Linéaire Ordinaire (OLS)
La régression linéaire ordinaire (OLS) est utilisée pour prédire une variable continue. Dans cet exemple, nous allons utiliser un dataset fictif.

### 3.1 Exemple de régression OLS avec OLS

```python
import statsmodels.api as sm
import numpy as np
import pandas as pd

# Exemple de données fictives
data = {
    'X1': [1, 2, 3, 4, 5],
    'X2': [2, 3, 4, 5, 6],
    'Y': [5, 7, 9, 11, 13]
}

df = pd.DataFrame(data)

# Définir les variables explicatives (X) et la variable cible (Y)
X = df[['X1', 'X2']]
y = df['Y']

# Ajouter une constante à X pour l'ordonnée à l'origine
X = sm.add_constant(X)

# Créer le modèle OLS
model = sm.OLS(y, X)

# Ajuster le modèle
result = model.fit()

# Résumé du modèle
print(result.summary())

# Prédictions avec le modèle ajusté
predictions = result.predict(X)
print(predictions)
```

### 3.2 Explication du code

1. sm.OLS(y, X): Crée un modèle de régression linéaire ordinaire avec X comme variables explicatives et y comme variable cible.
2. model.fit(): Ajuste le modèle aux données.
3. result.summary(): Affiche un résumé détaillé des résultats du modèle.
4. result.predict(X): Effectue des prédictions avec le modèle ajusté sur les données X.