# Template LaTeX - Rapport de Fin d'Études EPITA

Ce dépôt contient le template LaTeX pour le Rapport de Stage de Fin d'Études (SFE) de l'EPITA. Il a été conçu pour reproduire fidèlement la charte graphique et la structure demandées par l'école, tout en assurant une rédaction modulaire et centralisée.

## Structure du projet

- `main.tex` : Le document principal à compiler, contenant la configuration de vos variables et l'inclusion des chapitres.
- `epita-sfe.sty` : Le package personnalisé contenant la charte graphique. **Il gère toute la mise en page**, la page de garde, les en-têtes/pieds de page, et charge les dépendances nécessaires.
- `chapters/` : Dossier contenant chaque chapitre du rapport séparé dans des fichiers `.tex` distincts (`01_exec_sum.tex`, `02_remerciements.tex`, etc.) pour une meilleure visibilité.
- `media/` : Dossier dédié pour stocker toutes vos images et logos (notamment le logo de l'EPITA et de votre entreprise).

## 1. Configuration globale (Fichier `main.tex`)

Dès le début du fichier `main.tex`, vous devez configurer les variables personnelles et spécifiques à votre stage. Celles-ci alimenteront automatiquement la page de garde, ainsi que les en-têtes et pieds de page dynamiques de votre rapport.

```latex
% Informations de l'étudiant
\studentname{Votre Prénom NOM}
\linkedin{https://linkedin.com/in/votrenom}
\promotion{2026}
\majeure{Ma Majeure (ex: SSSE)}

% Informations de l'entreprise et du stage
\company{Nom de l'entreprise d'accueil}
\internshipsubject{Titre complet de votre stage de fin d'études}

% Logos
\epitalogo{media/epita_logo.png}    % Le logo complet EPITA
\companylogo{media/company_logo.png} % Le logo de l'entreprise
```
*Note : Si vous ne disposez pas d'un logo d'entreprise, vous pouvez laisser le champ vide (`\companylogo{}`), l'espace s'adaptera sans planter.*

## 2. Commandes personnalisées et macros

Pour vous aider dans la rédaction et le respect du style initial (fichier Word standard de l'EPITA), des commandes et environnements spécifiques ont été mis en place dans le package `epita-sfe`.

### A. Masquer toutes les consignes pour la version finale
Pendant la rédaction, le template affiche les consignes scolaires en magenta ou dans divers encadrés.
Pour la compilation de **votre version PDF finale** à rendre au jury, vous pouvez faire disparaître absolument toutes ces consignes temporaires en un clin d'œil en activant le mode "hideinstructions".

Modifiez l'import du package à la ligne 2 de `main.tex` :
```latex
% Mode rédaction (les consignes de l'école s'affichent)
\usepackage{epita-sfe}

% Mode rendu final (toutes les instructions disparaissent du PDF !)
\usepackage[hideinstructions]{epita-sfe}
```

### B. Commande d'instruction (`\instruction`)
Cette commande permet d'afficher du texte en magenta et en italique, imitant les directives habituelles laissées par l'école dans le document modèle d'origine. Liée à l'option ci-dessus, ce texte disparaîtra si l'option `hideinstructions` est activée dans le `main.tex`.

**Utilisation :**
```latex
\instruction{Ceci est une consigne de rédaction à suivre scrupuleusement.}
```

### C. Environnement "Ligne Directrice" (`guideline`)
Cet environnement produit un encadré gris clair au contour bleu, titré "Conseil / Ligne directrice" exactement comme ce qui peut être trouvé dans les exemples pédagogiques. Si vous avez besoin de formuler une remarque méthodologique.

**Utilisation :**
```latex
\begin{guideline}
Il est impératif que cette section résume parfaitement la rentabilité du projet ainsi que les enjeux techniques.
\end{guideline}
```

### D. Génération de la page de garde (`\makeepitatitle`)
Réservée au fichier `main.tex`, cette commande est appelée juste après le `\begin{document}`. Elle génère automatiquement la structure complexe de la page de garde avec un placement symétrique de vos informations, le centrage de vos logos, et insère les informations de pied de page (votre profil LinkedIn).

**Utilisation :**
```latex
\begin{document}
\makeepitatitle
% Reste du document...
```

## 3. Compilation du projet

Afin d'obtenir votre PDF final (notamment pour que la génération de la Table des Matières soit exacte), effectuez un cycle de compilation classique. Votre éditeur local (VScode LaTeX Workshop, TexMaker) ou Overleaf le fait très souvent de manière automatique.

Si vous le faites à la main dans le terminal de MacOS/Linux :
```bash
pdflatex main.tex
pdflatex main.tex
```
*(Une double compilation est nécessaire lors d'un gros ajout afin de mettre à jour le sommaire et les numéros de page des chapitres intégrés).*
