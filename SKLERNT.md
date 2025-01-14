# Guide : Utiliser `sklearn` pour faire des prédictions en Python

Scikit-learn (`sklearn`) est une bibliothèque Python puissante pour le machine learning. Ce guide vous montre comment l'utiliser pour effectuer des prédictions.

## Installation

Avant de commencer, assurez-vous que `sklearn` est installé :

```bash
pip install scikit-learn
```

---

## Étape 1 : Importer les bibliothèques nécessaires

Voici les imports essentiels :

```python
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.linear_model import SGDClassifier
from sklearn.svm import SVC
from sklearn.metrics import accuracy_score
from sklearn.feature_extraction.text import TfidfVectorizer
```

---


## Étape 2 : Diviser les données en ensembles d'entraînement et de test

Divisez vos données pour évaluer le modèle :

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

---

## Étape 3 : Choisir un modèle et l'entraîner

Scikit-learn propose une variété de modèles. Certain parameter peuvent doivoir être ajoutés. Voici quelques exemples :

### Exemple avec un Random Forest Classifier :

```python
# Initialiser le modèle Random Forest
model = RandomForestClassifier(random_state=42)

# Entraîner le modèle
model.fit(X_train, y_train)
```

### Exemple avec un SGDClassifier :

```python
# Initialiser le modèle SGDClassifier
model = SGDClassifier(random_state=42)

# Entraîner le modèle
model.fit(X_train, y_train)
```

### Exemple avec un SVM (Support Vector Machine) :

```python
# Initialiser le modèle SVM
model = SVC(random_state=42)

# Entraîner le modèle
model.fit(X_train, y_train)
```

---

## Étape 4 : Faire des prédictions

Utilisez le modèle entraîné pour prédire les étiquettes de l'ensemble de test :

```python
# Prédire
predictions = model.predict(X_test)

# Afficher les prédictions
print("Prédictions :", predictions)
```

---

## Étape 5 : Évaluer les performances du modèle

Utilisez des métriques comme la précision pour évaluer votre modèle :

```python
# Calculer la précision
accuracy = accuracy_score(y_test, predictions)
print(f"Précision du modèle : {accuracy * 100:.2f}%")
```

---

## Utilisation d'un `TfidfVectorizer` (pour les données textuelles)

Le `TfidfVectorizer` est souvent utilisé pour transformer des données textuelles en une matrice de caractéristiques numériques. Voici un aperçu :

### Pourquoi utiliser un `TfidfVectorizer` ?
1. **Vectorisation** : Transforme les textes en vecteurs numériques exploitables par les modèles de machine learning.
2. **Pondération TF-IDF** : Met en avant les mots importants tout en réduisant l'importance des mots fréquents mais peu significatifs (ex. "le", "et", "de").

### Exemple avec un jeu de données textuel :

```python
from sklearn.feature_extraction.text import TfidfVectorizer

# Données textuelles (exemple)
documents = ["Ceci est un texte d'exemple.", "Un autre document d'exemple.", "Le machine learning est fascinant !"]

# Initialiser le vectorizer
vectorizer = TfidfVectorizer()

# Transformer les documents en vecteurs
X = vectorizer.fit_transform(documents)

print("Matrice TF-IDF :\n", X.toarray())
```

Ensuite, vous pouvez utiliser ces vecteurs (`X`) comme entrée pour vos modèles de machine learning.

---

## Exemple complet

Voici un exemple complet avec un modèle Random Forest :

```python
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score


# Diviser les données
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Initialiser et entraîner le modèle
model = RandomForestClassifier(random_state=42)
model.fit(X_train, y_train)

# Faire des prédictions
predictions = model.predict(X_test)

# Évaluer les performances
accuracy = accuracy_score(y_test, predictions)
print(f"Précision du modèle : {accuracy * 100:.2f}%")
```

---

## Aller plus loin

1. **Autres algorithmes :** Essayez des modèles comme `KNeighborsClassifier`, `GradientBoostingClassifier`, etc.
2. **Optimisation :** Utilisez `GridSearchCV` ou `RandomizedSearchCV` pour trouver les meilleurs hyperparamètres.

Pour plus d'informations, consultez la [documentation officielle de scikit-learn](https://scikit-learn.org/).
