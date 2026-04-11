# Fiche de Préparation aux Questions - Communications Quantiques

## Structure de Réponse Standard
**Format recommandé:** Réponse courte (1-2 min) suivi de détails si voulu
- Commencer par la réponse directe
- Fournir contexte/motivation
- Donner un exemple concret
- Conclure avec pertinence cybersécurité

---

## SECTION 1: FONDAMENTAUX QUANTIQUES

### Q1: "Qu'est-ce que la superposition quantique et comment l'exploite-t-on en cryptographie?"

**Réponse courte:**
Un qubit en superposition existe simultanément en états 0 et 1 jusqu'à mesure. Cela permet de sonder deux bases cryptographiques (rectilinéaire et diagonale) sans que l'espion ne puisse deviner la bonne sans risque de détection.

**Détails:**
- Mathématiquement: |ψ⟩ = α|0⟩ + β|1⟩
- Exemple BB84: Alice code 4 bits dans 4 photons, utilise 2 bases aléatoires
- Si Eve mesure dans mauvaise base, elle dénature le qubit → Bob détecte anomalie
- Impact: Détection d'écoute GARANTIE si tentée

**Préparation contre-question:** "Comment détecte-t-on l'écoute pratiquement?"
→ Réponse: Via QBER (Quantum Bit Error Rate) : sans écoute ~1%, avec écoute ~25%

---

### Q2: "Le théorème du non-clonage quantique - pourquoi c'est crucial?"

**Réponse courte:**
Impossible de copier un état quantique inconnu. Cette propriété fondamentale empêche un espion de dupliquer les photons pour les renvoyer inchangés à Bob - il DOIT mesurer, donc il DOIT détruire/modifier.

**Détails:**
- Preuve par contradiction: Si clonage existait, on pourrait mesurer deux bases simultanément → viole principe d'incertitude
- Conséquence: Tout espion laisse une trace
- Différence avec crypto classique: Copie RSA = pas de trace, Copie QKD = détectable

**Cas d'usage sécurité:**
- Impossible de "backuper" une clé quantique secrètement
- Empêche vol de clé en mouvement
- Fondamentalement différent de disque dur classique copiable infiniment

**Préparation:** Soyez prêt à expliquer pourquoi "aucun backup quantique possible" n'est pas limitant

---

### Q3: "Intrication quantique (Bell states) - explication simple et application?"

**Réponse courte:**
Deux photons intriqués partagent un état indivisible - mesurer l'un affecte instantanément l'autre, même s'éloignés. En cryptographie (E91), cela permet de détecter tout espion via violation CHSH.

**Détails:**
- État Bell: |Φ⁺⟩ = (|00⟩ + |11⟩)/√2 - mesurer 0 sur A → forcément 0 sur B
- Non-localité Einstein-Podolsky-Rosen (EPR) - pas de transmission d'info (règles de la physique préservées)
- Protocole E91: 3 bases au lieu de 2 → violations CHSH si écoute

**Avantage vs BB84:**
- Sécurité basée sur physique fondamentale (non-localité)
- Plus difficile à contourner théoriquement
- Plus complexe à mettre en œuvre pratiquement

**Préparation:** Ne pas inventer communication "instantanée" - clarifier: corrélation oui, information non

---

## SECTION 2: PROTOCOLES QKD

### Q4: "Expliquez succinctement le protocole BB84 (Bennett-Brassard 1984)"

**Réponse courte (< 2 min):**

**Étape 1 - Préparation:**
- Alice génère N bits aléatoires et N bases aléatoires
- Pour chaque bit: encode dans base rectilinéaire (+) ou diagonale (×)
- Envoie N photons à Bob

**Étape 2 - Mesure Bob:**
- Bob choisit N bases aléatoires
- Mesure chaque photon
- ~50% des bases corrects, ~50% incorrects (résultat aléatoire)

**Étape 3 - Réconciliation:**
- Bob envoie à Alice quelles bases il a utilisé (non secret!)
- Alice dit "correct" ou "incorrect" (public)
- Garde seulement bits où base était correcte (~N/4 bits)

**Étape 4 - Test d'écoute:**
- Alice envoie sous-ensemble de ses bits corrects à Bob via canal classique
- Bob compare ses mesures
- Erreurs > seuil? → Écoute détectée

**Résultat:** Alice et Bob partagent clé secrète, Eve détectée si présente

**Préparation contre-questions:**
- "Pourquoi Alice doit envoyer les bases?" → Besoin de réconciliation, bases elles-mêmes ne sont pas secrètes
- "Peut-on forcer débit plus haut?" → Non, information = 1 bit de clé par photon sûr
- "Quel taux d'erreur acceptable?" → 11% (seuil ETSI) - au-delà = abandon session

---

### Q5: "Différence BB84 vs E91 vs MDI-QKD?"

**Tableau comparatif rapide:**

| Aspect | BB84 | E91 | MDI-QKD |
|--------|------|-----|---------|
| Base théorique | No-cloning | Intrication/Bell | Intrication |
| Bases utilisées | 2 | 3 | 2+ |
| Détection écoute | QBER classique | Violation CHSH | QBER indépendant |
| Implémentation | Simple | Complexe | Très complexe |
| Robustesse deviceDépendant | Faible (détecteur) | Faible | Fort (deviceindépendant) |
| Débit pratique | 1-10 kbps | 0.1 kbps | 0.01-0.1 kbps |
| Portée typique | 50-100 km | 50-100 km | 200+ km |

**Choix en industrie:**
- **BB84 variantes:** Commun, déploiements actuels
- **E91:** Recherche académique
- **MDI-QKD:** Future - sécurité meilleure mais lent

**Préparation:** Savoir que MDI-QKD = "idéal théorique" mais pas prêt production aujourd'hui

---

### Q6: "Protocoles modernes: Twin-Field QKD et Decoy-state - utilité?"

**Réponse courte:**

**Twin-Field QKD (TF-QKD):**
- Augmente portée 500+ km (vs 100 km classique)
- Technique: Chaque partie envoie photons, interfèrent au milieu
- Pas besoin répéteur quantique
- Débit ~ 4 Mbps en lab (vs 1 kbps BB84)

**Decoy-state:**
- Résout problème: Photons réels ≠ Un photon (multi-photon = faille)
- Technique: Alice mélange vraies états + états "leurre" (decoy states)
- Permet utiliser sources laser réalistes (classiques, pas quantum)
- Impact: Fait commercial BB84 possible

**Pourquoi important pour cyber?**
- Decoy-state = QKD déploiement bas-coût
- TF-QKD = Communication sécurisée longue-distance sans satellite
- Ensemble = QKD devient scalable urbain/national

**Préparation:** Ces protocoles = évolutions techniques BB84 de base, pas révolutions conceptuelles

---

## SECTION 3: CYBERSÉCURITÉ QUANTIQUE

### Q7: "Qu'est-ce que la menace 'Harvest Now, Decrypt Later'?"

**Réponse courte:**
Adversaire enregistre trafic chiffré aujourd'hui. Quand ordinateur quantique suffisant existe (2030-2035?), déchiffre rétrospectivement tout ce stocké. Données sensibles actuelles en danger.

**Détails:**
- RSA-2048: Cassable en 8h avec 2 milliards qubits + stabilité
- Données "long shelf-life": Secrets d'état, plans industriels, données médicales
- Aujourd'hui: Espion accumule TB de trafic chiffré TLS
- Demain: Tout devient lisible

**Timeline réaliste:**
- Avant 2030: Attaque peu probable
- 2030-2035: Ordinateurs quantiques viables possibles
- Après 2035: Cryptographie RSA/ECC = non-sécurisée

**Action recommandée:**
- Identifier données sensibles pour long-terme
- Déployer QKD ou PQC (post-quantum crypto) immédiatement
- Budget: Transition cryptographique priorité nationale

**Préparation:** Insister que c'est menace RÉELLE, pas théorique - plusieurs gouvernements planifient déjà

---

### Q8: "Failles side-channel en QKD - exemples?"

**Réponse courte:**
Implémentations réelles (pas théoriques) ont défauts: détecteurs qui saturent, timing attacks, rayonnement EM. Espion peut exploiter sans violer mécanique quantique.

**Exemples concrets:**

**Faille 1 - Aveuglement du détecteur:**
- Détecteur QKD: Efficace pour 1 photon, saturé par (10+ photons intenses)
- Eve envoie photons très intenses
- Détecteur ne "clique" que si photons Eve
- Résultat: Eve voit tout, Bob ne sait pas

**Faille 2 - Timing attacks:**
- Mesure délai entre envoi/réception
- Révèle bits via micro-variations timing
- Exemple: Si photon = polarisation, "temps de traitement" légèrement différent selon orientation

**Faille 3 - Rayonnement EM:**
- Électronique QKD émet EM
- Side-channel analysis (Kocher 1998): Consommation power ∝ données traitées
- Espion proche peut écouter rayonnement → déduit clés

**Solution QKD:**
- MDI-QKD: Élimine défauts détecteur par conception
- Blindage EM: Labos de recherche standards
- Randomisation timing: Courtes latences + jitter aléatoire

**Préparation:** C'est pourquoi sécurité pratique ≠ sécurité théorique - industrie doit vigilance

---

### Q9: "Comment intégrer QKD + cryptographie post-quantique (PQC)?"

**Réponse courte:**
Stratégie défense-en-profondeur double: QKD = sécurité inconditionnelle (basée physique), PQC = sécurité mathématique (post-quantum). Si l'une échoue, l'autre protège.

**Schéma intégration:**

```
Chiffrement hybride (recommandé NIST/ETSI):

Message = "Secret"
    ↓
Chiffrer avec AES-256 (clé = K)
    ↓ K = K_QKD ⊕ K_PQC
    ↓ où:
    ├─ K_QKD = De distribution QKD
    └─ K_PQC = De Kyber (post-quantum)
    ↓
Envoyer: AES-256(Message) + Kyber-chiffré(K_PQC)
```

**Avantages:**
- QKD échoue? → PQC encore sûr
- PQC mathématique cassée (miraculeusement)? → QKD sauver données
- Transition graduelle possible à 2024-2027

**Timeline déploiement (ISO/ETSI recommandé):**
- 2024-2026: Hybride QKD + PQC pour prioritaire
- 2026-2028: Migration complète PQC classiques
- 2028+: QKD pour ultra-sensible uniquement

**Préparation:** Clarifier = pas "QKD replace PQC" mais "complémentaires"

---

### Q10: "Sécurité du canal d'authentification en QKD - problématique?"

**Réponse courte:**
QKD distribue clés chiffrement, mais ELLE-MÊME a besoin authentification pour empêcher Man-in-the-Middle. C'est circulaire: besoin crypto pour distribuer crypto.

**Problème concret:**

```
Scénario classique MITM:

Alice → [Eve fake] ← Bob
 "Bonjour, je suis Alice"
        ↓ Eve pose proxy
                  "Bonjour, je suis Alice"

Eve intercept ENTIÈRE session QKD entre Alice/Bob!
Eve obtient clé → partage à Alice et Bob (légèrement modifiée)
```

**Solutions en pratique:**

1. **Certificats classiques initiaux:**
   - Alice/Bob pré-partagent certificat (hors-bande)
   - Vérifie identité via RSA classique
   - puis exécute QKD pour clés futures

2. **Clés d'authentification dérivées:**
   - Première session QKD = dériver clés d'authentification (pas chiffrement)
   - Sessions futures: Authentifier via ces clés
   - Besoin "seed" initial sûr (pré-distribué)

3. **Architecture réseau:**
   - Nœuds QKD derrière firewall réseau classique sécurisé
   - Pas auto-suffisant = intégration infrastructure existante

**Préparation:** Mentionner = défi pratique majeur, pas théorique, mais soluble via infrastructure classique moderne

---

## SECTION 4: ARCHITECTURE RÉSEAU & IMPLÉMENTATION

### Q11: "Architecture réseau quantique - topologies?"

**Réponse courte:**
Trois modèles: point-à-point (simple, pas scalable), étoile (hub central fait bottleneck), maillé (robuste mais complexe management).

**Comparatif détaillé:**

| Topologie | Simplicité | Scalabilité | Coût | Cas d'usage |
|-----------|-----------|------------|------|-----------|
| Point-Point | ⭐⭐⭐ | ⭐ | ⭐⭐ | Banque-Banque critico |
| Étoile | ⭐⭐ | ⭐⭐ | ⭐⭐⭐ | Campus urbain (~10 nœuds) |
| Maillé | ⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ | Réseaux nationaux 50+ nœuds |

**Exemple déploiement réel:**
- **Genève (SECOQC, 2009):** Topologie étoile - 6 nœuds, hub central
- **China Jinan:** Maillée partielle - 10+ nœuds, redondance régionale
- **EuroQCI (Europe):** Maillée planifiée - Backbones nationaux + transfrontaliers

**Préparation:** Étoile = compromis actuel (2024-2026), maille = objectif long-terme

---

### Q12: "Trajet fibre optique vs communication espace-libre vs hybride?"

**Réponse courte:**
- **Fibre:** Portée 100 km, atténuation ~0.2 dB/km, infrastructure existante réutilisable
- **Espace-libre:** Satellite portée globe, météo problématique, moins atténuation
- **Hybride:** Terrestre réseau + satellite reprise distance

**Détails fibre optique:**

```
Distance vs réalisabilité:

< 50 km:   Direct fibre, no répéteur (courant)
50-150 km: Répéteur optique classique + QKD
150-300 km: Répéteur demi-quantique (expérimental)
300+ km:   TF-QKD ou satellite (recherche)
```

- Atténuation: Chaque 100 km = 1/5000 photons restant
- Bruit: Photons thermiques background ~ 100 comptes/s même fibre noire
- Avantage: Infrastructure télécom existante (99% mondial est fibre)

**Détails espace-libre:**

```
Satellite quantique:
- Micius (China, 2017): Démonstration QKD ↔ sol
- Débit: 10-100 bps (très faible, mais globe)
- Latence: 100 ms
- Météo: Nuages = pas transmission possible
```

- Avantage: Global, pas infrastructure terrestre
- Désavantage: Bas débit, dépendance météo
- Futur: Constellation satellites + terrestre maillée

**Cas d'usage combiné (hybride):**
- Réseau urbain terrestre (fibre) + satellites relais lointain
- Continent via fibre dense + satellite intercontinental
- Redondance: Si fibre casse, satellite continuité

**Préparation:** Hybrid = direction écosystème 2030+

---

### Q13: "Rôle et défis des répéteurs quantiques - timeline réaliste?"

**Réponse courte:**
Répéteurs quantiques étendent portée fibre (actuellement ~100 km) vers 500+ km. Utilisent intrication et téléportation. Défis majeurs: Faibles taux succès (< 10%), besoin mémoires quantiques stables long-terme.

**Principes (très simplifié):**

```
Standard fiber (< 100 km):
Alice ---→ Qubit → Bob

Avec répéteur quantique:
Alice ---→ Qubit → [Répéteur R1] ---→ Qubit → Bob
                    (intrication + téléportation)
```

- Répéteur reçoit photon Alice
- Entrelacer avec mémoire quantique interne
- Mesurer + Envoyer résultat classique (détruit qubit)
- Bob mesure qubit télépor­té = obtient état Alice

**Défis techniques:**

| Défi | Status | Frontier |
|-----|--------|----------|
| Memoire quarantum | Très difficile | 1 seconde (2023) |
| Taux d'intrication | 0.1-1% | 1% suffisant → 500 km |
| Téléportation fidélité | ~85% | Besoin 99%+ |
| Répéteurs en cascade | 2-3 max | Besoin 10+ |

**Timeline optimiste vs réaliste:**

```
Optimiste (NIST):      Réaliste:
2026: Répéteur 1 nœud  2027-2028: Prototype répéteur
2028: Réseau 300 km    2030: Déploiement limité (test)
2030: Continental      2035: Réseau opérationnels
```

**Préparation:** Répéteur quantique = NEXT frontier après QKD urbain, pas immédiate

---

## SECTION 5: STANDARDISATION & RÉGULATION

### Q14: "NIST Post-Quantum Cryptography Standardization - résumé?"

**Réponse courte:**
NIST a sélectionné 4 algorithmes standards (2022):
- **Kyber:** Chiffrement (Key Encapsulation Mechanism)
- **Dilithium:** Signature numérique
- **SPHINCS+:** Signature alternative
- **FALCON:** Signature compacte

Tous résistants attaque Shor (ordinateurs quantiques).

**Timeline:**
- 2022: Finalisation standards (NIST FIPS)
- 2023-2024: Pilotes / Beta
- 2025-2026: Déploiement production
- 2027+: Migration complète recommandée

**Détails sélectionnés:**

**Kyber (chiffrement):**
- Base: Learning With Errors (LWE lattice-based)
- Clé publique: 800 bytes
- Ciphertext: 768 bytes
- Sûr: 128-bits classique ≈ 256-bits post-quantum

**Dilithium (signature):**
- Base: CRYSTALS-Dilithium
- Clé secrète: ~2.5 KB
- Signature: ~2.4 KB
- Équivalent RSA-3072 classique

**Préparation:** Kyber/Dilithium = futurs standards industrie, comparable TLS

---

### Q15: "ETSI QKD Standards - exigences implémentation?"

**Réponse courte:**
ETSI GS QKD (002-004) définent specs techniques:
- GS QKD 004 = Security proofs → exigences QBER, détection eavesdropping
- GS QKD 002 = Architecture système
- GS QKD 003 = Network integration

**Recommandations clés:**

1. **QBER Threshold:** < 11% (BB84 standard)
   - Formation: Mesurer QBER sur bits test
   - Si QBER > 11%: ABORT session entière
   - Pas de degradation gracieuse

2. **Détection eavesdropping:** Oui/Non binaire
   - Pas de "peut-être"
   - Eve partielle visible ou pas?

3. **Channel authentication:** Obligatoire
   - Empêche MITM
   - Peut être classique RSA-2048 (court-terme acceptable)

4. **Key rates et distance:**
   - Recommandation: >1 kbps à 100 km minimum
   - Déploiement urbain visé

5. **Certification:** Laboratoires indépendants
   - CC (Common Criteria) niveau 5+
   - Sécurité physique contrôlée

**Préparation:** ETSI = industrie European, NIST = US - alignement progressif + recommandation hybride

---

## SECTION 6: CAS D'USAGE CRITIQUES

### Q16: "Secteur financier - pourquoi QKD?"

**Réponse courte:**
Banques besoin absolue confidentialité clés chiffrement (RSA problématique post-quantum). QKD distribue clés AES-256 impossibles traduire même avec ordinateur quantique futur.

**Cas d'usage spécifiques:**

1. **Échange inter-bancaire:**
   - Devises: Millions échangés
   - Latence acceptable: 1-10 ms
   - QKD débit: 1-100 kbps → Suffisant

2. **Archivage 30+ ans:**
   - Régulation: Données financière retrouvables 30 ans
   - Harvest-now-decrypt-later: Risque majeur
   - Solution: Chiffrer AES-256(QKD) + Archive immédiate

3. **Conformité régulatrice:**
   - Basle III exige security communications
   - QKD = évidence of due diligence

**Déploiements pilots:**
- **SWIFT (Society for Worldwide Interbank Financial Telecommunication):**
  - Lab 2023: QKD tested avec 10 banques
  - Pilot production: 2024-2025 visé

- **Banque Nationale Belgique:**
  - QKD déploiement bruxelles (2023+)

**Préparation:** Financier = first-mover QKD, législation aidant

---

### Q17: "Infrastructure Critique (SCADA/Énergie) - sécurisation QKD?"

**Réponse courte:**
Substation électrique control via SCADA (Supervisory Control and Data Acquisition). Compromis = blackout régional. QKD sécurise commandes critiques via clés inviolables.

**Risques actuels:**

```
Attaque SCADA classique:

Attaquant → [Internet] → Firewall → [SCADA network] → Interruption électrité
                          (exploit RDP  credentials)
```

- Credentials en plaintext voient dans memory
- RSA compromise: Toute session cryptée lisible
- Impact: Arrêt région entière

**Solution QKD intégrée:**

```
SCADA-QKD:
Centrale ←→ [QKD Appliance] ←→ Substation
              └─ AES-256(QKD)

Avantages:
- Even si credentials volés: AES-256 inviolable
- Clés renouvelées quotidienne
- Eavesdropping détecté immédiatement
```

**Déploiements:**
- **USA (NIST):** GridEx résilience tests
- **Allemagne:** Stromanbieter (energy suppliers) pilots
- **Japan:** Tohoku Electric (post-Fukushima)

**Préparation:** Infrastructure-critique = second wave QKD après finance

---

### Q18: "Santé/RGPD - données patient sensibles - protection?"

**Réponse courte:**
Patient data: Diagnoses, génétique, traitement. RGPD Amendement 2018: Breach notification obligatoire. Long-terme santé data (50+ années patient) risque harvest-now. QKD+PQC = obligation quasi-légale futur.

**Données santé sensibilité:**

| Type | Shelf-life sensibilité | Risque |
|------|------|--------|
| Diagnostic banal | 5 ans | Client disclosure |
| Génétique | 50 ans | Discrimination/assurance |
| Traitements VIH | 80+ ans | Stigmatisation |
| Mental health | 80+ ans | Social ruin |

**Régulation actuelle vs future:**
- **Maintenant (RGPD 2018):** Notification breach suffisant
- **Future (c.2027):** Proof of "adequate crypto" → PQC/QKD
- **Après Q-day (2030+):** QKD obligatoire si long-term data

**Implémentation hôpital:**
- Electronic Health Record (EHR) chiffré AES-256(QKD)
- Certaines données ultra-sensible: Genetic, psychiatric
- Clé rotation: Quotidienne + audit trail complet

**Préparation:** Santé/Privacy = régulation-driven, va accélérer déploiement

---

## SECTION 7: QUESTIONS PIÈGES & RÉPONSES

### Q19: "Mais la physique quantique vs relativité - contradiction?"

**Pièges:**
- "Intrication = communication instantanée?"
- "EPR communication supraluminale?"

**Réponse correcte:**
Non-localité corrélation, pas information. Théorème no-signaling: Aucune info utile peut transmettre > c.

**Explication rapide:**
```
Alice mesure qubit A → résultat aléatoire (classique)
Bob mesure qubit B → résultat corrélé (pas aléatoire!)

Mais Alice ne peut IMPOSER résultat Alice
→ Bob voit "aléatoire" à lui jusqu'à comparer classiquement avec Alice
```

**Préparation:** C'est question test si jury connaît physique basique

---

### Q20: "Pourquoi pas SIMPLEMENT utiliser 256-bit AES classique - pourquoi quantum complexe?"

**Pièges:**
- "AES jamais cassé, quantum inefficace"
- "Déploiement coûteux pour rien"

**Réponse correcte:**
AES-256 actuellement sûr vs attaque computationnelle classique. MAIS ordinateur quantique (Shor 2030+) × Harvest-now données = déchiffrable.

**Timeline critique:**
```
2024: Trafic chiffré RSA-2048 = aujourd'hui sûr, demain risqué
2025: Données sensible (gen, finance, state secrets) = urgent QKD/PQC
2030: Ordinateur quantique supposé possible → Q-day
2035: Toutes données pré-2023 RSA mathématiquement cassable

Durée données bancaire: 30 ans → 1995-2025 RSA tous risqué 2025+
```

**AES vs Quantum pour clé distribution:**
- AES chiffre données (rapide, sûr court-term)
- QKD distribue clés AES (sûr long-term + proof d'absence écoute)
- Complémentaires, pas alternatifs

**Préparation:** Clarifier = QKD pas remplacer AES, mais distribution sûre clés AES

---

### Q21: "Quantum supremacy (Google 2019) - impact QKD?"

**Pièges:**
- "Google cassé crypto?"
- "QKD déjà obsolète?"

**Réponse correcte:**
Google Sycamore: Supériorité computationnelle domaine très spécifique (random problem), pas cryptanalyse. Ordinateur quantique RSA-2048 besoin MILLIONS qubits stables, Google ~50 fragiles.

**Réalités:**

| Paramètre | Google 2019 | Cryptanalyse RSA |
|-----------|----------|---------|
| Qubits | 53 | 2,000,000+ |
| Temps cohérence | μs | minutes+ |
| Taux erreur | 1/100 | <1/million |
| Faisabilité | 2-3 ans | 15-25 ans |

**Timeline impact crypto:**
- 2019-2025: Aucun (quantum computers fragiles)
- 2025-2030: Possible ordinateur cassant RSA-2048 pas certain
- 2030-2035: High probability si investissements soutenus
- Post-2035: Crypto classique pré-2025 cassable

**QKD position:**
- Pas affecté quantum supremacy
- QKD sécurité physique pas computationnelle
- Sécurité même dans univers quantique hostile

**Préparation:** Google ≠ fin crypto, mais début compte-à-rebours

---

### Q22: "RSA peut aussi distribuer clés - pourquoi QKD compliqué?"

**Pièges:**
- "RSA sûr classiquement, pourquoi changer?"

**Réponse correcte:**
RSA sûr *today*, pas *forever*. Shor's algorithm + L qubits = RSA factorisable polynomial-time. QKD sûr même si attaquant=ordinateur quantique illimité.

**Comparaison sécurité:**

```
RSA-2048:
- Classique: 2^128 travail → sûr à jamais (peut-être)
- Quantique: Shor polynomial → Shor factorisable
- Harvest-now-decrypt-later 2035: 100% risque

QKD (BB84):
- Classique: Impossible (théorème no-cloning)
- Quantique: Toujours impossible
- Harvest-now: Zéro risque si clé distruibée sûrement
```

**Pourquoi pas remplacer RSA immédiatement:**
- QKD besoin canal quantique (fibre optique)
- Tout Internet pas fibre quantique (100 km limite)
- RSA/TLS/HTTPS continue long-terme

**Stratégie transition (NIST 2023):**
```
Maintenant:
├─ RSA/ECC cryptage données quotidienne
├─ QKD distribuer clés AES ultra-sensible
└─ Évaluer PQC

2026+:
├─ PQC standard chiffrement
├─ QKD accélération déploiement
└─ Phased migration
```

**Préparation:** RSA ≠ remplacer immédiatement, mais transition commence now

---

## SECTION 8: QUESTIONS OUVERTES EXPECTANTES

### Q23: "Que devrait faire gouvernement français pour QKD 2024-2026?"

**Réponse structurée:**

**Priorité 1 - Invest Research:**
- INRIA/CNRS quantum photonic labs
- Budget: €50-100M (vs DARPA $1.2B US)

**Priorité 2 - Standardisation ETSI alignment:**
- Participer QKD WG (déjà: Oui, partial)
- Aligner PQC NIST → EU eSTandard

**Priorité 3 - Déploiement pilot:**
- Paris-Lyon QKD backbone (500 km fibre)
- Integration avec BNP/Société Générale network
- Timeline: 2025-2026

**Priorité 4 - Éduc/Talents:**
- Curricula universitaire quantum
- Formation 5000+ ingénieurs
- Budget formation: €20M

**Priorité 5 - Stockpile long-term:**
- Archiver données critic (30Y+) AES-256 QKD-distributed
- Lois: PQC obligation 2027 sensibles

---

### Q24: "Principaux risques déploiement QKD 2024-2026 France?"

**Réponse SWOT-style:**

| Strengths | Weaknesses |
|-----------|------------|
| Fiber optic dense | Talent shortage quantum |
| Telecom expertise (Orange) | Commercialisé / costs |
| ETSI leadership | Regulatory fragmented |
| Academic research base | Late vs China/US |

| Opportunities | Threats |
|---|---|
| EU QCI funding | China leads (time) |
| Infrastructure renewal | Post-quantum standards delays |
| Finance sensitive | Security breaches pilot |
| Global soft power | US export controls QKD |

---

### Q25: "Si quantum computing devient réalité 2030 - que pas?"

**Réponse timeline panic/calme:**

**Panic scenarios si pas préparé:**
- Toutes données RSA pré-2025 attaquable immédiatement
- Diplomatic cables century exposed
- Industrial secrets & IP volée
- Finance recalculate entire basis

**Si préparé (2024-2026 transition):**
- RSA → PQC phased (2 ans transition acceptable)
- QKD critical channels depuis 2024 → déjà sûr
- Archive process: Rekey 2023-2025 archives en PQC/QKD before Q-day
- Morale: Post-quantum + QKD hedges

**Préparation:** Timing stress test important, mais pas alarmiste

---

## SECTION 9: CONSEILS PRÉSENTATION GÉNÉRALE

### Structure de présentation recommandée (20 min)

**Timing (20 minutes = 1200 sec):**

```
Intro (2 min)                               Forces:
├─ Présentation groupe                      - Quantum = hot topic
├─ Définition communications quantiques     - Timely avec NIST/ETSI
└─ Importance cybersécurité                 Weaknesses:
                                            - Complexe physicien
Fondamentaux (4 min)                        Solution:
├─ Superposition/intrication (1.5 min)      - Dessins visuels clairs
├─ No-cloning theorem (0.5 min)             - Pas équations lourdes
├─ Principes QKD (2 min)                    - Metaphores quotidiennes
└─ Pourquoi révolution (0 min ⚠️ timing)

Protocoles (5 min)
├─ BB84 (2 min - détaillé)
├─ Variantes modernes (2 min)
└─ Comparaison PQC (1 min)

Architecture & Déploiement (4 min)
├─ Topologies réseau (1 min)
├─ Cas d'usage industrie (2 min)
└─ Implémentations actuelles (1 min)

Cybersécurité & Menaces (3 min)
├─ Harvest-now-decrypt-later (1 min)
├─ Menaces pratiques (1 min)
└─ Défense (1 min)

Conclusion (2 min)
├─ Timeline réaliste 2025-2035
├─ Appel action gouvernement français
└─ Questions
```

### Slides en Anglais - Structure (30-40 slides)

```
Slide 1: Title + Authors + Date
Slide 2: Agenda
Slides 3-5: Quantum Fundamentals (Superposition, Entanglement, No-cloning)
Slides 6-8: Classic Cryptography vs Quantum (Why needed)
Slides 9-12: Protocol Deep Dive (BB84 protocol + diagram)
Slides 13-14: Modern Protocols (Decoy-state, TF-QKD)
Slides 15-16: PQC Comparison (NIST standards)
Slides 17-19: Network Architecture (P2P, Star, Mesh topologies)
Slides 20-23: Real Deployments (China, Europe, US, Switzerland examples)
Slides 24-26: Security Threats (Harvest-now, Side-channel, MITM)
Slides 27-29: Practical Implementation Challenges (Distance, Cost, Standardization)
Slides 30-31: Use Cases (Finance, Healthcare, Critical Infrastructure)
Slides 32-33: Timeline & Roadmap (2025-2035)
Slides 34-35: French / EU Strategy Recommendations
Slide 36: Q&A
Slide 37: References (papers, NIST, ETSI, arXiv)
```

### Points d'amélioration présentation

**À ÉVITER:**
1. Équation de Schrödinger sur slide - tue attention
2. Débat EPR paradoxe - controversé without PhD physics
3. Histoires "Alice & Bob" trop longues (5+ min)
4. Chiffres de déploiement inexact - vérifier source

**À FAIRE:**
1. Diagramme photon polarisation clair (vertical/horizontal)
2. Animation "bit detection" Eve catching photon
3. Graphique timeline threat (2024/2030/2035)
4. Photo réelle QKD equipment (ID Quantique, Toshiba)
5. Live comparison: "Si Eve écoute" → QBER + chart

---

## SECTION 10: RESSOURCES PRÉPARATION SUPPLÉMENTAIRES

### Livres Recommandés

1. **"Quantum Cryptography and Quantum Computing" (Aharanov & Ben-Or, 2008)**
   - Pour théorie fondamentale

2. **"The Little Book of Quantum Computing" (Rieffel & Polak)**
   - Pour intuition sans math lourdee

### Videos YouTube (anglais)

- MIT OpenCourseWare: "Quantum Computing" Prof. Isaac Chuang
- NIST Quantum YouTube channel
- TEDx talks quantum cryptography

### Papers Académiques (Faciles premières lectures)

- Brunner et al. (2014): "Bell nonlocality" - très lisible, foundational
- Vazirani & Vidick (2014): "Fully Device-Independent Quantum Key Distribution"

### Ressources en ligne

- https://quantuminternet.org/ (QIA portal)
- https://csrc.nist.gov/projects/post-quantum-cryptography/
- https://www.etsi.org/deliver/etsi_gs/QKD/001_099/001/02.01.01_60/gs_qkd_001v020101p.pdf

---

## CHECKLIST PRE-PRÉSENTATION (24h avant)

- [ ] Slides révisées anglais (grammaire + orthographe)
- [ ] Vidéo projecteur test (resolution OK?)
- [ ] Timing lecture entière (aller vite? trop lent?)
- [ ] Imprimer slides en cas problème tech
- [ ] Familiariser avec questions ci-dessus (minimum 10)
- [ ] Préparer papier 1-2 questions pièges pour membres groupe
- [ ] Dormir 8h veille présentation (cognition critique!)
- [ ] Arriver 15 min avant room (setup + breathe)

---

**FIN FICHE**

*Dernière mise à jour: 8 Avril 2026*
*Auteur: Assistant de préparation Master Cybersécurité*
