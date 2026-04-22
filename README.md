# Template LaTeX - Rapport de Fin d'Études EPITA

> **Adaptée pour la majeure SRS (Systèmes, Réseaux & Sécurité) - EPITA Promotion 2026**
> Modifications réalisées conformément aux directives spécifiques de la majeure
> transmises par Sébastien BOMBAL, responsable de majeure.

---

*Based on [SFE-EPITA-TEMPLATE](https://github.com/Le-Jy/SFE-EPITA-TEMPLATE)
by Le-Jy - adapté et enrichi pour les exigences SRS.*

---

Ce dépôt contient le template LaTeX pour le Rapport de Stage de Fin d'Études (SFE) de l'EPITA, adapté pour la majeure SRS. Il a été conçu pour reproduire fidèlement la charte graphique et la structure demandées par l'école, tout en assurant une rédaction modulaire et centralisée, et en intégrant les exigences spécifiques communiquées par la majeure SRS.

## Modifications apportées par rapport à la template originale

- Réorganisation de l'ordre des chapitres conformément aux directives SRS
- Ajout de la synthèse exécutive bilingue (français + anglais)
- Ajout d'une section Introduction
- Ajout d'une section Apprentissages scientifiques et techniques (section centrale SRS)
- Ajout d'une section Valeur ajoutée
- Ajout d'une section Conclusion distincte
- Ajout d'un emplacement dédié pour le planning visuel (Gantt)
- Ajout du support bibliographique via biblatex (style IEEE)

## Structure du projet

- `main.tex` : Le document principal à compiler, contenant la configuration de vos variables et l'inclusion des chapitres.
- `epita-sfe.sty` : Le package personnalisé contenant la charte graphique. **Il gère toute la mise en page**, la page de garde, les en-têtes/pieds de page, et charge les dépendances nécessaires.
- `references.bib` : Le fichier de bibliographie au format BibTeX (style IEEE).
- `chapters/` : Dossier contenant chaque chapitre du rapport séparé dans des fichiers `.tex` distincts.

| Fichier | Contenu |
|---|---|
| `00_introduction.tex` | Introduction, contexte général, problématique, fil directeur |
| `01_exec_sum.tex` | Synthèse exécutive en français + Executive Summary en anglais |
| `02_remerciements.tex` | Remerciements |
| `03_contexte.tex` | Présentation de l'entreprise, équipe, mission |
| `04_recit_stage.tex` | Récit du stage + planning visuel (Gantt) |
| `05_auto_evaluation.tex` | Auto-évaluation et analyse réflexive |
| `06_annexes.tex` | Annexes et traces commentées |
| `07_apprentissages.tex` | Apprentissages scientifiques et techniques |
| `08_valeur_ajoutee.tex` | Valeur ajoutée, livrables, contribution personnelle |
| `09_conclusion.tex` | Bilan, retour critique, perspectives professionnelles |

- `media/` : Dossier dédié pour stocker toutes vos images et logos (logo EPITA, logo entreprise, Gantt exporté...).

## 1. Configuration globale (Fichier `main.tex`)

Dès le début du fichier `main.tex`, vous devez configurer les variables personnelles et spécifiques à votre stage. Celles-ci alimenteront automatiquement la page de garde, ainsi que les en-têtes et pieds de page dynamiques de votre rapport.

```latex
% Informations de l'étudiant
\studentname{Votre Prénom NOM}
\linkedin{https://linkedin.com/in/votrenom}
\promotion{2026}
\majeure{SRS}

% Informations de l'entreprise et du stage
\company{Nom de l'entreprise d'accueil}
\internshipsubject{Titre complet de votre stage de fin d'études}

% Logos
\epitalogo{media/epita_logo.png}
\companylogo{media/company_logo.png}
```

*Note : Si vous ne disposez pas d'un logo d'entreprise, vous pouvez laisser le champ vide (`\companylogo{}`), l'espace s'adaptera sans planter.*

## 2. Commandes personnalisées et macros

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

Cette commande permet d'afficher du texte en magenta et en italique, imitant les directives habituelles laissées par l'école dans le document modèle d'origine. Ce texte disparaîtra si l'option `hideinstructions` est activée.

```latex
\instruction{Ceci est une consigne de rédaction à suivre scrupuleusement.}
```

### C. Environnement "Ligne Directrice" (`guideline`)

Cet environnement produit un encadré gris clair au contour bleu, titré "Conseil / Ligne directrice". Il reste visible même en mode `hideinstructions` - pensez à supprimer ces blocs manuellement avant le rendu final.

```latex
\begin{guideline}
Il est impératif que cette section résume parfaitement les enjeux techniques.
\end{guideline}
```

### D. Génération de la page de garde (`\makeepitatitle`)

Réservée au fichier `main.tex`, cette commande génère automatiquement la page de garde avec vos informations, logos et profil LinkedIn.

```latex
\begin{document}
\makeepitatitle
% Reste du document...
```

### E. Bibliographie

Les références bibliographiques sont gérées via `biblatex` au format IEEE. Ajoutez vos sources dans `references.bib` et compilez avec `biber`.

```bibtex
@online{exemple_web,
  author  = {Nom de l'auteur},
  title   = {Titre de la page},
  year    = {2025},
  url     = {https://example.com},
  urldate = {2025-01-01},
}
```

## 3. Compilation du projet

Avec `biblatex` et `biber`, la séquence de compilation est légèrement différente de la template originale :

```bash
pdflatex main.tex
biber main
pdflatex main.tex
pdflatex main.tex
```

Votre éditeur local (VSCode LaTeX Workshop, TeXMaker) ou Overleaf gère cette séquence automatiquement si configuré correctement.

> **Note Overleaf** : Pensez à sélectionner `biber` comme compilateur de bibliographie dans les paramètres du projet (*Settings → Bibliography tool → Biber*).