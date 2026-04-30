# ESG Search Engine
 
> Moteur de recherche et d'analyse ESG unifié — 31 indicateurs · 26 350 entreprises · 7 modules d'analyse
 
**Projet groupe** — Chanez, Blaine, Irène, Laurel et Robin | Master DEFIS, Sorbonne Paris Nord | Mars 2026
 
---
 
## Contexte & Problématique
 
L'analyse ESG publique souffre d'une fragmentation majeure : les données sont dispersées sur 20+ sources hétérogènes (WBA, SBTi, Urgewald, ChemSec…), dans des formats incompatibles (CSV, PDF, APIs, scraping web), sans vue consolidée ni score comparable entre émetteurs.
 
Notre plateforme web d'** ESG Search** répond à ce problème en construisant une base de données unifiée et une plateforme d'analyse accessible, 100% open data.
 
---
 
## Résultats Clés
 
| Métrique | Valeur |
|---|---|
| Entreprises consolidées | 26 350 |
| Indicateurs ESG intégrés | 31 |
| Scripts de collecte Python | 22 |
| Secteurs GICS couverts | 11 |
| Modules d'analyse web | 7 |
| Déploiement | Vercel (open source) |
 
---
 
## Architecture Technique
 
Le pipeline de données repose sur 4 étapes :
 
1. **Collecte** — 22 scripts Python par source (CSV, Excel, PDF, APIs, scraping)
2. **Référencement** — 1 ligne = 1 entreprise, identifiée par code ISIN unique
3. **Croisement** — Matching des 31 indicateurs sur la base ISIN commune
4. **Consolidation** — 10 000 ISIN résolus manuellement · 26 350 entreprises au total
> **Problème clé résolu** : le nommage non standardisé entre sources (`"TotalEnergies" ≠ "Total SA"`) est traité via l'ISIN comme clé de jointure commune.
 
---
 
## Données : 31 Indicateurs ESG
 
### Environnement (E)
SBTi · TPI · Climate Action 100+ · Urgewald · Forest IQ · Global Canopy · Reclaim Finance · ACT · ChemSec · SPOTT · WBA Nature · WBA Electric Utilities
 
### Social (S)
WBA Social · WBA Gender · WBA CHRB · WBA Digital · WBA Food & Agri · Know The Chain · Global Child Forum · FAIRR · Access to Medicine · BBFAW · Equileap Gender
 
### Gouvernance (G)
UN Global Compact · InfluenceMap LobbyMap · The 266 Accounting · Robeco Institutional · Label ISR · As you Sow
 
Sources : web scraping, APIs publiques, fichiers CSV/Excel — consolidées par ISIN.
 
---
 
## Méthodologie de Scoring ESG
 
Le score ESG composite intègre quatre mécanismes :
 
**Score ajusté par pays**
Diviser par 31 indicateurs pénalise les entreprises pour lesquelles seul un sous-ensemble est géographiquement applicable. La formule corrige ce biais :
 
```
Score = (Indicateurs présents ∩ applicables) / Indicateurs applicables au pays × 100
```
 
**Pondérations E / S / G**
- Environnement : 40%
- Social : 35%
- Gouvernance : 25%
**Fréquence inverse**
Les indicateurs rares pèsent plus lourd, afin de valoriser la profondeur de couverture plutôt que la simple présence sur les datasets les plus larges.
 
**Peer benchmarking sectoriel**
Percentile GICS — positionnement relatif par rapport aux pairs du même secteur.
 
**Niveau de confiance** : Low / Medium / High, calculé à partir du ratio d'applicabilité des indicateurs.
 
---
 
## Les 7 Modules de la Plateforme
 
| Module | Description |
|---|---|
| **Recherche** | Full-text instantané par nom, ISIN ou indicateur (MiniSearch, fuzzy + prefix) |
| **Carte** | Couverture ESG multi-indicateurs par pays (Leaflet.js, choroplèthe dynamique) |
| **Analytics** | Heatmaps sectorielles, co-occurrence, top companies, analyse régionale |
| **Comparer** | Comparaison côte-à-côte sur toutes dimensions E/S/G |
| **Portefeuille** | Score agrégé, ESG Drag Analysis, enrichissement Yahoo Finance, export Excel/PDF |
| **Score ESG** | Score composite ajusté E/S/G avec niveau de confiance |
| **Indicateurs** | Fiches détaillées : méthodologie, limites, pertinence par source |
 
---
 
## Stack Technique
 
- **Collecte** : Python (pandas, requests, BeautifulSoup, pdfplumber)
- **Base de données** : Excel consolidé — 31 indicateurs × 14 colonnes de qualification
- **Frontend** : JavaScript, MiniSearch, Leaflet.js, Chart.js
- **Déploiement** : Vercel
---
 
## Contributeurs
 
| Membre | Rôle principal |
|---|---|
| Irène & Chanez | Recherche entreprises, construction matrice Excel, fiches indicateurs |
| Blaine & Laurel | Vérification scores & données, analyses croisées indicateurs |
| Robin | Architecture web, scraping Python, modules avancés, déploiement |
 
---
 
## Limites & Perspectives
 
**Limites actuelles**
- Couverture moyenne de 7% par entreprise (2,2 indicateurs / entreprise en moyenne)
- Données statiques, sans historisation temporelle des scores
- Matching fuzzy perfectible sur les noms d'entreprises non standardisés
**Évolutions envisagées**
- Ajout de nouveaux indicateurs (CDP, ISS) et historisation des scores
- API REST pour intégration dans des outils tiers
- Modèle ML pour prédiction de trajectoire ESG
- Alignement avec la taxonomie européenne
---
