# Quantum Communications: Presentation Structure & Key Points
## Master Cybersecurity - Project Presentation

---

## SLIDE 1-2: INTRODUCTION
**Slide 1: Title**
```
QUANTUM COMMUNICATIONS & CYBERSECURITY
Securing the Future of Telecommunications

Authors: [Group Members]
Date: [Presentation Date]
University: [Université]
Master: Cybersécurité
```

**Slide 2: Context**
- RSA/ECC encryption will be vulnerable to quantum computers
- Timeline: Q-Day possibly 2030-2035
- Current data encrypted today = at risk tomorrow
- Solution: Quantum Key Distribution (QKD) + Post-Quantum Cryptography (PQC)

---

## SLIDE 3-5: QUANTUM FUNDAMENTALS

**Slide 3: Quantum Superposition**
```
Classical bit: 0 OR 1
Quantum bit (Qubit): 0 AND 1 simultaneously

|ψ⟩ = α|0⟩ + β|1⟩

Where |α|² + |β|² = 1

Key point: Measurement FORCES the qubit to one state
           No measurement = we don't know the state
```

**Slide 4: No-Cloning Theorem**
```
Theorem: It is IMPOSSIBLE to copy an unknown quantum state

Implications for cryptography:
✓ A spy cannot duplicate a photon and send it unchanged
✓ Any eavesdropping attempt MUST measure the state
✓ Measurement = qubit state CHANGES or DESTROYS
✓ This change is DETECTABLE

This is the heart of quantum security
```

**Slide 5: Quantum Entanglement**
```
Two entangled photons share a single quantum state

Example (Bell state):
|Φ⁺⟩ = (|00⟩ + |11⟩)/√2

Property: Measuring one photon INSTANTLY correlates the other
         (NOT communication, correlations only)

Used in: E91 protocol, MDI-QKD
```

---

## SLIDE 6-8: WHY QUANTUM SECURITY IS NECESSARY

**Slide 6: The Harvest-Now-Decrypt-Later Threat**
```
Today (2024):
Adversary collects encrypted traffic (TLS, RSA, ECC)
Stores petabytes in secure vault

Tomorrow (2035):
Quantum computer becomes operational
"Decrypt now" - all stored data becomes readable

Impact:
- Diplomatic cables (100-year sensitivity)
- Industrial secrets (30-50 year life)
- Medical records (Lifetime sensitivity)
```

**Slide 7: Classical vs Quantum Security**
```
CLASSICAL ENCRYPTION (RSA-2048):
- Secure NOW: 2^128 computational effort
- Secure with Quantum Computer: ✗ BROKEN
- Attack: Shor's Algorithm (polynomial time)
- Timeline: Vulnerable from 2030+

QUANTUM KEY DISTRIBUTION:
- Secure NOW: Unconditional (based on physics)
- Secure with Quantum Computer: ✓ STILL SECURE
- Attack: IMPOSSIBLE (violates quantum mechanics)
- Timeline: Protected forever
```

**Slide 8: Defense Strategy**
```
Recommended Approach (NIST/ETSI):

          2024-2025          |          2025-2030         |        2030+
Immediate |  Urgent         |  Mainstream              |  Established
─────────────────────────────────────────────────────────────────────
- RSA/ECC | - Deploy QKD    | - PQC standards         | - PQC dominant
- Keep current  | - PQC pilots  | - QKD expansion        | - QKD specialist
                | - Evaluate PQC | - Hybrid integration   | - Archive protection
```

---

## SLIDE 9-12: QUANTUM KEY DISTRIBUTION - BB84 PROTOCOL

**Slide 9: BB84 Protocol Overview**
```
Bennett-Brassard 1984 - First practical QKD protocol

Goal: Securely distribute encryption keys

Process (4 steps):
1. Alice generates random bits & random bases
2. Alice encodes bits in photons using bases
3. Alice sends photons to Bob
4. Bob receives and measures using random bases
```

**Slide 10: BB84 Step-by-Step**
```
STEP 1: Setup
Alice's bits:      0 1 0 0 1 1 0 1
Alice's bases:     + × + × × + × +
                   (+ = rectilinear, × = diagonal)

STEP 2: Encoding & Transmission
Photon 1: |0,+⟩ → Photon 2: |1,×⟩ → ... → Bob

STEP 3: Bob's Measurement
Bob's bases:       × + + × + × + ×
Bob's result:      1 1 0 0 1 ? 0 1 (? = wrong base)

STEP 4: Sifting
Alice: "Your bases correct?" → Positions 1,3,4,7,8
Bob keeps only: 1 0 0 0  (and Alice keeps matching bits)
→ Shared secret key: 1001 (50% data loss is normal)
```

**Slide 11: Eavesdropping Detection in BB84**
```
Scenario: Eve tries to intercept

Alice → Photon → Eve → Modified Photon? → Bob

What happens:
1. Eve doesn't know Alice's bases
2. Eve guesses (50% wrong guesses)
3. When Eve guesses wrong → qubit state CHANGES
4. Bob receives corrupted photon
5. Quantum Bit Error Rate (QBER) increases

Detection:
- No eavesdropping: QBER ≈ 1% (measurement noise)
- Total eavesdropping: QBER ≈ 25%
- Threshold: QBER > 11% → ABORT session
```

**Slide 12: BB84 Security Properties**
```
✓ Unconditional Security
  - Theoretically impossible to break (quantum physics)
  - NOT dependent on mathematical complexity

✓ Eavesdropping Detection
  - Any spy caught with high probability
  - Uncertainty principle guarantees disturbance

⚠ Authentication Required
  - Need secure channel for Sift messages
  - Current solution: RSA-based initially

⚠ Practical Limitations
  - Distance: ~100 km in fiber (attenuation)
  - Key rate: ~1 kbps typical
  - Implementation side-channels: Detector attacks
```

---

## SLIDE 13-14: MODERN QKD PROTOCOLS

**Slide 13: Decoy-State QKD & Twin-Field QKD**
```
Evolution of BB84:

DECOY-STATE QKD (Shor & Preskill):
- Problem: Real lasers emit multi-photons
- Multi-photon states = vulnerability (Eve flaw)
- Solution: Mix real states + dummy "decoy" states
- Result: Can use classical lasers → commercial feasible
- Deployment: Current commercial systems

TWIN-FIELD QKD (TF-QKD):
- Problem: Distance limit ~100 km due attenuation
- Solution: Alice & Bob both send photons to middle point
- Photons interfere at "untrusted" measurement point
- Result: Works with receiver on my side only
- Benefit: Distance 500+ km, rate 4 Mbps (lab)
- Status: Cutting edge research (2024-2026)
```

**Slide 14: Comparison - Three Main Protocols**
```
┌─────────────────┬──────────────┬────────────┬────────────┐
│ Protocol        │ BB84         │ E91        │ MDI-QKD    │
├─────────────────┼──────────────┼────────────┼────────────┤
│ Basis           │ No-cloning   │ Entangle.  │ Entangle.  │
│ Implementations │ ★★★ Simple   │ ★ Complex  │ ★ Very     │
│ Distance        │ 100 km       │ 100 km     │ 200+ km    │
│ Keyrate         │ 1 kbps       │ 0.1 kbps   │ 0.01 kbps  │
│ Robustness      │ ★★ Medium    │ ★★ Medium  │ ★★★ High   │
│ Deployment      │ Now          │ Research   │ 2026+      │
└─────────────────┴──────────────┴────────────┴────────────┘

Choice: Industry uses BB84 variants (simple, practical)
        Research explores E91/MDI (better theory)
```

---

## SLIDE 15-16: POST-QUANTUM CRYPTOGRAPHY STANDARDS

**Slide 15: NIST PQC Standardization (2022)**
```
Selected Algorithms (NIST FIPS 203-205):

ENCRYPTION (KEM):
✓ CRYSTALS-Kyber    - Lattice-based (Learning With Errors)
                      Key: 800 bytes, Ciphertext: 768 bytes

DIGITAL SIGNATURES:
✓ CRYSTALS-Dilithium - Lattice-based, compact
✓ SPHINCS+           - Hash-based, conservative
✓ FALCON             - Lattice-based, ultra-compact

All resistant to Shor's algorithm quantum attack
Migration timeline: 2025-2027 for critical systems
```

**Slide 16: QKD + PQC Integration (Defense in Depth)**
```
Why BOTH QKD and PQC?

Defense-in-Depth Strategy:

┌─ Message Encryption
│  └─ AES-256(K_combined)
│
├─ K_combined = K_QKD ⊕ K_PQC
│  ├─ K_QKD: From QKD (unconditional security)
│  └─ K_PQC: From Kyber (post-quantum resistant)
│
└─ Advantage:
   - QKD fails? → PQC still protects
   - PQC breaks? → QKD still protects
   - Better than either alone

Deployment: Hybrid mandatory 2025-2030 (ETSI)
```

---

## SLIDE 17-19: NETWORK ARCHITECTURE

**Slide 17: QKD Network Topologies**
```
Three main architectures:

POINT-TO-POINT        STAR TOPOLOGY         MESH TOPOLOGY
┌─────────┬─────────┐  ┌─────────┐         ┌──────┐
│ Alice   │ Bob     │  │ Node1   │      ┌──│Node1 ├──┐
└─────────┴─────────┘  └────┬────┘      │  └──────┘  │
                         ┌──┴──┐        │           │
Simple, Limited       │ Hub  │    ┌────┴────┐   ┌──┘
Scaling              └──┬───┘    │ Node2    │   │
                      ┌─┴─┐   ┌─┴─┐      ┌─┴───┘
                      │N2 │   │N3 │  ─   │
                      └───┘   └───┘      └──────┘

Scalable,           Robust,
Limited Cost        Complex Management

Current:  Most deployments use Star (compromise)
Future:   Transition to Mesh (long-term)
```

**Slide 18: Physical Channel Options**
```
FIBER OPTIC (Terrestrial):
✓ Reuses existing telecom infrastructure
✓ Distance: 100 km typical (attenuation ~0.2 dB/km)
✗ Break risk (backhoe fades!)
Industry: Primary for cities/regions

SPACE-FREE (Satellite):
✓ Global coverage without fiber
✓ Distance: Unlimited (same continent)
✗ Weather dependent (clouds block)
✗ Low throughput (~100 bps from Micius 2017)
Research: China Jinan + Europe planning

HYBRID (Best):
✓ Fiber backbone urban (high speed)
✓ Satellite bridges long-distance (reliability)
Future infrastructure: 2025-2030
```

**Slide 19: Quantum Network Components**
```
Complete QKD system:

┌─────────────┐       ┌──────────────┐       ┌──────────┐
│ Source      │──────│ Transmission │──────│ Detection│
│ (Photons)   │      │   Channel    │      │(SPAD)    │
└─────────────┘      └──────────────┘      └──────────┘
  • Laser            • Fiber (100km)         • Efficiency:
  • SPDC             • Variable attenuation    50-85%
                                            • Noise sombre:
                                              100-10k counts/s

        ┌──────────────────┐
        │  Quantum         │
        │  Repeater (?)    │  [Optional for 200+ km]
        │                  │  • Memory quantum
        │  - Extends       │  • Entanglement resource
        │    distance      │  • Teleportation
        └──────────────────┘

Current status:
- Repeaters: Research labs only (1-2 seconds coherence)
- Production repeaters: 2027+ earliest
```

---

## SLIDE 20-23: REAL-WORLD DEPLOYMENTS

**Slide 20: Current QKD Deployments (2024)**
```
EUROPE:
✓ Switzerland: Genève-CERN fiber QKD
✓ Netherlands: EuroQCI backbone planning
✓ Germany: Stromanbieter (electricity grid) pilots

ASIA:
✓ China: Jinan network (10 nœuds), Micius satellite
✓ Japan: Tokyo metropolitan trials
✓ India: Delhi-Agra fiber link

NORTH AMERICA:
✓ USA: Chicago Quantum Exchange (network)
✓ Canada: Secure communications trials

COMMERCIAL VENDORS:
- ID Quantique (Switzerland)
- Toshiba (Japan)
- Huawei (China)
- PsiQuantum (UK - future)
```

**Slide 21: Finance Sector - Use Case**
```
WHY BANKS DEPLOY QKD:

Data Sensitivity:
├─ Transaction keys: 5-30 year confidentiality
├─ Customer data: 30-50 years (regulatory PII)
└─ Strategic secrets: 50+ years

Regulation:
├─ Basel III: Secure communications mandated
├─ Future Standard: Post-quantum proof required
└─ Timeline: 2027+ enforcement expected

Practical Deployment:
┌─ Unilever Paris Office
│  ├─ Backend cryptographic key distribution
│  ├─ AES-256 encryption of transactions
│  └─ Re-keying daily via QKD
│
└─ Inter-bank (SWIFT):
   ├─ QKD pilots 2023-2024 (10 banks)
   ├─ Production deployment 2025+ visé
   └─ Estimated deployment rate: 50% major banks by 2028
```

**Slide 22: Critical Infrastructure - Use Case**
```
SCADA/POWER GRID:

Current Threat:
- SCADA remote access via RDP/SSH
- Credentials compromise = blackout risk
- RSA compromise = all sessions readable
- Impact: Regional electricity outage

QKD Solution:
└─ Central ← [QKD Secure Channel] ← Substation
   └─ Commands encrypted AES-256(K_QKD)
   └─ Re-key hourly (vs daily finance)
   └─ Any decryption attempt detected immediately

Deployments:
├─ USA: NIST GridEx security tests
├─ Germany: Pre-deployment planning
└─ Japan: Tohoku Electric (resilience post-Fukushima)

Timeline:
- 2024-2025: Pilots 5-10 grids
- 2027-2030: Rolling deployment +50 substations
- 2035+: Standard in critical infrastructure
```

**Slide 23: Healthcare/GDPR - Use Case**
```
DATA PROTECTION REQUIREMENTS:

Sensitive Data:
├─ Genetic information:     80+ year sensitivity
├─ Mental health:           80+ year sensitivity
├─ Diagnoses:              30+ year sensitivity
└─ Treatment history:      Lifetime sensitivity

GDPR Breach Notification:
├─ Current: Notify regulators/patients (2018)
├─ Future: Proof of "adequate crypto" required (2027+)
└─ Projection: QKD/PQC mandatory by 2029

Implementation (Hospital):
┌─ EHR (Electronic Health Records)
│  ├─ Encrypted: AES-256
│  ├─ Key distribution: QKD urban link + PQC backup
│  └─ Key rotation: Daily full fresh
│
└─ Ultra-sensitive data (Genetic/Psychiatric):
   ├─ Private fiber to hospital archives
   ├─ Separate QKD node
   └─ Audit trail: Every access logged + encrypted

Compliance:
- ICH (EU) recommendations 2023+
- France: CNIL guidance TBD (2025)
```

---

## SLIDE 24-26: SECURITY THREATS & DEFENSES

**Slide 24: Practical Attacks on QKD**
```
THEORETICAL vs PRACTICAL SECURITY:

Theoretical (Physics):
✓ Unconditional security (if perfect devices)

Practical (Real Equipment):
⚠ Implementation side-channels:

1. DETECTOR BLINDNESS:
   - Detector may saturate with intense photons
   - Eve floods detector → clicks only at Eve's signal
   - Result: Eve sees everything, Bob sees nothing
   - Fix: MDI-QKD (independent detector)

2. TIMING ATTACKS:
   - Measurement processing time varies by qubit state
   - Eve measures processing delay
   - Reveals bits via side-channel
   - Fix: Constant-time randomization

3. ELECTROMAGNETIC SIDE-CHANNEL:
   - Power consumption of gates reveals computation
   - Kocher 1998 first example
   - Eve with radio sniffer outside lab
   - Fix: Shielding + randomization
```

**Slide 25: Man-in-the-Middle Attack (QKD)**
```
AUTHENTICATION CHALLENGE:

Problem (Circular dependency):
├─ QKD = secure key exchange
├─ QKD itself needs authentication to prevent MITM
└─ But authentication needs crypto! (circular)

Attack Example:
Alice ---→ [Eve: I'm Alice] ←--- Bob
           (Eve poses as both)

Eve intercepts entire QKD handshake:
├─ Gets key shared with Alice
├─ Gets key shared with Bob
├─ Rewrites channel in middle (MITM)
└─ Communicates both directions

Current Solution:
├─ Pre-shared certificates (RSA initially, 2024-2026)
├─ Out-of-band authentication (phone call, in-person)
├─ Infrastructure network-level security
└─ Not perfect but solves 90% + other defenses

Long-term:
- Derivative keys first QKD session (authentication only)
- Symmetric authentication (no PKI circularity)
- Timeline: 2027+ standards expected
```

**Slide 26: Quantum vs Classical Cryptanalysis**
```
SECURITY GUARANTEES COMPARISON:

                 Classical (RSA) │ Quantum (QKD)
────────────────────────────────┼─────────────
Current (2024):  ✓ Secure       │ ✓ Secure

2030 (Q-Day):    ✗ BROKEN       │ ✓ Still secure
                 (10M qubits)    │

2035:            ✗ BROKEN       │ ✓ Still secure
                 (standard)      │

Data collected    VULNERABLE     PROTECTED
2020-2024:       NOW onwards     Forever

Why QKD survives Q-Day:
├─ Security = Physics (no-cloning)
├─ Quantum computer can't violate no-cloning
├─ Even with unlimited qubits
└─ Cryptanalysis attack impossible

Defense recommendation (2025+):
- Store sensitive data NOW encrypted AES-256(K_QKD)
- K_QKD sourced from QKD deployment
- Annual key rotation keeps data protected
```

---

## SLIDE 27-29: CHALLENGES & LIMITATIONS

**Slide 27: Technical Challenges**
```
┌────────────────────┬──────────┬─────────────┐
│ Challenge          │ Status   │ Solution    │
├────────────────────┼──────────┼─────────────┤
│ Distance (>500km)  │ Critical │ Repeaters   │
│ Throughput (Mbps)  │ Limited  │ TF-QKD      │
│ Quantum Memory     │ Hard     │ Research    │
│ Integration        │ In prog. │ ETSI std.   │
│ Cost per km        │ High     │ Scale       │
└────────────────────┴──────────┴─────────────┘

Distance Problem:
- Fiber attenuation: -0.2 dB/km
- 100 km = 1/5000 photons reach Bob
- Solution #1: Shorter distances (city = 50 km)
- Solution #2: Repeaters (2027+)
- Solution #3: Satellite bridges (2030+)

Throughput Problem:
- BB84: ~1 kbps maximum
- Finance needs: 1-100 kbps
- Solution: TF-QKD (4 Mbps lab, 100 kbps realistic)
- Timeline: Production 2025-2027
```

**Slide 28: Cost & Timeline Analysis**
```
DEPLOYMENT COST ESTIMATE:

City-scale QKD network (50 km, 10 nodes):
├─ Equipment (sources, detectors, repeaters): €2-5M
├─ Fiber (installation/leasing 50 km): €1-3M
├─ Integration & commissioning: €0.5-1M
└─ Total: €3.5-9M
   Per-km cost: ~€70-180K/km (declining)

Return on Investment (Finance):
├─ Value: Impossible to breach AES-256
├─ Threat avoidance worth >€50M (data breach)
├─ ROI breakeven: 3-5 years
└─ Worth it for large institutions

Scaling Effects (2024-2030):
2024: €180K/km (boutique)
2026: €80K/km (moderate deployment)
2028: €40K/km (standardized, mass prod.)
2030: €20K/km (commodity)
→ Exponential decline as scale increases
```

**Slide 29: Standardization & Interoperability**
```
STANDARDS ORGANIZATIONS:

ETSI (European Telecommunications Standards):
├─ GS QKD 001: Use Cases
├─ GS QKD 002: Architecture
├─ GS QKD 003: Network Integration
├─ GS QKD 004: Security Proofs
└─ Status: Published, followed by EU vendors

NIST (National Institute of Standards, USA):
├─ Quantum Safe Cryptography Project
├─ PQC Standardization: FIPS 203-205 (2022)
└─ Status: International adoption in progress

ISO/IEC:
├─ 30551: Quantum key distribution
├─ 23917: Quantum safe crypto requirements
└─ Status: In development (2024-2026)

Challenges:
├─ Incompatible QKD protocols (vendor-specific)
├─ Fallback to classical crypto not detected tricky
├─ Network-level integration undefined
└─ Solution: Converge on 2-3 standards by 2026
```

---

## SLIDE 30-32: ROADMAP & RECOMMENDATIONS

**Slide 30: Global QKD Deployment Roadmap (2024-2035)**
```
TIMELINE PROJECTION:

2024-2025:  Initial Deployment Phase
├─ Pilots: Banking, government, critical infrastructure
├─ Cities deployed: 10-20 worldwide
├─ Key rate: 1 kbps typical
└─ Coverage: 50-100 km range per network

2025-2027:  Rapid Expansion Phase
├─ Standards finalized (ETSI, NIST, ISO)
├─ Production repeaters available (500 km range)
├─ Cities deployed: 100+ worldwide
├─ Key rate: 10-100 kbps average
└─ Regional networks connecting

2027-2030:  Consolidation Phase (Critical!)
├─ Post-quantum crypto mainstream (Kyber/Dilithium)
├─ Hybrid deployment (QKD + PQC required)
├─ Q-Day threat zone (ordinateur quantique possible)
├─ Key decision: Archive re-encryption NOW
└─ Late adopters penalized (security debt)

2030-2035:  Mature Infrastructure
├─ Continental QKD networks operational
├─ Long-term data protection standard procedure
├─ Quantum computers exist (threat realization)
├─ Migration incomplete = liability
└─ QKD commodity, PQC mandatory

```

**Slide 31: Strategy for France / EU**
```
RECOMMENDED ACTIONS (2024-2026):

IMMEDIATE (2024-2025):
1. Budget: €50-100M R&D quantum photonics
   - INRIA quantum labs, CNRS, universities

2. Urban Pilots: 2 networks
   - Paris-Lyon backbone (500 km)
   - Benelux interconnection (existing ETSI work)

3. Standardization: ETSI WG leadership
   - France underrepresented; increase contribution

4. Industry Partnerships:
   - Orange Telecom: Fiber infrastructure leverage
   - Ubisoft: Secure communications (IP protection)
   - BNP Paribas: Finance leadership

MEDIUM-TERM (2025-2027):
1. National Strategy:
   - QKD deployment roadmap ministériels
   - PQC transition plan (Kyber adoption timeline)

2. Education:
   - 5000+ engineers quantum cryptography trained
   - Curriculum additions: Master/École ingénieur

3. Archive Program:
   - Identify long-term sensitive data (30-50Y) NOW
   - Begin AES-256(K_QKD) migration 2025
   - Complete before 2030 (Q-Day insurance)

4. Regulation:
   - CNIL guidance on post-quantum crypto
   - Compliance deadline 2027 for sensitive sectors
   - Healthcare, Finance, Government priority

Budget: €300-500M total (2024-2027)
```

**Slide 32: Q&A Preparation Summary**
```
Key Talking Points (Distilled):

✓ WHY quantum: "Harvest-now-decrypt-later is real threat"
✓ WHEN urgent: "2025-2027 critical window before Q-Day"
✓ HOW secure: "Physics-based security, not just math"
✓ WHAT cost: "High now, declining rapidly as scale grows"
✓ WHO benefits: "Banking, Healthcare, Government, Critical Infra"

Common Questions:

Q: "RSA still useful?"
A: "Yes, for short-term data. Complement with QKD long-term."

Q: "Quantum computers exist already?"
A: "Not yet (2024). Google's 53-qubit ≠ cryptanalysis capable."

Q: "Can satellites replace fiber?"
A: "Complementary, not replacement (weather, latency)."

Q: "Why not just bigger encryption keys?"
A: "Size doesn't help vs. quantum; different physics required."

Q: "EU behind China?"
A: "Quality research strong; deployment speed lags. Catch-up 2025-2027."

Confidence Areas:
✓ Fundamentals & protocols: Strong
✓ Architecture & deployment: Strong
✓ Security implications: Strong
⚠ Exact timelines: Soft (say "estimated")
⚠ Cost breakdowns: Ranges only (vendor-dependent)
```

---

## SLIDE 33: REFERENCES (ENGLISH)

### Academic Papers
1. Bennett, C. H., & Brassard, G. (1984). "Quantum cryptography: Public key distribution and coin tossing."
   *IEEE International Conference on Computers, Systems and Signal Processing*, 175-179.

2. Ekert, A. K. (1991). "Quantum cryptography based on Bell's theorem."
   *Physical Review Letters*, 67(6), 661.

3. Brunner, N., et al. (2014). "Bell nonlocality."
   *Reviews of Modern Physics*, 86(2), 419-478.

4. Scarani, V., et al. (2009). "The security of practical quantum key distribution."
   *Reviews of Modern Physics*, 81(3), 1301-1350.

5. Arnon-Friedman, R., Renner, R., & Scarani, V. (2018). "Simple and tight device-independent security proofs."
   *SIAM Journal on Computing*, 48(1), 181-225.

### Standards & Reports
6. ETSI (2020). "GS QKD 001: Quantum Key Distribution (QKD); Use Cases." V1.1.1.

7. ETSI (2021). "GS QKD 004: Quantum Key Distribution (QKD); Information Security Proofs." V2.1.1.

8. NIST (2022). "Post-Quantum Cryptography Standardization: Fourth Round Candidates."

9. Quantum Internet Alliance. "Roadmap for the Quantum Internet Alliance."
   https://www.quantum-internet-alliance.org/

### Online Resources
10. arXiv.org Quantum Physics: https://arxiv.org/list/quant-ph/

11. NIST Quantum Information Science: https://www.nist.gov/programs/VHL/quantum-information-science

12. QIA Research Portal: https://www.quantum-internet-alliance.org/

---

## SLIDE 34: THANK YOU / QUESTIONS
```
QUANTUM COMMUNICATIONS & CYBERSECURITY
Protecting Tomorrow's Data Today

Questions?

Contact: [Group Email]
Presentation Repo: [GitHub if applicable]
```

---

## PRESENTATION TIPS FOR SPEAKERS

### Delivery Strategy
1. **Language:** Present in French OR English (choose one language for entire presentation)
   - Slides: English (mandated)
   - Spoken: French or English (flexible per student)
   - Recommendation: French for audience comfort, English for international credibility

2. **Pacing:**
   - Fundamentals (Slides 3-5): SLOW - use diagrams, repeat concepts
   - Protocols (Slides 9-14): MODERATE - walk through BB84 step-by-step
   - Deployment (Slides 20-26): Fast - real examples keep interest
   - Recommendations (Slides 31-32): Engaging - future vision

3. **Body Language:**
   - Stand central (not desk-hidden)
   - Point at slides (build engagement)
   - Maintain eye contact (jury evaluation)
   - Pause 3 seconds between ideas (absorb)

4. **Common Pitfalls to Avoid:**
   - ❌ Reading slides verbatim (death by PowerPoint)
   - ❌ Equations/math heavy (lose non-physicist jury)
   - ❌ Assumptions deep quantum knowledge (explain terms)
   - ❌ Vague timelines ("maybe someday" = weak)
   - ❌ Defensive tone (you're experts!)

### Group Members Distribution (20 min total)
Suggested timing (assuming 3-4 members):

**Member 1 - Fundamentals (4 min):**
- Slides 1-5 (Intro + Quantum basics)
- Known to all, confident, warm-up speaker

**Member 2 - Protocols & Standards (5 min):**
- Slides 9-16 (BB84 detailed + PQC)
- Technical leader, live demo potential if prepared

**Member 3 - Deployment & Real-World (6 min):**
- Slides 20-26 (Use cases, attacks, current status)
- Most animated, cases relatable

**Member 4 - Strategy & Q&A (5 min):**
- Slides 31-36 (Recommendations, questions)
- Strong closer, fields questions effectively

### Questions Likely from Jury:
1. "Explain eavesdropping detection in < 2 min"
2. "Difference between QKD and PQC?"
3. "When can France deploy?"
4. "Cost-benefit for business?"
5. "Is quantum computing a hoax for media?" [Be diplomatic!]

---

**END OF PRESENTATION GUIDE**
*Last updated: April 8, 2026*
