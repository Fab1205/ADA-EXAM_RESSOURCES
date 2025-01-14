# Guide pour Travailler avec NetworkX en python

Ce guide vous apprendra à utiliser **NetworkX**, une bibliothèque Python puissante pour l'analyse et la visualisation de graphes. Nous allons également explorer **BiGraphMulti**, une structure de graphe biparti et multi-arêtes.

---

## 1. Introduction à NetworkX

### 1.1. Création d'un Graphe Simple

NetworkX permet de créer différents types de graphes, comme les graphes non orientés, orientés, pondérés, etc. Voici un exemple simple :

```python
import networkx as nx
import matplotlib.pyplot as plt

# Création d'un graphe
G = nx.Graph()

# Ajout de nœuds (un ou plusieurs)
G.add_node(1)
G.add_nodes_from([2, 3, 4])

# Ajout d'arêtes (un ou plusieurs)
G.add_edge(1, 2)
G.add_edges_from([(2, 3), (3, 4), (4, 1)])

# Visualisation du graphe
nx.draw(G, with_labels=True, node_color='lightblue', node_size=500, font_size=10)
plt.title("Graphe Simple")
plt.show()
```

### 1.2. Propriétés du Graphe

NetworkX offre des outils pour accéder aux propriétés du graphe :

```python
# Liste des nœuds et arêtes
print("Nœuds :", G.nodes())
print("Arêtes :", G.edges())

# Nombre de nœuds et arêtes
print("Nœuds :", len(G.nodes()))
print("Arêtes :", len(G.edges()))

# Degré d'un nœud
print("Degré du nœud 1 :", G.degree[1])

# Degré de tout les nœud
degree = list(dict(G.degree()).values())

# Degré de tout les nœud (entrant et sortant) (si graph directionnel !)
out_degree = list(dict(G.out_degree()).values())
in_degree = list(dict(G.in_degree()).values())
```

### 1.3. Graph à partir de DataFrames

```python
G = nx.from_pandas_edgelist(edge_df, source='node1', target='node2', edge_attr='attr', create_using=nx.DiGraph())
```

```python
G = nx.DiGraph()

for _, row in node_df.iterrows():
    G.add_node(row['node1'], score=row['attr1'], name=row['attr2'])

for _, row in edge_df.iterrows():
    G.add_edge(row['node1'], row['node2'], gender=row['attr'])
```

### 1.4. Iterate sur toutes les nodes du graph
```python
for node in G.nodes:
    continue
```
---

## 2. Différents Types de Graphes avec NetworkX

### 2.1. Graphe Orienté

Un graphe orienté a des arêtes directionnelles :

```python
# Création d'un graphe orienté
DG = nx.DiGraph()
DG.add_edges_from([(1, 2), (2, 3), (3, 1)])

# Visualisation
nx.draw(DG, with_labels=True, node_color='lightgreen', node_size=500, font_size=10, arrowsize=20)
plt.title("Graphe Orienté")
plt.show()
```

### 2.2. Graphe Pondéré

Un graphe pondéré associe des poids aux arêtes :

```python
# Création d'un graphe pondéré
WG = nx.Graph()
WG.add_edge(1, 2, weight=4)
WG.add_edge(2, 3, weight=7)

# Visualisation avec poids
pos = nx.spring_layout(WG)
nx.draw(WG, pos, with_labels=True, node_color='lightcoral', node_size=500, font_size=10)
labels = nx.get_edge_attributes(WG, 'weight')
nx.draw_networkx_edge_labels(WG, pos, edge_labels=labels)
plt.title("Graphe Pondéré")
plt.show()
```

---

## 3. Introduction aux Graphes Bipartis avec BiGraphMulti

### 3.1. Création d'un Graphe Biparti

Un graphe biparti est un graphe dont les nœuds peuvent être divisés en deux ensembles distincts, tels qu'aucune arête ne relie deux nœuds du même ensemble. Voici un exemple :

```python
from networkx.algorithms import bipartite

# Création d'un graphe biparti
B = nx.Graph()

# Ajout des nœuds des deux ensembles
B.add_nodes_from([1, 2, 3], bipartite=0)  # Ensemble 1
B.add_nodes_from(['A', 'B'], bipartite=1)  # Ensemble 2

# Ajout des arêtes
B.add_edges_from([(1, 'A'), (2, 'A'), (3, 'B')])

# Visualisation
pos = nx.bipartite_layout(B, nodes=[1, 2, 3])
nx.draw(B, pos, with_labels=True, node_color=['lightblue', 'lightgreen'], node_size=500, font_size=10)
plt.title("Graphe Biparti")
plt.show()
```

### 3.2. Vérification de la Bipartition

Vous pouvez vérifier si un graphe est biparti :

```python
is_bipartite = bipartite.is_bipartite(B)
print("Le graphe est biparti :", is_bipartite)
```

---

## 4. Graphes Multiples avec MultiGraph et MultiDiGraph

### 4.1. Création d'un MultiGraph

Un **MultiGraph** permet d'avoir plusieurs arêtes entre deux nœuds :

```python
# Création d'un MultiGraph
MG = nx.MultiGraph()
MG.add_edge(1, 2)
MG.add_edge(1, 2, weight=3)
MG.add_edge(2, 3)

# Visualisation
pos = nx.spring_layout(MG)
nx.draw(MG, pos, with_labels=True, node_color='orange', node_size=500, font_size=10)
plt.title("MultiGraph")
plt.show()
```

### 4.2. Accès aux Arêtes Multiples

Vous pouvez accéder aux arêtes multiples et leurs attributs :

```python
# Accéder aux arêtes multiples entre deux nœuds
edges = MG[1][2]
print("Arêtes entre 1 et 2 :", edges)
```

### 4.3. MultiDiGraph

Un **MultiDiGraph** est un MultiGraph orienté :

```python
# Création d'un MultiDiGraph
MDG = nx.MultiDiGraph()
MDG.add_edge(1, 2)
MDG.add_edge(1, 2, weight=5)
MDG.add_edge(2, 1)

# Visualisation
pos = nx.spring_layout(MDG)
nx.draw(MDG, pos, with_labels=True, node_color='pink', node_size=500, font_size=10, arrowsize=20)
plt.title("MultiDiGraph")
plt.show()
```

## 5. Autres opérations utiles

### 5.1. Trier les edges par attributes et obtenir un subgraph avec ce tri :

```python
edges_2004 = [i for i, v in nx.get_edge_attributes(G, "YEA").items() if v == 2004]
G_2004 = G.edge_subgraph(edges_2004)
```

### 5.2. Get l'attributes d'une node ou d'un edge :
```python
color = nx.get_node_attributes(G, "color")
>>> color[4]
color=nx.get_edge_attributes(G,'color')
>>> color[(1,2)]
```

### 5.3. Get les attributes de tout les edges d'un graph ou subgraph.
```python
edge_attr = nx.get_edge_attributes(G.subgraph(node_list), "attribute")
```

### 5.4. Set un attribute à un edge :
```python
nx.set_edge_attributes(G, dict(df.set_index(["node1", "node2"]).COL_NAME), "ATTR_NAME")
# dict(df.set_index(["node1", "node2"]).COL_NAME) could differ but need to be of the form :
# {(node1, node2): attr12, (node3, node4): attr34 , ...}
```
### 5.5. Check si un edge existe :
```python
G.has_edge(0, 1)  # using two nodes
>>> True
```
