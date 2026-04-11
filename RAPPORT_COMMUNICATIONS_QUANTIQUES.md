# Rapport: Communications Quantiques et Cybersécurité

## Table des matières
1. [Introduction](#introduction)
2. [Fondamentaux Théoriques](#fondamentaux-théoriques)
3. [Aspects de Recherche](#aspects-de-recherche)
4. [Architecture Réseau Quantique](#architecture-réseau-quantique)
5. [Cybersécurité Quantique](#cybersécurité-quantique)
6. [Implémentations Actuelles](#implémentations-actuelles)
7. [Défis et Perspectives](#défis-et-perspectives)
8. [Références](#références)

---

## 1. Introduction

Les communications quantiques représentent une révolution dans le domaine de la sécurité informatique et des télécommunications. Elles exploitent les principes de la mécanique quantique pour offrir des garanties de sécurité théoriquement inviolables.

**Contexte:**
- Obsolescence prévue de la cryptographie RSA/ECC face aux ordinateurs quantiques
- Besoin urgent de solutions cryptographiques résistantes aux menaces quantiques
- Développement de protocoles de distribution de clés quantiques (QKD)
- Standardisation en cours par le NIST pour l'algorithme post-quantique

---

## 2. Fondamentaux Théoriques

### 2.1 Principes Quantiques Essentiels

#### Superposition quantique
- Un qubit peut exister dans une superposition d'états |0⟩ et |1⟩
- Représentation: |ψ⟩ = α|0⟩ + β|1⟩ où |α|² + |β|² = 1
- L'observation force le qubit à un état défini

#### Intrication quantique (Quantum Entanglement)
- Deux qubits intriqués partagent un état quantique indépendant
- État de Bell: |Φ⁺⟩ = (|00⟩ + |11⟩)/√2
- Corrélation instantanée entre mesures distantes (pas de communication supraluminale)

#### Principe d'incertitude et No-Cloning
- Théorème du non-clonage: Impossible de copier un état quantique inconnu
- Mesurer un qubit détruit l'information
- Fondement de la détection d'écoute en QKD

### 2.2 Mécanique Quantique appliquée à la Cryptographie

**Bases de Recknagel et Shor:**
- Codage qubit-photon: polarisation, phase, direction
- Deux bases non-orthogonales: rectilinéaire (+/×) et diagonale (/)
- Incompatibilité mesure: mesurer dans la mauvaise base donne résultat aléatoire

---

## 3. Aspects de Recherche

### 3.1 Domaines de Recherche Actifs

#### Quantum Key Distribution (QKD)
- **BB84 (Bennett-Brassard 1984):** Premier protocole QKD pratique
  - Utilise quatre états quantiques (2 bases × 2 bits)
  - Sécurité prouvée inconditionnelle
  - Limitations: Besoin de canal classique authentifié

- **E91 (Ekert 1991):** Basé sur intrication
  - Utilise les états de Bell
  - Détection d'écoute via violation des inégalités CHSH
  - Plus robuste théoriquement mais complex à implémenter

- **Protocoles modernes:**
  - **Decoy-state QKD:** Améliore les implémentations faibles
  - **Twin-field QKD (TF-QKD):** Augmente la portée (jusqu'à 500 km)
  - **Measurement-device-independent QKD (MDI-QKD):** Élimine les failles d'implémentation

#### Quantum Internet Alliance (QIA)
- Développement de l'Internet quantique multi-nœuds
- Distribution de clés sur longues distances
- Mémoires quantiques et répéteurs quantiques

#### Standardisation
- ETSI (European Telecommunications Standards Institute)
  - Norme GS QKD pour l'implémentation sécurisée
  - Recommandations d'architecture

- NIST: Post-Quantum Cryptography Standardization
  - CRYSTALS-Kyber (chiffrement)
  - CRYSTALS-Dilithium (signature)
  - Déploiement parallèle QKD + PQC recommandé

### 3.2 État de l'Art

**Exploits réalisés:**
- Distance record: 512 km de fibre optique (2022, China-Europe)
- Débit record: 4 Mbps en laboratoire (TF-QKD)
- Maillage QKD urbain: Plusieurs villes (Genève, China, USA)

**Publications clés:**
- Brunner et al. (2014): "Bell nonlocality"
- Scarani et al. (2009): "The security of practical QKD"
- Arnon-Friedman et al. (2018): "Simple and tight device-independent security"

---

## 4. Architecture Réseau Quantique

### 4.1 Topologies de Réseau

#### Point-à-Point (P2P)
```
[Alice] --QKD channel-- [Bob]
         --Auth channel--
```
- Simple, premières implémentations
- Limitation: Pas de scalabilité
- Cas d'usage: Liens bancaires sécurisés

#### Réseau en Étoile (Star)
```
     [QKD Node 1]
           |
    [QKD Hub Central]
          /|\
         / | \
        /  |  \
      N2  N3  N4
```
- Hub central distribue les clés
- Avantage: Scalabilité modérée
- Risque: Point unique de défaillance

#### Réseau Maillé (Mesh)
```
[Node1] -- [Node2]
  |  \    /  |
  |   \  /   |
[Node4]- [Node3]
```
- Chaque nœud peut communiquer directement
- Avantage: Redondance, robustesse
- Défi: Complexité de gestion

### 4.2 Composants du Réseau Quantique

**Source de photons:**
- Source cohérente laser classique
- Source de paires intriquées (SPDC - Spontaneous Parametric Down Conversion)
- Quantum dots (présentatrices)

**Canaux de transmission:**
- Fibre optique (atténuation ~0.2 dB/km)
- Espace libre (satellite quantum communication)
- Combiné hybride (terrestre + satellite)

**Répéteurs quantiques:**
- Extendent la portée au-delà de 200 km
- Utilise l'intrication et la téléportation quantique
- Défis: Faibles taux de succès actuels (1-10%)

**Détecteurs:**
- Single-Photon Avalanche Diodes (SPAD)
- Effondrement en avalanche (APD)
- Efficacité: 50-85%
- Bruit de sombre: 100-10000 comptes/s

### 4.3 Paramètres de Performance

| Paramètre | Valeur Typique | État de l'Art |
|-----------|---|---|
| Distance | 100 km | 512 km (fibre) |
| Débit de clés | 1 kbps | 4 Mbps (lab) |
| QBER acceptable | <11% | <4% (cible) |
| Temps de latence | 1-10 ms | 100 μs |
| Fiabilité | 95% | 99% |

---

## 5. Cybersécurité Quantique

### 5.1 Menaces Quantiques

#### Menace 1: Harvesting (Collect Now, Decrypt Later)
- Adversaire collecte le trafic crypté actuel
- Attend ordinateur quantique suffisamment puissant
- Déchiffre rétrospectivement les données

**Impact:** Données sensibles avec long cycle de vie menacées
**Recommandation:** Données hautement sensibles = Transition immédiate QKD

#### Menace 2: Attaques sur Implémentations (Side-Channel)
- Timing attacks
- Analyse de puissance
- Rayonnement électromagnétique

**Exemple:** Faille Eve-drops dans BB84 faible
- Détecteur "ébloui" par photons forts
- Attaquant envoie photons intenses → Eve voit tout

#### Menace 3: Failles d'Interopérabilité
- Différentes implémentations QKD incompatibles
- Dégradation gracieuse vers crypto classique non détectée
- Attaque MITM exploite fallback

### 5.2 Sécurité de la QKD

#### Sécurité Inconditionnelle
- Sécurité mathématique indépendante de capacités computationnelles
- Preuve: Théorème no-cloning + incertitude
- Limitation: Suppositions sur la source/détecteur

**Niveaux d'incertitude (BB84):**
- Pas d'écoute: QBER ~ 1%
- Écoute totale: QBER ~ 25% (pour bits détectés)
- Seuil de rejet: QBER > 11%

#### Sécurité Pratique (Device-Dependent)
- Implémentations réelles ont failles
- Détecteurs non-idéaux
- Sessions "Eve" partielles détectées statiquement

**Solution: MDI-QKD (Measurement-Device-Independent)**
- Élimine les défauts du détecteur
- Réduit attaques side-channel
- Prix: Complexité et débit réduits

### 5.3 Intégration avec Cryptographie Post-Quantique

**Pourquoi les deux?**

```
Stratégie de transition (NIST/ETSI):

Phase 1 (Maintenant):
┌─ RSA/ECC pour service existants
├─ QKD pour canaux prioritaires
└─ Évaluation PQC

Phase 2 (2025-2026):
┌─ Déploiement PQC (Kyber/Dilithium)
├─ Expansion QKD (réseaux urbains)
└─ Intégration hybride

Phase 3 (2027+):
┌─ Migration complète post-quantum
├─ QKD pour données ultra-sensibles
└─ Attestation de sécurité quantique
```

**Avantages du mode hybride:**
- Défense en profondeur
- Pas de dépendance monolithique
- Transition progressive

### 5.4 Sécurité de Transmission

#### Canaux d'authentification
- Essentiels pour prévention MITM
- Basé sur cryptographie classique
- Bottleneck de sécurité en QKD

**Solution envisagée:**
- Dériver clés d'authentification de QKD initial
- Rotation périodique via QKD
- Certificats quantiques signés classiquement initialement

#### Intégrité du réseau
- Attaques par rejeu (replay attacks)
- Attaques de timing (délai d'acheminement)
- Attaques par brouillage (jamming) en espace libre

---

## 6. Implémentations Actuelles

### 6.1 Systèmes Commerciaux

| Fournisseur | Produit | Protocole | Portée |
|---|---|---|---|
| ID Quantique | Cerberis | BB84 variante | 100 km |
| Toshiba | QKD Node | E91 variante | 100+ km |
| Huawei | Quantumpass | MDI-QKD | 200+ km |
| PsiQuantum | - | Architecture complète | À développer |

### 6.2 Déploiements Gouvernementaux

**Europe:**
- Quantum Internet Alliance (QIA): 11 millions d'euros
- Réseau EuroQCI: Connexions nationales + transfrontalières

**China:**
- Réseau Jinan (10 nœuds)
- Satellite Micius (2017+)
- Objectif: Internet quantique globe 2030

**USA:**
- Chicago Quantum Exchange
- National Quantum Initiative (NQI)
- DARPA Quantum Internet Alliance

### 6.3 Cas d'Usage Actuels

1. **Secteur financier:** Échange de clés de chiffrement entre banques
2. **Gouvernement:** Communications diplomates sensibles
3. **Infrastructure critique:** SCADA, générateurs électriques
4. **Santé:** Données patient confidentielles (RGPD)

---

## 7. Défis et Perspectives

### 7.1 Défis Techniques

| Défi | Statut | Approche |
|---|---|---|
| Distance (> 1000 km) | En cours | Répéteurs quantiques, satellites |
| Débit (> 1 Mbps) | Laboratoire | TF-QKD, multiplicité de canaux |
| Maintien cohérence | Critique | Mémoires quantiques à long terme |
| Intégration réseau | Actif | Standards ETSI, architecture modulaire |
| Coûts | Élevés | Économies d'échelle, miniaturisation |

### 7.2 Défis Organisationnels

- **Standardisation:** Nécessité de normes interopérables
- **Compétences:** Pénurie de physiciens quantiques industriels
- **Investissement:** Besoin de R&D long terme
- **Régulation:** Cadre légal pour communications quantiques

### 7.3 Roadmap 2026-2035

```
2026: Déploiement QKD urbain (50+ villes)
      PQC standardisé en production

2027: Premiers répéteurs quantiques (portée 500 km+)
      Hybridation systématique QKD+PQC

2028-2029: "Q-Day" potentiel (10+ millions de qubits)
           Transition urgente cryptographie sensible

2030-2035: Internet quantique régional établi
           Post-quantum crypto dominant
           Threat quantum obsolète (crypto pré-2025)
```

---

## 8. Références

### Articles Académiques

1. Bennett, C. H., & Brassard, G. (1984). "Quantum cryptography: Public key distribution and coin tossing." *Proceedings of IEEE International Conference on Computers, Systems and Signal Processing*, 175-179.

2. Ekert, A. K. (1991). "Quantum cryptography based on Bell's theorem." *Physical Review Letters*, 67(6), 661.

3. Brunner, N., Cavalcanti, D., Pironio, S., Scarani, V., & Brunner, B. (2014). "Bell nonlocality." *Reviews of Modern Physics*, 86(2), 419.

4. Scarani, V., Bechmann-Pasquinucci, H., Cerf, N. J., Dušek, M., Lütkenhaus, N., & Peev, M. (2009). "The security of practical quantum key distribution." *Reviews of Modern Physics*, 81(3), 1301.

5. Arnon-Friedman, R., Renner, R., & Scarani, V. (2018). "Simple and tight device-independent security proofs." *SIAM Journal on Computing*, 48(1), 181-225.

### Rapports et Standards

6. ETSI (2020). "GS QKD 001: Quantum Key Distribution (QKD); Use Cases." V1.1.1.

7. ETSI (2021). "GS QKD 004: Quantum Key Distribution (QKD); Security Proofs." V2.1.1.

8. NIST (2022). "Post-Quantum Cryptography Standardization: Fourth Round Candidates."

9. Quantum Internet Alliance (QIA). "Roadmap for the Quantum Internet Alliance."

### Ressources de Recherche

10. arXiv.org - Quantum Physics section: https://arxiv.org/list/quant-ph/

11. NIST Quantum Information Science Program: https://www.nist.gov/programs/VHL/quantum-information-science

12. Quantum Internet Alliance: https://www.quantum-internet-alliance.org/

