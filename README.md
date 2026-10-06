<div align="center">

# 🏠 ELE Monitor

### Intelligence Immobilière · Gironde (33)

**Moniteur open source d'analyse du marché immobilier basé sur les données DVF+ officielles (Cerema)**

[![Démo](https://img.shields.io/badge/🌐_Démo-En_ligne-000091?style=for-the-badge)](https://gunout.github.io/monitor-ele-immo/)
[![Données](https://img.shields.io/badge/📊_Données-324_343_mutations-D4AF37?style=for-the-badge)](#-données)
[![Couverture](https://img.shields.io/badge/📅_Période-2014--2025-1B7F5A?style=for-the-badge)](#-données)
[![Licence](https://img.shields.io/badge/⚖️_Licence-MIT-C41E3A?style=for-the-badge)](LICENSE)

</div>

---

## 📖 À propos

**ELE Monitor** est un tableau de bord web 100% statique qui permet d'explorer et d'analyser **324 343 transactions immobilières** enregistrées en Gironde entre **2014 et 2025**, à partir des données publiques DVF+ du Cerema.

Conçu pour les **particuliers**, les **investisseurs**, les **agents immobiliers** et les **collectivités**, il offre **15 vues d'analyse** sans backend, sans base de données, et sans inscription.

## 🌐 Démonstration

**👉 [Accéder au monitor en ligne](https://gunout.github.io/monitor-ele-immo/)**

## ✨ Fonctionnalités

| Vue | Description |
|---|---|
| 📊 **Vue d'ensemble** | KPIs globaux, répartition par type, dernières transactions |
| 📋 **Mutations** | Tableau filtrable (année, prix/m², surface, type) + tri + export |
| 📈 **Évolution annuelle** | Tendance des prix année par année |
| 📉 **Tendance longue** | Courbe SVG interactive 2014 → 2025 |
| 🏘️ **Types de biens** | Répartition maisons / appartements / locaux |
| 🗺️ **Carte interactive** | Heatmap des prix + points géolocalisés (Leaflet) |
| 🔥 **Top communes** | Classement par prix et volume |
| 📊 **Distribution** | Histogramme des prix par tranches |
| 📅 **Saisonnalité** | Nombre de ventes par mois |
| 🎯 **Comparateur** | Deux communes côte à côte |
| 💰 **Rendement locatif** | Estimation du rendement brut |
| 📈 **Volatilité** | Coefficient de variation par commune |
| 🏆 **Top ventes** | 50 transactions les plus chères |
| 📉 **Anomalies** | Détection des prix hors normes (3σ) |
| 🔬 **Indice de tension** | Ratio ventes / population |

## 📊 Données

| Métrique | Valeur |
|---|---|
| **Transactions** | 324 343 |
| **Période** | Janvier 2014 → Décembre 2025 |
| **Communes** | 534 |
| **Département** | Gironde (33) |
| **Source** | [DVF+ open-data — Cerema](https://cerema.app.box.com/v/dvfplus-opendata) |
| **Licence source** | Licence Ouverte 2.0 |

### Filtrage appliqué

- Département : **33** (Gironde uniquement)
- Prix/m² : entre **200 €** et **30 000 €** (exclusion des outliers)
- Surfaces : supérieures à 0 m²
- Valeurs foncières : supérieures à 0 €

## 🛠️ Architecture technique

Le projet est **100% statique** : un seul fichier HTML contient toute l'application (structure, styles, logique). Aucun serveur, aucune base de données.

**Fichiers principaux :**

| Fichier | Rôle | Taille |
|---|---|---|
| `index.html` | Application complète (HTML + CSS + JavaScript) | ~62 Ko |
| `data/mutations.json.gz` | Base de données compressée (324 343 transactions) | 3.9 Mo |
| `data/communes.json` | Centroïdes des 534 communes de Gironde | 51 Ko |

**Flux de fonctionnement :**

1. Le navigateur télécharge `index.html`
2. Il télécharge ensuite `data/mutations.json.gz` (3.9 Mo)
3. Il le décompresse en mémoire avec **pako** (librairie gzip)
4. Il parse le JSON et effectue les calculs (statistiques, agrégations)
5. Il affiche les résultats dans les 15 vues

**Bibliothèques externes utilisées (via CDN) :**

- **Leaflet 1.9.4** — Cartographie interactive
- **Leaflet.heat 0.2.0** — Heatmap des prix
- **pako 2.1.0** — Décompression gzip côté client

## 🚀 Installation locale

### Prérequis

- Un navigateur moderne (Chrome, Firefox, Safari, Edge)
- Python 3 (pour servir les fichiers en local)

### Étapes

```bash
# 1. Cloner le dépôt
git clone https://github.com/gunout/monitor-ele-immo.git
cd monitor-ele-immo

# 2. Lancer un serveur HTTP local
python3 -m http.server 8080

# 3. Ouvrir dans le navigateur
# → http://localhost:8080

```
## ⚠️ Limites connues

- **Géolocalisation** : les points sont placés au **centroïde de chaque commune** (précision ± 1 km). Pour une précision à l'adresse exacte, il faut la table `local` du Cerema (accès restreint).
- **Adresses** : non incluses dans la table `mutation` utilisée.
- **RGPD** : les données DVF sont anonymisées à la source. Aucune ré-identification des personnes n'est possible ni autorisée.
- **Inflation** : les prix ne sont pas corrigés de l'inflation. Une comparaison directe 2014 / 2025 doit être nuancée.

## 🤝 Contribution

Les contributions sont bienvenues ! Pour proposer une amélioration :

1. Fork le projet
2. Créer une branche (`git checkout -b feature/amelioration`)
3. Commit (`git commit -m 'Ajout nouvelle vue'`)
4. Push (`git push origin feature/amelioration`)
5. Ouvrir une Pull Request

## 📜 Licence

Ce projet est sous licence **MIT** — voir [LICENSE](LICENSE).

Les **données sources** (DVF+) sont sous **Licence Ouverte 2.0** (Etalab).

## 🙏 Remerciements

- [Cerema](https://www.cerema.fr/) — Diffusion des données DVF+
- [Etalab](https://www.etalab.gouv.fr/) — API Géo (centroïdes de communes)
- [OpenStreetMap](https://www.openstreetmap.org/) — Fond de carte
- [Leaflet](https://leafletjs.com/) — Cartographie interactive
- [pako](https://github.com/nodeca/pako) — Décompression gzip

## 📞 Contact

- **GitHub** : [@gunout](https://github.com/gunout)
- **Issues** : [Signaler un bug](https://github.com/gunout/monitor-ele-immo/issues)

---

<div align="center">

**⭐ Si ce projet vous est utile, laissez une étoile sur GitHub ! ⭐**

*ELE Monitor — La donnée immobilière, claire et locale.*

</div>
