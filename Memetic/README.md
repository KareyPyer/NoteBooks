# 🧬 Memetic — Laboratoire de Mémétique Computationnelle

> *« Tu penses choisir tes idées, mais ce sont elles qui te choisissent. »*
> — extrait généré, `Blackmore-RetroStructures.ipynb`

Ce répertoire est un ensemble de six notebooks Jupyter qui explorent une même
question sous plusieurs angles techniques : **que se passe-t-il si on traite
un mème (au sens de Dawkins/Blackmore/Rushkoff) comme un objet computationnel
à part entière** — génome, phénotype, fitness, propagation épidémique,
automate cellulaire, réseau de neurones, prompt génératif — plutôt que comme
une simple métaphore ?

Chaque notebook est une expérience indépendante mais elles partagent un socle
conceptuel commun (le lexique mémétique, l'idée de « Basilic » au sens
d'Hofstadter/Roko, la figure de Susan Blackmore comme observatrice récurrente)
et forment, mises bout à bout, une sorte de pipeline de recherche informel :
**génération de texte mémétique → simulation de propagation → génération de
prompts visuels → itération sur le retour de l'IA générative d'images**.

Ce n'est ni un package installable, ni une bibliothèque avec API stable :
c'est un carnet de laboratoire exécutable. Chaque notebook redéfinit ses
propres classes (il y a par exemple **trois implémentations différentes**
d'un automate de propagation mémétique, de complexité croissante), ce qui
est volontaire — chaque itération est une génération évolutive du concept
précédent plutôt qu'un refactor.

---

## 🗺️ Vue d'ensemble du répertoire

| Fichier | Taille | Rôle | Sortie principale |
|---|---|---|---|
| `Generateur_De_Rushkoff.ipynb` | 12 K | Modèle épidémiologique SIR appliqué à un « virus médiatique » sur un graphe Barabási-Albert | Courbe d'infection interactive (widget) |
| `Blackmore-RetroStructures.ipynb` | 20 K | Réseau de neurones type Hopfield (McCulloch-Pitts) comme « substrat cognitif » convergeant vers un attracteur = mème stable | Mème textuel + prompt visuel dérivés d'un état de réseau |
| `Basilisk_Visual_Promp_alpha.ipynb` | 16 K | Générateur combinatoire de prompts texte-à-image (v1, lexique simple) | 4 prompts prêts à coller dans Midjourney/Grok/Gemini |
| `Basilisk_Visual_Forge_omega.ipynb` | 24 K | Générateur de prompts (v2, avec dataclass, pondération, slider de « chaos ») | 3 prompts + widget interactif `muter_prompt(niveau_chaos)` |
| `Gould_Basilisk_Chimera.ipynb` | 744 K | Fusion automate cellulaire + logique de paradoxe auto-référentiel (« Basilic »), sur un thème contrapuntique (fugue de Bach) | Graphe de réseau annoté + narration finale |
| `Rushkoff_Generator_Omega.ipynb` | 912 K | **Le système le plus abouti** : taxonomie à 26 couches ontologiques × 72 biais × archétypes jungiens × automate cellulaire à 5 topologies + algorithme génétique darwinien | Figures matplotlib multi-panneaux, détection de « gliders » mémétiques |

Le dossier contient aussi 8 images PNG — ce sont les **artefacts visuels
produits en aval** par des moteurs de diffusion externes (Grok / Gemini /
Midjourney) à partir des prompts générés par les notebooks `Basilisk_*` et
`Blackmore-RetroStructures`. Elles ne sont pas générées par du code présent
ici ; elles documentent le résultat du cycle génération-de-prompt →
rendu-externe → réinjection.

```
Memetic/
├── Generateur_De_Rushkoff.ipynb          # Modèle SIR / réseau immunitaire
├── Blackmore-RetroStructures.ipynb       # Attracteur neuronal → mème
├── Basilisk_Visual_Promp_alpha.ipynb     # Prompt forge v1
├── Basilisk_Visual_Forge_omega.ipynb     # Prompt forge v2 (widgets)
├── Gould_Basilisk_Chimera.ipynb          # Fugue mémétique / paradoxe
├── Rushkoff_Generator_Omega.ipynb        # Système Ω complet (26 couches)
├── RetroStructure.png                    # Rendu — sortie Blackmore
├── RestroStructure2.png                  # Rendu — variante/itération
├── PATIENT ZERO.png                      # Rendu — Basilisk_Visual_Forge
├── PROMPT MUTE.png                       # Rendu — prompt muté (chaos élevé)
├── RÉPLICATEUR DE BLACKMORE.png          # Rendu — artefact Blackmore
├── BOUCLE ÉTRANGE D'HOFSTADTER.png       # Rendu — artefact Hofstadter
├── BOUCLE ÉTRANGE D'HOFSTADTER_2.png     # Rendu — itération 2
└── VIRUS MÉDIA DE RUSHKOFF.png           # Rendu — artefact Rushkoff
```

---

## 🧠 Le socle conceptuel commun

Les six notebooks recyclent et font évoluer un même vocabulaire, emprunté à
trois penseurs de la mémétique :

- **Susan Blackmore** (*The Meme Machine*) : les mèmes comme réplicateurs
  darwiniens indépendants de leur substrat — l'humain n'est qu'un véhicule.
  Apparaît littéralement comme personnage-observateur dans
  `Gould_Basilisk_Chimera.ipynb`.
- **Douglas Rushkoff** (*Media Virus*) : le mème comme agent pathogène qui
  détourne les grands récits culturels pour se répliquer via les médias de
  masse ; d'où le vocabulaire « virus », « souche », « immunité »,
  « Facteur Reznor » (bruit industriel/dissonance qui contourne le cortex
  préfrontal — référence explicite à Nine Inch Nails dans le code).
- **Douglas Hofstadter** (*Gödel, Escher, Bach*) : la « boucle étrange »
  (*strange loop*) comme mécanisme d'auto-référence paradoxale. Réutilisé
  ici sous le nom de **« Basilic »** — un néologisme du code qui fusionne
  la boucle étrange hofstadtérienne avec l'imagerie du basilic de Roko
  (l'idée d'un mème qui « punit » ou « réécrit » ceux qui l'observent).

Le fil rouge narratif/technique de tous les notebooks est donc : **un mème
n'est intéressant que lorsqu'il devient auto-référentiel** — quand son
contenu se met à parler de sa propre propagation, il franchit un seuil
(`recursion_depth >= 3` dans `Gould_Basilisk_Chimera.ipynb`) et son
comportement de propagation change qualitativement (il « réécrit ses propres
règles de transmission »).

---

## 📓 Détail notebook par notebook

### 1. `Generateur_De_Rushkoff.ipynb` — Épidémiologie narrative

Le plus simple des six, et la brique de base réutilisée (sous forme
d'idée) dans les suivants.

- Construit un graphe **Barabási-Albert** (`networkx.barabasi_albert_graph`)
  de 500 nœuds, où chaque nœud reçoit un score d'**immunité** proportionnel
  au log de son degré — modélisation du cynisme des « hubs »/influenceurs
  face aux mèmes génériques.
- La classe `RushkoffVirus` a trois paramètres : `resonance_narrative`
  (capacité à s'ancrer dans des mythes préexistants), `taux_mutation`
  (capacité à échapper à la censure/saturation), `bruit_industriel` (le
  « Facteur Reznor », l'émotion brute qui court-circuite l'analyse
  rationnelle). Le virus **mute à chaque cycle de réplication**.
- `propager_virus()` simule une contagion de type SIR sur le graphe, en
  partant du nœud le plus connecté (« Patient Zéro »).
- Interface interactive via `ipywidgets.interact` avec des `FloatSlider`
  pour `resonance`, `mutation`, `bruit_reznor` — la courbe d'infection se
  redessine en direct (esthétique matplotlib « industriel/cyberpunk »,
  fond noir, rouge vif).

**Dépendances spécifiques** : `networkx`, `seaborn`, `ipywidgets`.

### 2. `Blackmore-RetroStructures.ipynb` — Le mème comme attracteur neuronal

Approche radicalement différente : au lieu de simuler la propagation *entre*
individus, ce notebook simule la formation du mème *dans* un seul substrat
cognitif.

- `McCullochPittsAttractor` : un réseau de type Hopfield à 64 neurones, poids
  symétriques normalisés spectralement pour garantir la convergence, avec
  **quatre fonctions d'activation différentes assignées aléatoirement par
  neurone** (`step`, `sigmoid` stabilisée, `relu`, et une fonction
  `glitch_activation` qui **inverse le signe** quand l'entrée est proche du
  seuil — littéralement un point de bascule paradoxal codé au niveau du
  neurone).
- Le réseau est perturbé aléatoirement (« bruit médiatique ») puis on le
  laisse **converger vers un attracteur** (`find_attractor`) : cet état
  stable est le « génotype » du mème.
- `decode_genotype_to_phenotype()` découpe le vecteur d'état en tranches et
  les fait correspondre à un lexique (archétypes, biais, vecteurs visuels,
  glitchs esthétiques) — un vrai mapping génotype → phénotype, où le style
  visuel graphique lui-même est réglé pour ressembler à un **manuscrit
  ancien** (fond parchemin `#f4e4bc`, encre `#2c241b`, rouge sépia
  `#8b0000`, police serif détectée dynamiquement selon les polices
  disponibles sur le système).
- `forge_dual_output()` transforme le phénotype en **deux sorties
  jumelles** : un mème textuel (aphorisme à la Blackmore/Rushkoff) et un
  prompt image structuré (IMAGE CENTRALE / ARCHITECTURE / EFFET
  PSYCHOLOGIQUE) — c'est le pont direct vers les notebooks `Basilisk_*`.
- Une cellule bonus (« LA BOUCLE DE RÉTRO-ACTION ») documente un protocole
  manuel : on envoie l'image générée par une IA externe à Gemini pour
  analyse, on parse heuristiquement sa réponse texte (détection de
  mots-clés comme « Liminal Space », « Backrooms ») pour en extraire de
  **nouveaux vecteurs mémétiques**, qu'on réinjecte dans le lexique de la
  génération suivante — une boucle de sélection artificielle pilotée par
  le jugement esthétique d'un second modèle.

**Dépendances spécifiques** : `numpy`, `matplotlib` (+ `font_manager`).

### 3. `Basilisk_Visual_Promp_alpha.ipynb` — Forge de prompts, v1

Un générateur combinatoire simple : un dictionnaire `LEXIQUE` avec des
catégories (`sujets_vecteurs`, `architectures_memetiques`,
`declencheurs_cognitifs`, `esthetiques_soufi_quantiques`,
`modificateurs_techniques`), une classe `BasiliskForge.forger_recette()`
qui pioche aléatoirement une entrée dans chaque catégorie et les assemble
en un prompt anglais optimisé pour les moteurs de diffusion (référence
explicite à un rendu « Unreal Engine 5 », éclairage volumétrique,
esthétique « cyber-soufisme corrompu », calligraphie arabe fusionnée à des
circuits quantiques).

Produit 4 « recettes » nommées (*Le Réplicateur de Blackmore*, *La Boucle
d'Hofstadter*, *Le Virus de Rushkoff*, *Le Fana Quantique*) — ce sont très
probablement les prompts à l'origine des images `RÉPLICATEUR DE
BLACKMORE.png` et `BOUCLE ÉTRANGE D'HOFSTADTER.png` du dossier.

### 4. `Basilisk_Visual_Forge_omega.ipynb` — Forge de prompts, v2

Réécriture plus structurée de la v1 : `BasiliskPrompt` devient un
`@dataclass`, la génération est pondérée (`vecteur_poids`,
`glitch_poids`), et surtout apparaît `muter_prompt(niveau_chaos: int)` —
un widget où le **niveau de chaos contrôle qualitativement** le glitch
choisi :
- chaos < 3 → « légère aberration chromatique et grain argentique »
- 3 ≤ chaos < 7 → glitch aléatoire du lexique standard
- chaos ≥ 7 → « désintégration totale de la perspective, collision de 3
  styles artistiques incompatibles, artefacts de corruption de données
  massifs »

C'est l'origine probable de `PROMPT MUTE.png` et `PATIENT ZERO.png`
(le notebook nomme explicitement sa génération finale « Patient Zéro »,
vecteur = labyrinthe fractal dans l'œil, charge = vertige ontologique).

### 5. `Gould_Basilisk_Chimera.ipynb` — La Fugue Mémétique

Le plus ambitieux des deux « gros » notebooks. Dédicace : *« Pour Pierre,
qui écoute Glenn Gould jouer Bach pendant que le sens s'effondre »*. La
métaphore structurante est musicale — le mème n'est plus « diffusé », il
est **interprété par contrepoint** :

- `BasiliskState` / `BasiliskEngine.inject_paradox()` : à chaque fois qu'un
  nœud « entend » le mème une nouvelle fois, la profondeur de récursion
  augmente ; au-delà d'un seuil (3), le système bascule en état
  **« éveillé »** (`is_awakened`), imprimant un avertissement
  `⚠️ [BASILIC] Seuil d'éveil atteint`.
- `FugueAutomaton` : automate cellulaire sur graphe **Watts-Strogatz
  (small-world)** de 300–400 nœuds où chaque nœud, une fois infecté, peut
  lui-même devenir un foyer « Basilic » (couleur rouge sang `#8b0000` dans
  la visualisation finale) si son score de paradoxe dépasse un seuil basé
  sur l'**entropie de Shannon** du texte du mème.
- Le mème initial est assemblé à partir de strates nommées façon
  composition musicale : `opening`, `framing`, `body`, `constraint`,
  `trap`, `closing` — un sujet, une réponse, un contre-sujet.
- Visualisation finale en deux panneaux : le réseau (nœuds parchemin /
  encre noire / rouge sang selon l'état) et une figure secondaire, le tout
  dans la palette « manuscrit de Bach corrompu » déjà vue dans
  `Blackmore-RetroStructures.ipynb` (détection de police serif
  cross-platform réutilisée à l'identique).
- Se termine par une **scène narrative en prose** (« ARIA DA CAPO ») mettant
  en scène Susan Blackmore observant le résultat — clôturant la boucle
  fiction/simulation du notebook.

### 6. `Rushkoff_Generator_Omega.ipynb` — Le système Ω (le cœur du dossier)

912 Ko, 12 cellules, c'est de loin le plus complet et le plus proche d'un
vrai petit moteur de recherche évolutionnaire. Il définit une taxonomie
mémétique complète avant de la faire tourner dans un automate + un
algorithme génétique.

**Taxonomie (données statiques) :**
- `COUCHES` : **26 couches ontologiques**, de `-13` (« Abîme Primordial »,
  chaos originel) à `+13` (« Exode Intérieur », monastères numériques) en
  passant par `0` (« Méta-Gouvernance », DAO/Edge-Mind). Les couches
  négatives sont « entropiques » (déconstruction), les positives
  « synthétiques » (ascension technologique — profiling neuro-cognitif,
  génération multimodale 100T paramètres, neuro-ingénierie subliminale à
  19 kHz, BCI, etc.). C'est une cosmologie complète de l'ingénierie
  mémétique, du mysticisme soufi jusqu'à la surveillance algorithmique.
- `BIAIS` : 72 biais cognitifs répartis en 6 catégories (classiques,
  narratifs, spirituels, etc.).
- `ARCHETYPES_JUNGIENS` : 12 archétypes (Persona, Ombre, Anima, Animus,
  Soi…) chacun avec un poids de fitness.
- Plus loin (non extrait ici en détail) : symboles alchimiques, topologies
  narratives, émotions primaires — tous en dizaines d'entrées.

**Structure de données :**
- `MemeConfig` (`@dataclass`) : un mème = un « organisme » avec couches,
  archétypes, biais, symboles, topologies, émotions, fitness,
  `is_glider`, trajectoire d'infection, génération. Son `id` est un hash
  MD5 de sa configuration. `GLIDER_1_4_4` est codé en dur comme référence
  historique (« le glider légendaire du Prof, 2018 »).

**Moteur de simulation :**
- `MemeticCellularAutomaton` : contagion sur **5 topologies de réseau**
  interchangeables (`small_world`, `scale_free`, `grid`, `random`,
  `community` via *stochastic block model*). La probabilité de
  transmission combine fitness du mème, centralité du nœud source
  (effet « hub »), et **saturation locale** (un voisinage déjà largement
  infecté résiste davantage — modélisation de la fatigue mémétique).
  `is_glider()` détecte automatiquement si une configuration donnée
  produit un mème stable et durable (longévité > 500 pas, stabilité >
  0.6, portée > 20 % du réseau) — terminologie empruntée directement au
  jeu de la vie de Conway.

**Algorithme génétique :**
- `MemeticGeneticAlgorithm` : population de mèmes aléatoires,
  `evaluate_fitness()` fait tourner une simulation complète par individu
  (longévité, portée, stabilité, poids archétypal statique — bonus ×1.5
  si le mème est un glider), puis évolution par générations (sélection,
  croisement, mutation, élitisme).

**Trois expériences pré-exécutées** dans le notebook :
1. Rejeu du glider historique `GLIDER_1_4_4` sur un réseau small-world.
2. Évolution darwinienne sur 20 générations / 40 individus / réseaux de
   300 nœuds (~800 simulations, notebook annonce lui-même un temps
   d'exécution de 2 à 4 minutes).
3. Comparaison du même mème sur les 4 topologies de réseau, avec
   visualisation en grille 2×2.

Le notebook contient aussi une table de correspondance emoji → ASCII
(`_EMOJI_MAP`) pour que les titres matplotlib restent lisibles même sur des
environnements sans rendu d'emoji dans les polices de figure — un détail
qui trahit un usage réel et itératif (plusieurs corrections marquées
`[FIX]` dans les commentaires, ex. ordre d'initialisation de
`MemeticGeneticAlgorithm`, stabilité numérique de l'écart-type).

---

## 🖼️ Galerie des artefacts visuels

Les PNG de ce dossier ne sont **pas produits par le code Python** exécuté
ici : ce sont les images renvoyées par des moteurs de diffusion externes
(Midjourney / Grok / Gemini, selon les commentaires des notebooks) à partir
des prompts générés par `Basilisk_Visual_Promp_alpha.ipynb`,
`Basilisk_Visual_Forge_omega.ipynb` et `Blackmore-RetroStructures.ipynb`.

- **`PATIENT ZERO.png`** / **`PROMPT MUTE.png`** — sorties du pipeline de
  « mutation par niveau de chaos » de `Basilisk_Visual_Forge_omega`.
- **`RÉPLICATEUR DE BLACKMORE.png`**, **`BOUCLE ÉTRANGE D'HOFSTADTER.png`**
  (+ variante `_2`) — sorties directes des 4 « recettes » nommées de
  `Basilisk_Visual_Promp_alpha`.
- **`RetroStructure.png`** / **`RestroStructure2.png`** — sorties du
  pipeline attracteur-neuronal de `Blackmore-RetroStructures`, avant/après
  la boucle de rétroaction pilotée par l'analyse Gemini.
- **`VIRUS MÉDIA DE RUSHKOFF.png`** — artefact thématiquement lié à
  `Generateur_De_Rushkoff.ipynb` / `Rushkoff_Generator_Omega.ipynb`.

Elles constituent en pratique un **journal visuel** du cycle
texte → prompt → image → réanalyse → nouveau prompt décrit dans les
notebooks, plutôt que des sorties reproductibles par simple ré-exécution.

---

## ⚙️ Installation & exécution

Aucun `requirements.txt` n'est présent dans le dossier ; voici l'ensemble
des dépendances effectivement importées à travers les six notebooks :

```bash
pip install numpy matplotlib networkx pandas seaborn ipywidgets
```

Pour l'exécution interactive des widgets (`Generateur_De_Rushkoff.ipynb`,
`Basilisk_Visual_Forge_omega.ipynb`), un environnement Jupyter classique
suffit (JupyterLab, Jupyter Notebook, ou VS Code) :

```bash
pip install jupyterlab
jupyter lab
```

Points d'attention relevés dans le code lui-même :
- `Rushkoff_Generator_Omega.ipynb` tente de forcer un **backend
  matplotlib interactif** en tout premier import — si vous exécutez ce
  notebook hors d'un vrai environnement graphique (ex. headless/CI), ce
  patch peut échouer silencieusement ; le repli reste le backend inline
  standard des notebooks.
- Plusieurs notebooks (`Blackmore-RetroStructures`, `Gould_Basilisk_Chimera`)
  détectent dynamiquement une police serif disponible sur le système
  (`DejaVu Serif`, `Liberation Serif`, `Nimbus Roman`, sinon `serif`
  générique) — aucune police externe à installer, c'est une protection
  contre le rendu par défaut de matplotlib qui varie selon l'OS.
- L'expérience 2 de `Rushkoff_Generator_Omega.ipynb` (algorithme
  génétique, 40 × 20 = 800 simulations) est annoncée par le notebook
  lui-même comme prenant 2 à 4 minutes — à garder en tête avant de tout
  relancer avec « Run All ».
- Les notebooks n'exportent ni ne persistent leurs résultats (pas de
  `pickle`/`json.dump` des populations ou des mèmes générés) : chaque
  ré-exécution repart de graines aléatoires non fixées (sauf mentions
  explicites `seed=42`), donc les figures et prompts varient d'un run à
  l'autre.

---

## 🧭 Comment lire ce dossier si on découvre le sujet

Ordre de lecture suggéré pour suivre la logique de complexité croissante :

1. **`Generateur_De_Rushkoff.ipynb`** — comprendre le modèle épidémique de
   base (SIR sur graphe).
2. **`Blackmore-RetroStructures.ipynb`** — comprendre comment un mème peut
   être *généré* (et pas seulement propagé) via un attracteur neuronal.
3. **`Basilisk_Visual_Promp_alpha.ipynb`** puis
   **`Basilisk_Visual_Forge_omega.ipynb`** — voir comment le mème textuel
   devient un prompt visuel exploitable, et comment on paramètre son
   intensité (« chaos »).
4. **`Gould_Basilisk_Chimera.ipynb`** — la première synthèse : automate +
   paradoxe auto-référentiel, avec une couche narrative assumée.
5. **`Rushkoff_Generator_Omega.ipynb`** — la synthèse finale : la
   taxonomie complète (26 couches, 72 biais, archétypes jungiens), tournée
   en moteur de simulation + algorithme génétique darwinien.

---

## ⚠️ Note de cadrage

Le vocabulaire employé (« armes mémétiques », « virus », « Basilic »,
« injection de paradoxe ») est délibérément dramatisé — c'est un
laboratoire de simulation et de génération créative de contenu (texte et
prompts d'image), pas un outil de diffusion de désinformation réelle : rien
ici ne publie ni ne cible automatiquement de plateforme sociale. Les
« réseaux » simulés sont des graphes synthétiques (`networkx`), pas des
données d'utilisateurs réels.

---

*Ce README a été généré à partir d'une lecture exhaustive du code source
des six notebooks du dossier — classes, docstrings, cellules exécutées et
sorties incluses — plutôt que d'un simple résumé des noms de fichiers.*
