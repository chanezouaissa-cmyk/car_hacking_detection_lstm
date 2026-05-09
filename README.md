#  Car Hacking Detection avec LSTM

##  Description
Détection d'attaques sur le bus CAN de véhicules connectés
en utilisant un réseau de neurones LSTM (Long Short-Term Memory).
Le modèle effectue une **classification multiclasse** pour identifier
le type d'attaque parmi 5 classes.

Projet réalisé dans le cadre du Master 1 IA - Université A. Mira de Béjaïa.


---

##  Objectif
dentifiant le type d'attaque à partir du Car-Hacking Dataset.
| Label | Classe        |
|-------|---------------|
| 0     | Normal        |
| 1     | DoS           |
| 2     | Fuzzy         |
| 3     | RPM Spoofing  |
| 4     | Gear Spoofing |

---

##  Dataset
**Car-Hacking Dataset** - disponible sur Kaggle

| Fichier               | Type         | Lignes       |
|-----------------------|--------------|--------------|
| `normal_run_data.csv` | Normal       | ~988 k       |
| `DoS_dataset.csv`     | DoS          | ~3.6 M       |
| `Fuzzy_dataset.csv`   | Fuzzy        | ~3.8 M       |
| `RPM_dataset.csv`     | Gear Spoofing | ~4.6 M      |
| `gear_dataset.csv`    | RPM Spoofing| ~4.4 M        |

**Colonnes** : `Timestamp`, `CAN_ID`, `DLC`, `D0`–`D7`, `Flag`

---

##  Pipeline de traitement

### Exploration (Partie 1)
- Vérification des valeurs manquantes
- Distribution des classes par dataset
- Distribution des CAN ID

### Pré-traitement (Partie 2)

| Étape | Description |
|-------|-------------|
| 1 | Conversion Hexadécimal : Décimal (`CAN_ID`, `D0`–`D7`) |
| 2 | Encodage des labels en classes numériques (0 à 4) |
| 3 | Calcul du `Delta_T` + suppression du Timestamp brut |
| 4 | Traitement des valeurs manquantes |
| 5 | Équilibrage - Under-sampling de la classe majoritaire |
| 6 | Split Train / Test (80% / 20%) |
| 7 | Normalisation - MinMaxScaler [0, 1] |

**Encodage des labels :**
Normal          : 0
Attaque DoS     : 1
Attaque Fuzzy   : 2
Attaque Gear    : 3
Attaque RPM     : 4

---

## Stratégie de split

Tous les datasets ont été fusionnés (Normal + DoS + Fuzzy + RPM + Gear),
puis divisés en **80% Train / 20% Test** de façon aléatoire.

| Ensemble  | Proportion | Contenu                        |
|-----------|------------|--------------------------------|
| **TRAIN** | 80%        | Mélange de tous les datasets   |
| **TEST**  | 20%        | Mélange de tous les datasets   |



---

##  Modèle LSTM

Le LSTM est adapté aux données de séquences temporelles comme
les trames CAN, car il peut capturer les **dépendances temporelles**
entre messages consécutifs.




##  Auteurs

- **Chanez Ouaissa** 
- **Ait Saidi Mazigh** 

---

## 📚 Références

- Car-Hacking Dataset - OTIDS, Kaggle
- *"OTIDS: A Novel Intrusion Detection System for In-vehicle Network
  by using Remote Frame"* - Lee et al., 2017
