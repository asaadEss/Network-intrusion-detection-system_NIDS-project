# Détection d'Intrusion Botnet par Analyse Comportementale (Algorithme MINDS)

Ce projet implémente un système de détection d'intrusion réseau (NIDS) basé sur l'analyse comportementale (statistique) pour identifier le botnet **Neris** (CTU-13 Dataset). Contrairement aux approches par signature, cet algorithme détecte les anomalies de volume et de fréquence dans les flux NetFlow.

## 📌 Résultats Clés

* **Taux de Détection (Rappel) :** 91% (Le botnet est quasi-systématiquement détecté).
* **Méthode de Seuillage :** Indice de Youden sur courbe ROC.
* **Performance Globale (AUC) :** 0.85.

## 📊 Visualisations

### 1. Performance du Modèle (Courbe ROC)
Nous avons utilisé la statistique de Youden pour déterminer le seuil optimal d'anomalie (14.25), offrant le meilleur compromis Sensibilité/Spécificité.

![Courbe ROC](images/courbe_roc_youden.png)

### 2. Matrice de Confusion
Le modèle montre une excellente capacité à détecter les attaques (Vrais Positifs élevés), mais nécessite un filtrage par liste blanche (Whitelisting) pour réduire les faux positifs causés par les serveurs DNS légitimes.

![Matrice de Confusion](images/matrice_confusion.png)

## 🛠️ Méthodologie Technique

L'algorithme **MINDS** calcule 4 dimensions contextuelles pour chaque flux réseau sur une fenêtre glissante :
1.  **Fan-out :** Nombre de destinations distinctes contactées par une source.
2.  **Fan-in :** Nombre de sources distinctes contactant une destination.
3.  **Complexité Port/IP :** Analyse des ratios de trafic sortant/entrant.

Le score d'anomalie est calculé via une distance statistique (Z-Score multivarié) par rapport au trafic normal appris lors de la phase d'entraînement.

## 📂 Structure du Projet

* `IDS_Detection_Botnet.ipynb` : Le code complet (Nettoyage, Feature Engineering, Entraînement, Test).
* `images/` : Graphiques générés lors de l'analyse.

## DATASET
Le projet utilise le scénario 9 du dataset CTU-13.
Source : [Stratosphere IPS](https://www.stratosphereips.org/datasets-ctu13)
