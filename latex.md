%==============================================================
% RAPPORT - Communications Quantiques et Cybersécurité
% Auteurs : DRISSI Anasse & RENOUT Quentin
% Master Cybersécurité - Année 2025/2026
%==============================================================

\documentclass[12pt, a4paper]{report}

%--- Encodage & langue ---
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage[french]{babel}

%--- Mise en page ---
\usepackage[top=2.5cm, bottom=2.5cm, left=2.5cm, right=2.5cm]{geometry}

%--- En-tête et pied de page ---
\usepackage{fancyhdr}
\pagestyle{fancy}
\fancyhf{}
\fancyhead[L]{\textit{Communications Quantiques et Cybersécurité}}
\fancyhead[R]{\textit{Sujet 10}}
\fancyfoot[L]{\textit{DRISSI Anasse \& RENOUT Quentin}}
\fancyfoot[C]{\thepage}
\fancyfoot[R]{\textit{Master Cybersécurité -- 2025/2026}}
\renewcommand{\headrulewidth}{0.5pt}
\renewcommand{\footrulewidth}{0.5pt}

%--- Style de la page de garde (sans en-tête/pied) ---
\fancypagestyle{plain}{
  \fancyhf{}
  \renewcommand{\headrulewidth}{0pt}
  \renewcommand{\footrulewidth}{0pt}
}

%--- Mathématiques & physique ---
\usepackage{amsmath}
\usepackage{amssymb}
\usepackage{braket}   % Pour la notation de Dirac |0>, |1>

%--- Tableaux ---
\usepackage{booktabs}
\usepackage{array}
\usepackage{tabularx}

%--- Couleurs & boîtes ---
\usepackage{xcolor}
\usepackage{tcolorbox}
\tcbuselibrary{skins, breakable}

%--- Listes ---
\usepackage{enumitem}

%--- Liens hypertextes ---
\usepackage{hyperref}
\hypersetup{
    colorlinks=true,
    linkcolor=blue!60!black,
    urlcolor=blue!60!black,
    citecolor=blue!60!black,
    pdftitle={Rapport Communications Quantiques},
    pdfauthor={DRISSI Anasse, RENOUT Quentin},
}

%--- Code / blocs verbatim ---
\usepackage{listings}
\usepackage{fancyvrb}

%--- Graphiques ---
\usepackage{graphicx}
\usepackage{tikz}
\usetikzlibrary{shapes, arrows, positioning, calc}

%--- Titres de chapitres personnalisés ---
\usepackage{titlesec}
\titleformat{\chapter}[block]
  {\normalfont\Large\bfseries\color{blue!70!black}}
  {\thechapter.}{1em}{}
  [\titlerule]

\titleformat{\section}[block]
  {\normalfont\large\bfseries\color{blue!50!black}}
  {\thesection}{1em}{}

\titleformat{\subsection}[block]
  {\normalfont\normalsize\bfseries\color{blue!40!black}}
  {\thesubsection}{1em}{}

%--- Espacement chapitres ---
\titlespacing*{\chapter}{0pt}{10pt}{20pt}

%--- Polices ---
\usepackage{lmodern}

%==============================================================
\begin{document}

%--------------------------------------------------------------
%  PAGE DE GARDE
%--------------------------------------------------------------
\begin{titlepage}
  \thispagestyle{empty}
  \centering

  \vspace*{1.5cm}

  % Filet supérieur
  {\color{blue!70!black}\rule{\linewidth}{2pt}}\\[0.4cm]

  {\LARGE\bfseries\color{blue!80!black} Master Cybersécurité}\\[0.2cm]
  {\large Année 2025/2026}\\[0.4cm]

  {\color{blue!70!black}\rule{\linewidth}{0.8pt}}\\[1.5cm]

  {\huge\bfseries\color{blue!70!black} Sujet 10 -- Communications quantiques}\\[1cm]

  {\LARGE\bfseries Communications Quantiques\\et Cybersécurité}\\[0.5cm]

  {\large\itshape Rapport de projet}\\[2cm]

  {\color{blue!70!black}\rule{0.5\linewidth}{0.8pt}}\\[1cm]

  {\large\bfseries Binôme :}\\[0.5cm]
  {\Large DRISSI Anasse \& RENOUT Quentin}\\[2cm]

  \vfill

  % Filet inférieur
  {\color{blue!70!black}\rule{\linewidth}{0.8pt}}\\[0.3cm]
  {\small Rapport rédigé dans le cadre du Master Cybersécurité -- 2025/2026}
  {\color{blue!70!black}\rule{\linewidth}{2pt}}

\end{titlepage}

%--------------------------------------------------------------
%  SOMMAIRE
%--------------------------------------------------------------
\tableofcontents
\thispagestyle{fancy}
\newpage

%==============================================================
\chapter{Introduction}
%==============================================================

Les communications quantiques représentent une révolution dans le domaine de la sécurité informatique et des télécommunications. Elles exploitent les principes de la mécanique quantique pour offrir des garanties de sécurité théoriquement inviolables.

\medskip

\begin{tcolorbox}[colback=blue!5!white, colframe=blue!60!black, title=Contexte]
\begin{itemize}[noitemsep]
  \item Obsolescence prévue de la cryptographie RSA/ECC face aux ordinateurs quantiques
  \item Besoin urgent de solutions cryptographiques résistantes aux menaces quantiques
  \item Développement de protocoles de distribution de clés quantiques (QKD)
  \item Standardisation en cours par le NIST pour l'algorithme post-quantique
\end{itemize}
\end{tcolorbox}

%==============================================================
\chapter{Fondamentaux Théoriques}
%==============================================================

\section{Principes Quantiques Essentiels}

\subsection{Superposition quantique}

Un qubit peut exister dans une superposition d'états $\ket{0}$ et $\ket{1}$. Sa représentation mathématique est :
\[
  \ket{\psi} = \alpha\ket{0} + \beta\ket{1} \quad \text{avec} \quad |\alpha|^2 + |\beta|^2 = 1
\]
L'observation force le qubit à s'effondrer vers un état défini.

\subsection{Intrication quantique (\textit{Quantum Entanglement})}

Deux qubits intriqués partagent un état quantique non séparable. L'état de Bell caractéristique est :
\[
  \ket{\Phi^+} = \frac{\ket{00} + \ket{11}}{\sqrt{2}}
\]
Il en résulte une corrélation instantanée entre les mesures distantes, sans toutefois permettre de communication supraluminale.

\subsection{Principe d'incertitude et No-Cloning}

\begin{itemize}
  \item \textbf{Théorème du non-clonage :} Il est impossible de copier un état quantique inconnu.
  \item Mesurer un qubit détruit l'information qu'il porte.
  \item Ce principe constitue le fondement de la détection d'écoute en QKD.
\end{itemize}

\section{Mécanique Quantique appliquée à la Cryptographie}

\textbf{Bases de codage :}
\begin{itemize}
  \item Codage qubit-photon : polarisation, phase, direction
  \item Deux bases non-orthogonales : rectilinéaire ($+$/$\times$) et diagonale ($/$)
  \item Incompatibilité de mesure : mesurer dans la mauvaise base donne un résultat aléatoire
\end{itemize}

%==============================================================
\chapter{Aspects de Recherche}
%==============================================================

\section{Domaines de Recherche Actifs}

\subsection{Quantum Key Distribution (QKD)}

\begin{description}
  \item[BB84 (Bennett-Brassard 1984)] Premier protocole QKD pratique. Utilise quatre états quantiques (2 bases $\times$ 2 bits). Sa sécurité est prouvée de manière inconditionnelle, mais nécessite un canal classique authentifié.

  \item[E91 (Ekert 1991)] Basé sur l'intrication, utilise les états de Bell. La détection d'écoute s'appuie sur la violation des inégalités CHSH. Théoriquement plus robuste, mais plus complexe à implémenter.

  \item[Protocoles modernes]~
  \begin{itemize}
    \item \textbf{Decoy-state QKD :} améliore les implémentations faibles
    \item \textbf{Twin-field QKD (TF-QKD) :} augmente la portée (jusqu'à 500 km)
    \item \textbf{MDI-QKD :} élimine les failles d'implémentation
  \end{itemize}
\end{description}

\subsection{Quantum Internet Alliance (QIA)}

\begin{itemize}
  \item Développement de l'Internet quantique multi-n\oe{}uds
  \item Distribution de clés sur longues distances
  \item Mémoires quantiques et répéteurs quantiques
\end{itemize}

\subsection{Standardisation}

\begin{itemize}
  \item \textbf{ETSI} -- Norme GS QKD pour l'implémentation sécurisée et recommandations d'architecture
  \item \textbf{NIST} -- Post-Quantum Cryptography Standardization :
    \begin{itemize}
      \item CRYSTALS-Kyber (chiffrement)
      \item CRYSTALS-Dilithium (signature)
      \item Déploiement parallèle QKD + PQC recommandé
    \end{itemize}
\end{itemize}

\section{État de l'Art}

\textbf{Exploits réalisés :}
\begin{itemize}
  \item Distance record : 512 km de fibre optique (2022, Chine-Europe)
  \item Débit record : 4 Mbps en laboratoire (TF-QKD)
  \item Maillage QKD urbain : plusieurs villes (Genève, Chine, États-Unis)
\end{itemize}

\medskip

\textbf{Publications clés :}
\begin{itemize}
  \item Brunner \textit{et al.} (2014) : \og Bell nonlocality \fg{}
  \item Scarani \textit{et al.} (2009) : \og The security of practical QKD \fg{}
  \item Arnon-Friedman \textit{et al.} (2018) : \og Simple and tight device-independent security \fg{}
\end{itemize}

%==============================================================
\chapter{Architecture Réseau Quantique}
%==============================================================

\section{Topologies de Réseau}

\subsection{Point-à-Point (P2P)}

Première topologie implémentée, elle consiste en un lien direct entre deux nœuds Alice et Bob, via un canal QKD et un canal classique authentifié. Simple mais non scalable, elle convient aux liens bancaires sécurisés.

\begin{center}
\begin{tikzpicture}[node distance=4cm, every node/.style={draw, rounded corners, minimum width=1.5cm, minimum height=0.8cm, fill=blue!10}]
  \node (A) {Alice};
  \node (B) [right of=A] {Bob};
  \draw[->, thick, blue!70!black] (A) -- node[above, draw=none, fill=none] {Canal QKD} (B);
  \draw[->, dashed, gray] ([yshift=-4pt]A.east) -- node[below, draw=none, fill=none] {Canal auth.} ([yshift=-4pt]B.west);
\end{tikzpicture}
\end{center}

\subsection{Réseau en Étoile (\textit{Star})}

Un hub central distribue les clés à plusieurs nœuds. La scalabilité est modérée mais un point unique de défaillance existe.

\subsection{Réseau Maillé (\textit{Mesh})}

Chaque nœud peut communiquer directement avec les autres. Cette topologie offre redondance et robustesse, au prix d'une complexité de gestion accrue.

\section{Composants du Réseau Quantique}

\begin{description}
  \item[Sources de photons] Source cohérente laser classique, source de paires intriquées (SPDC -- \textit{Spontaneous Parametric Down Conversion}), quantum dots.
  \item[Canaux de transmission] Fibre optique (atténuation $\sim$0{,}2 dB/km), espace libre (satellite), combiné hybride.
  \item[Répéteurs quantiques] Étendent la portée au-delà de 200 km via l'intrication et la téléportation quantique. Taux de succès actuels : 1--10\%.
  \item[Détecteurs] SPAD (\textit{Single-Photon Avalanche Diodes}), APD. Efficacité : 50--85\%, bruit de sombre : 100--10\,000 coups/s.
\end{description}

\section{Paramètres de Performance}

\begin{table}[h!]
\centering
\caption{Paramètres de performance des réseaux QKD}
\begin{tabularx}{\textwidth}{lXX}
\toprule
\textbf{Paramètre} & \textbf{Valeur Typique} & \textbf{État de l'Art} \\
\midrule
Distance          & 100 km        & 512 km (fibre) \\
Débit de clés     & 1 kbps        & 4 Mbps (labo) \\
QBER acceptable   & $<$11\%       & $<$4\% (cible) \\
Temps de latence  & 1--10 ms      & 100 $\mu$s \\
Fiabilité         & 95\%          & 99\% \\
\bottomrule
\end{tabularx}
\end{table}

%==============================================================
\chapter{Cybersécurité Quantique}
%==============================================================

\section{Menaces Quantiques}

\subsection{Menace 1 : Harvesting (\textit{Collect Now, Decrypt Later})}

Un adversaire collecte le trafic chiffré actuel et attend de disposer d'un ordinateur quantique suffisamment puissant pour le déchiffrer rétrospectivement.

\begin{tcolorbox}[colback=red!5!white, colframe=red!60!black, title=Impact \& Recommandation]
\textbf{Impact :} Les données sensibles à long cycle de vie sont particulièrement exposées.\\
\textbf{Recommandation :} Transition immédiate vers QKD pour les données hautement sensibles.
\end{tcolorbox}

\subsection{Menace 2 : Attaques sur Implémentations (\textit{Side-Channel})}

\begin{itemize}
  \item Attaques temporelles (\textit{timing attacks})
  \item Analyse de consommation
  \item Rayonnement électromagnétique
\end{itemize}

\textbf{Exemple :} Faille sur détecteurs en BB84 -- l'attaquant envoie des photons intenses éblouissant le détecteur (\textit{detector blinding}) et peut intercepter les clés.

\subsection{Menace 3 : Failles d'Interopérabilité}

\begin{itemize}
  \item Différentes implémentations QKD incompatibles
  \item Dégradation non détectée vers crypto classique
  \item Attaque MITM exploitant le fallback
\end{itemize}

\section{Sécurité de la QKD}

\subsection{Sécurité Inconditionnelle}

La sécurité mathématique est indépendante des capacités de calcul de l'adversaire. Elle repose sur le théorème du non-clonage et le principe d'incertitude.

\medskip

\textbf{Niveaux de QBER (\textit{Quantum Bit Error Rate}) en BB84 :}
\begin{itemize}
  \item Sans écoute : QBER $\approx$ 1\%
  \item Écoute totale : QBER $\approx$ 25\%
  \item Seuil de rejet : QBER $>$ 11\%
\end{itemize}

\subsection{Sécurité Pratique (\textit{Device-Dependent})}

Les implémentations réelles présentent des failles dues à des détecteurs non-idéaux et à des hypothèses non vérifiées. La solution \textbf{MDI-QKD} (\textit{Measurement-Device-Independent}) élimine les défauts du détecteur et réduit les attaques \textit{side-channel}, au prix d'une complexité et d'un débit réduits.

\section{Intégration avec la Cryptographie Post-Quantique}

\textbf{Stratégie de transition recommandée par le NIST/ETSI :}

\begin{description}
  \item[Phase 1 -- Maintenant] RSA/ECC pour services existants, QKD pour canaux prioritaires, évaluation PQC.
  \item[Phase 2 -- 2025-2026] Déploiement PQC (Kyber/Dilithium), expansion QKD (réseaux urbains), intégration hybride.
  \item[Phase 3 -- 2027+] Migration complète post-quantum, QKD pour données ultra-sensibles, attestation de sécurité quantique.
\end{description}

\textbf{Avantages du mode hybride :}
\begin{itemize}
  \item Défense en profondeur
  \item Pas de dépendance monolithique
  \item Transition progressive
\end{itemize}

\section{Sécurité de Transmission}

\begin{description}
  \item[Canaux d'authentification] Essentiels pour prévenir les attaques MITM, basés sur la cryptographie classique. Le goulot d'étranglement est la sécurité de ce canal en QKD.
  \item[Solution envisagée] Dériver les clés d'authentification d'un QKD initial, rotation périodique via QKD, certificats quantiques signés classiquement dans un premier temps.
\end{description}

\medskip

\textbf{Attaques sur l'intégrité réseau :}
\begin{itemize}
  \item Attaques par rejeu (\textit{replay attacks})
  \item Attaques de timing (délai d'acheminement)
  \item Attaques par brouillage (\textit{jamming}) en espace libre
\end{itemize}

%==============================================================
\chapter{Implémentations Actuelles}
%==============================================================

\section{Systèmes Commerciaux}

\begin{table}[h!]
\centering
\caption{Principaux fournisseurs de systèmes QKD commerciaux}
\begin{tabularx}{\textwidth}{lXXX}
\toprule
\textbf{Fournisseur} & \textbf{Produit} & \textbf{Protocole} & \textbf{Portée} \\
\midrule
ID Quantique & Cerberis         & BB84 variante & 100 km \\
Toshiba      & QKD Node         & E91 variante  & 100+ km \\
Huawei       & Quantumpass      & MDI-QKD       & 200+ km \\
PsiQuantum   & --               & Architecture complète & À développer \\
\bottomrule
\end{tabularx}
\end{table}

\section{Déploiements Gouvernementaux}

\begin{description}
  \item[Europe] Quantum Internet Alliance (QIA) : 11 millions d'euros. Réseau EuroQCI : connexions nationales et transfrontalières.
  \item[Chine] Réseau Jinan (10 nœuds), satellite Micius (2017+), objectif Internet quantique global en 2030.
  \item[États-Unis] Chicago Quantum Exchange, National Quantum Initiative (NQI), DARPA Quantum Internet Alliance.
\end{description}

\section{Cas d'Usage Actuels}

\begin{enumerate}
  \item \textbf{Secteur financier :} échange de clés de chiffrement entre banques
  \item \textbf{Gouvernement :} communications diplomatiques sensibles
  \item \textbf{Infrastructure critique :} SCADA, réseaux électriques
  \item \textbf{Santé :} données patient confidentielles (RGPD)
\end{enumerate}

%==============================================================
\chapter{Défis et Perspectives}
%==============================================================

\section{Défis Techniques}

\begin{table}[h!]
\centering
\caption{Principaux défis techniques et approches associées}
\begin{tabularx}{\textwidth}{lXX}
\toprule
\textbf{Défi} & \textbf{Statut} & \textbf{Approche} \\
\midrule
Distance ($>$1000 km)   & En cours   & Répéteurs quantiques, satellites \\
Débit ($>$1 Mbps)       & Laboratoire & TF-QKD, multiplicité de canaux \\
Maintien cohérence       & Critique   & Mémoires quantiques long terme \\
Intégration réseau       & Actif      & Standards ETSI, architecture modulaire \\
Coûts                    & Élevés     & Économies d'échelle, miniaturisation \\
\bottomrule
\end{tabularx}
\end{table}

\section{Défis Organisationnels}

\begin{itemize}
  \item \textbf{Standardisation :} nécessité de normes interopérables
  \item \textbf{Compétences :} pénurie de physiciens quantiques industriels
  \item \textbf{Investissement :} besoin de R\&D à long terme
  \item \textbf{Régulation :} cadre légal pour les communications quantiques
\end{itemize}

\section{Roadmap 2026--2035}

\begin{description}
  \item[2026] Déploiement QKD urbain (50+ villes) ; PQC standardisé en production.
  \item[2027] Premiers répéteurs quantiques (portée 500 km+) ; hybridation systématique QKD + PQC.
  \item[2028--2029] \og Q-Day \fg{} potentiel (10+ millions de qubits) ; transition urgente de la cryptographie sensible.
  \item[2030--2035] Internet quantique régional établi ; cryptographie post-quantique dominante ; menace quantum pré-2025 obsolète.
\end{description}

%==============================================================
\chapter{Références}
%==============================================================

\section*{Articles Académiques}
\addcontentsline{toc}{section}{Articles Académiques}

\begin{enumerate}[label={[\arabic*]}]
  \item Bennett, C. H., \& Brassard, G. (1984). \textit{Quantum cryptography: Public key distribution and coin tossing.} Proceedings of IEEE International Conference on Computers, Systems and Signal Processing, 175--179.

  \item Ekert, A. K. (1991). \textit{Quantum cryptography based on Bell's theorem.} Physical Review Letters, 67(6), 661.

  \item Brunner, N., Cavalcanti, D., Pironio, S., Scarani, V., \& Brunner, B. (2014). \textit{Bell nonlocality.} Reviews of Modern Physics, 86(2), 419.

  \item Scarani, V., Bechmann-Pasquinucci, H., Cerf, N. J., Dušek, M., Lütkenhaus, N., \& Peev, M. (2009). \textit{The security of practical quantum key distribution.} Reviews of Modern Physics, 81(3), 1301.

  \item Arnon-Friedman, R., Renner, R., \& Scarani, V. (2018). \textit{Simple and tight device-independent security proofs.} SIAM Journal on Computing, 48(1), 181--225.
\end{enumerate}

\section*{Rapports et Standards}
\addcontentsline{toc}{section}{Rapports et Standards}

\begin{enumerate}[label={[\arabic*]}, resume]
  \item ETSI (2020). \textit{GS QKD 001: Quantum Key Distribution (QKD); Use Cases.} V1.1.1.

  \item ETSI (2021). \textit{GS QKD 004: Quantum Key Distribution (QKD); Security Proofs.} V2.1.1.

  \item NIST (2022). \textit{Post-Quantum Cryptography Standardization: Fourth Round Candidates.}

  \item Quantum Internet Alliance (QIA). \textit{Roadmap for the Quantum Internet Alliance.}
\end{enumerate}

\section*{Ressources de Recherche}
\addcontentsline{toc}{section}{Ressources de Recherche}

\begin{enumerate}[label={[\arabic*]}, resume]
  \item arXiv.org -- Quantum Physics section : \url{https://arxiv.org/list/quant-ph/}

  \item NIST Quantum Information Science Program : \url{https://www.nist.gov/quantum-information-science}

  \item Quantum Internet Alliance : \url{https://www.quantum-internet-alliance.org/}
\end{enumerate}

%==============================================================
\end{document}
