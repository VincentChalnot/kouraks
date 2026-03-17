# J'aimerai qu'on fasse ensemble une liste de hardwares basée sur des données historiques pour qu'on définisse tous les hardwares disponibles dans la marketplace par "trimestre" (en gros : tiers d'évolution). On prend les hardwares historiques un peu reconnus / populaire de chaque époque, on transforme les noms et on définit le multiplicateur de puissance en se basant vaguement sur des données historiques de puissance.

Attention la mécanique des hardwares a un peu changé par rapport aux spécifications, on peut achèter et déployer
plusieurs hardwares en même temps et chaque service doit tourner sur un hardware précis.

Voilà la liste complète des 10 tiers de hardware pour Kouraks, calée sur des jalons historiques réels et transformée à
la sauce Kouraks. Avant la liste, un point sur la **mécanique révisée**  :[^1_1]

## Mécanique révisée

Dans le nouveau modèle, chaque service est assigné à une instance de hardware précise. La formule du yield projet
devient :

$$
\text{yield} = \text{baseYield} \times \min_i(\text{hw}_i.\text{mult} \times \text{service}_i.\text{yieldMult})
$$

Le `hardwareMultiplier` global disparaît — il est absorbé dans chaque service. La règle "maillon faible"  s'applique
maintenant **en cascade** : un service sur vieux hardware bottleneck tout le projet même si tous les autres sont sur du
récent. C'est parfait satiriquement — la "migration infra" devient une dépense massive par projet.[^1_1]

***

## Les 10 tiers — Marketplace Hardware

| \# | Nom Kouraks                                      | Inspiration réelle                                  | Époque | Coût/unité      | Multiplicateur |
|:---|:-------------------------------------------------|:----------------------------------------------------|:-------|:----------------|:---------------|
| 1  | **Conpac DeschPrau 486DX**                       | Compaq DeskPro 486DX2/66                            | 1994   | 0 K *(gratuit)* | ×1.0           |
| 2  | **PentioumPro Deux-Cent**                        | Intel Pentium Pro 200MHz workstation                | 1996   | 200 K           | ×1.7           |
| 3  | **Sonn SPARKztation Vingt**                      | Sun SPARCstation 20 (UltraSPARC)                    | 1999   | 800 K           | ×2.8           |
| 4  | **Dell PouarHedge Deux-Six-Cinq**                | Dell PowerEdge 2650 (Xeon 2.4GHz Prestonia)         | 2003   | 3 000 K         | ×4.5           |
| 5  | **H.P. ProLyant DéLée-TroisHuit**                | HP ProLiant DL380 G5 (Xeon 5160 Core 2)             | 2006   | 10 000 K        | ×7.5           |
| 6  | **Dell BladeauMille M-710**                      | Dell PowerEdge M710 Blade (Xeon X5570 Nehalem)      | 2009   | 35 000 K        | ×13.0          |
| 7  | **H.P. BL-QuatreZéro GenHuit**                   | HP ProLiant BL460c Gen8 (Xeon E5-2670 Sandy Bridge) | 2012   | 100 000 K       | ×21.0          |
| 8  | **Cisko UCS B-DeuxCent M.4**                     | Cisco UCS B200 M4 (Xeon E5-2680 v4 Broadwell)       | 2016   | 300 000 K       | ×34.0          |
| 9  | **Dell EMC PouarHedge Épique R-750**             | Dell PowerEdge R7515 (AMD EPYC 7702, 64 cores)      | 2019   | 900 000 K       | ×58.0          |
| 10 | **SuproMikro AS-Vingt-Quatrième Épique Ultreux** | Supermicro AS-2024US (AMD EPYC 7763 Milan)          | 2022   | 3 000 000 K     | ×95.0          |

***

## Descriptions sardoniques

- **Conpac DeschPrau** : *"Trouvée au fond d'un couloir. Le BIOS date de 1994. Personne n'ose la débrancher."*
- **PentioumPro Deux-Cent** : *"200 MHz. Coûtait un rein en 1996. La ventilation ressemble à un sèche-cheveux
  industriel."*
- **Sonn SPARKztation Vingt** : *"Unix de l'époque. 4 ingénieurs savent encore la configurer. Deux sont partis en
  retraite."*
- **Dell PouarHedge Deux-Six-Cinq** : *"Premier vrai rack 1U. La salle des serveurs est un placard. Le responsable
  l'appelle 'datacenter'."*
- **H.P. ProLyant DéLée-TroisHuit** : *"Le cheval de bataille du milieu des années 2000. Encore en prod dans 70% des DSI
  françaises."*
- **Dell BladeauMille M-710** : *"Blade. On a mis 16 serveurs dans un châssis 10U. La consommation électrique est
  désormais un problème RH."*
- **H.P. BL-QuatreZéro GenHuit** : *"Sandy Bridge. Le bond qualitatif qu'on attendait depuis 2004. Personne dans
  l'équipe ne peut expliquer pourquoi."*
- **Cisko UCS B-DeuxCent M.4** : *"Policy-driven. SDN-ready. 3 ingénieurs certifiés Cisco pour le configurer. Le ROI
  sera visible en 2031."*
- **Dell EMC PouarHedge Épique** : *"64 cores AMD. On pouvait avoir la même puissance moins cher. Mais ça n'avait pas le
  même logo."*
- **SuproMikro Épique Ultreux** : *"Le summum de l'on-premise. Acheté juste avant de tout migrer sur le cloud."*

***

## Config YAML prête à l'emploi

```yaml
hardware:
  - id: conpac-deschprau-486
    name: "Conpac DeschPrau 486DX"
    inspiration: "Compaq DeskPro 486DX2/66 (1994)"
    buyCost: 0
    multiplier: 1.0
    unlockAt: 0
    description: "Trouvée au fond d'un couloir. Le BIOS date de 1994. Personne n'ose la débrancher."

  - id: pentioum-pro-200
    name: "PentioumPro Deux-Cent"
    inspiration: "Intel Pentium Pro 200MHz (1996)"
    buyCost: 200
    multiplier: 1.7
    unlockAt: 200
    description: "200 MHz. Coûtait un rein en 1996. La ventilation ressemble à un sèche-cheveux industriel."

  - id: sonn-sparkztation-vingt
    name: "Sonn SPARKztation Vingt"
    inspiration: "Sun SPARCstation 20 (1999)"
    buyCost: 800
    multiplier: 2.8
    unlockAt: 1000
    description: "Unix de l'époque. 4 ingénieurs savent encore la configurer. Deux sont partis en retraite."

  - id: dell-pouarhedge-265
    name: "Dell PouarHedge Deux-Six-Cinq"
    inspiration: "Dell PowerEdge 2650 — Xeon 2.4GHz (2003)"
    buyCost: 3000
    multiplier: 4.5
    unlockAt: 5000
    description: "Premier vrai rack 1U. La salle des serveurs est un placard. Le responsable l'appelle 'datacenter'."

  - id: hp-prolyant-dl380
    name: "H.P. ProLyant DéLée-TroisHuit"
    inspiration: "HP ProLiant DL380 G5 — Xeon 5160 (2006)"
    buyCost: 10000
    multiplier: 7.5
    unlockAt: 20000
    description: "Le cheval de bataille du milieu des années 2000. Encore en prod dans 70% des DSI françaises."

  - id: dell-bladeau-m710
    name: "Dell BladeauMille M-710"
    inspiration: "Dell PowerEdge M710 Blade — Xeon X5570 (2009)"
    buyCost: 35000
    multiplier: 13.0
    unlockAt: 75000
    description: "Blade. On a mis 16 serveurs dans un châssis 10U. La consommation électrique est désormais un problème RH."

  - id: hp-bl460c-gen8
    name: "H.P. BL-QuatreZéro GenHuit"
    inspiration: "HP ProLiant BL460c Gen8 — Xeon E5-2670 (2012)"
    buyCost: 100000
    multiplier: 21.0
    unlockAt: 200000
    description: "Sandy Bridge. Le bond qualitatif qu'on attendait depuis 2004. Personne dans l'équipe ne peut expliquer pourquoi."

  - id: cisko-ucs-b200-m4
    name: "Cisko UCS B-DeuxCent M.4"
    inspiration: "Cisco UCS B200 M4 — Xeon E5-2680 v4 (2016)"
    buyCost: 300000
    multiplier: 34.0
    unlockAt: 600000
    description: "Policy-driven. SDN-ready. 3 ingénieurs certifiés Cisco pour le configurer. Le ROI sera visible en 2031."

  - id: dell-emc-epique-r750
    name: "Dell EMC PouarHedge Épique R-750"
    inspiration: "Dell PowerEdge R7515 — AMD EPYC 7702 (2019)"
    buyCost: 900000
    multiplier: 58.0
    unlockAt: 2000000
    description: "64 cores AMD. On pouvait avoir la même puissance moins cher. Mais ça n'avait pas le même logo."

  - id: supromikro-epique-ultreux
    name: "SuproMikro AS-Vingt-Quatrième Épique Ultreux"
    inspiration: "Supermicro AS-2024US — AMD EPYC 7763 (2022)"
    buyCost: 3000000
    multiplier: 95.0
    unlockAt: 7000000
    description: "Le summum de l'on-premise. Acheté juste avant de tout migrer sur le cloud."
```

***

## Points d'attention sur l'implémentation

Deux failles potentielles à anticiper avec la nouvelle mécanique :

1. **Coût UI** : afficher quel hardware est assigné à quel service devient critique — le joueur a potentiellement 10+
   instances à gérer. Un simple badge couleur par tier sur chaque service suffit, mais sans ça le jeu devient opaque
   rapidement.
2. **Orphelins hardware** : si un service est détruit ou réassigné, l'instance hardware ne doit pas disparaître — elle
   reste "libre" et réassignable. Il faut un état `assignedTo: serviceUid | null` sur chaque instance hardware, distinct
   de l'état service.
3. **Balance coût** : avec 8 services actifs en mid-game, passer tous à tier 5 coûte `8 × 10 000 = 80 000 K` — à
   comparer avec la phase 3 qui commence à ~5 000 K. Le ratio est à vérifier lors du playtest.
   <span style="display:none">[^1_10][^1_11][^1_12][^1_13][^1_14][^1_15][^1_16][^1_2][^1_3][^1_4][^1_5][^1_6][^1_7][^1_8][^1_9]</span>

<div align="center">⁂</div>

[^1_1]: 8a4f95e4.md

[^1_2]: http://www.vogons.org/viewtopic.php?t=28470\&start=280

[^1_3]: http://www.mrob.com/pub/comp/computer-history.html

[^1_4]: http://www.os2museum.com/wp/lies-damn-lies-and-wikipedia/

[^1_5]: https://www.tomshardware.com/reviews/benchmark-marathon,590-5.html

[^1_6]: https://www.vogons.org/viewtopic.php?t=28470

[^1_7]: https://www.servethehome.com/intel-releases-benchmark-comparison-to-amd-epyc-and-we-weigh-in/

[^1_8]: https://www.reddit.com/r/servers/comments/122f2jz/noteworthy_servers_throughout_the_90s_and_early/

[^1_9]: https://www.cpushack.com/2021/02/21/the-486-cpu-era-the-birth-of-overclocking-part-1/

[^1_10]: https://www.chpc.utah.edu/documentation/white_papers/rome.pdf

[^1_11]: https://en.wikipedia.org/wiki/Sun_Enterprise

[^1_12]: https://www.vogons.org/viewtopic.php?t=28470\&start=200

[^1_13]: https://www.reddit.com/r/Amd/comments/1gvwxna/8_vs_12_channel_ddr56000_memory_performance_with/

[^1_14]: https://www.webwerks.in/blogs/history-dedicated-server-cpus-till-today

[^1_15]: https://www.osnews.com/story/3997/analysis-x86-vs-ppc/

[^1_16]: http://ewams.net/specintd/?action=about


---

# Attends petite précision, il y a plusieurs autres choses qui ont changé dans les specs donc inutile d'essayer de sortir toutes les données finales par produit, on se concentre sur :

- Nom réel
- Nom satirique
- Facteur de puissance
  Et du coup ta tiers liste est parfaite mais maintenant il faut essayer de sortir plusieurs produits pour chaque tiers
  vu que le joueur va devoir choisir.
  En gros la règle c'est que pour chaque tiers il faut un mix de produits (à ajuster selon l'époque, pas obligé de
  mettre tous les types de produits pour chaque tiers, juste 3-4) :
- Un hardware d'entrée de gamme, potentiellement plus orienté consumer/prosumer
- Un hardware plus gaming : le désavantage de ce genre de matos se fera sur des critères dont on parlera plus tard.
- Un hardware flagship représentatif de l'époque (la liste que tu m'as sorti)
- Un hardware type serveur dédié en location qui aura un coût récurrent plutôt qu'un coût d'achat.
- Pareil pour un VPS
  Ensuite ce qu'on fera c'est qu'on ajustera le prix des vieux hardwares dans la marketplace pour continuer à les
  proposer aux tiers suivants

Parfait, on reste focus sur l'essentiel. Voici la liste complète, tier par tier, avec les 3-5 produits par génération
selon ce qui existait à l'époque. [^2_1]

Les types disponibles par tier évoluent avec l'histoire réelle : pas de VPS en 1994, pas de cloud en 2000, etc.

***

## Légende des types

| Type        | Description                                  |
|:------------|:---------------------------------------------|
| 🟤 Entry    | Consumer/prosumer — accessible, limité       |
| 🎮 Gaming   | Haute perf monocœur, désavantages à définir  |
| 🔵 Flagship | Serveur de référence de l'époque             |
| 🟠 Dédié    | Location à coût récurrent, hardware optimisé |
| ☁️ VPS      | Location virtualisée, overhead inclus        |

***

## Tier 1 — 1994, ère 486

| Type        | Nom réel                 | Nom satirique              | ×puissance |
|:------------|:-------------------------|:---------------------------|:-----------|
| 🟤 Entry    | Packard Bell 486SX/25    | **Pakard Bèle 486-Cesse**  | ×0.6       |
| 🔵 Flagship | Compaq DeskPro 486DX2/66 | **Conpac DeschPrau 486DX** | ×1.0       |

***

## Tier 2 — 1997, ère Pentium MMX

| Type        | Nom réel                                     | Nom satirique                                     | ×puissance |
|:------------|:---------------------------------------------|:--------------------------------------------------|:-----------|
| 🟤 Entry    | Intel Celeron 266MHz (Covington, sans cache) | **Céléreau Deux-Soixante-Six**                    | ×1.0       |
| 🎮 Gaming   | Pentium MMX 233MHz + 3Dfx Voodoo 2           | **Pentioum MMX Deux-Trente-Trois + Vouadou-Deux** | ×1.3       |
| 🔵 Flagship | Intel Pentium Pro 200MHz                     | **PentioumPro Deux-Cent**                         | ×1.7       |

***

## Tier 3 — 2000, ère PIII / Athlon

| Type        | Nom réel                               | Nom satirique                       | ×puissance |
|:------------|:---------------------------------------|:------------------------------------|:-----------|
| 🟤 Entry    | Intel Celeron 500MHz (Mendocino)       | **Céléreau Cinq-Cent Mendossino**   | ×1.6       |
| 🎮 Gaming   | AMD Athlon 800MHz + NVIDIA GeForce 256 | **Athlône Huit-Cent + GéForse 256** | ×2.1       |
| 🔵 Flagship | Sun SPARCstation 20 (UltraSPARC-II)    | **Sonn SPARKztation Vingt**         | ×2.8       |
| 🟠 Dédié    | Rackspace 1U PIII colocalisé           | **Rackspasse Dédié P-Trois**        | ×3.2       |

***

## Tier 4 — 2003, ère Pentium 4 / Xeon Prestonia

| Type        | Nom réel                                              | Nom satirique                                  | ×puissance |
|:------------|:------------------------------------------------------|:-----------------------------------------------|:-----------|
| 🟤 Entry    | Intel Celeron D 2.4GHz (Prescott-256)                 | **Céléreau D Deux-Virgule-Quatre**             | ×2.5       |
| 🎮 Gaming   | AMD Athlon 64 FX-51 (premier CPU 64-bit grand public) | **Athlône Soixante-Quatre FX-Cinquante-Et-Un** | ×3.5       |
| 🔵 Flagship | Dell PowerEdge 2650 (Xeon 2.4GHz dual)                | **Dell PouarHedge Deux-Six-Cinq**              | ×4.5       |
| 🟠 Dédié    | OVH Serveur Dédié 1U (era Xeon)                       | **OuvéHache Dédié Rack-Un-U**                  | ×5.2       |
| ☁️ VPS      | Virtuozzo VPS (premiers VPS commerciaux ~2003)        | **Virtuoze VPS Bassique**                      | ×3.0       |

***

## Tier 5 — 2006, ère Core 2 Duo

| Type        | Nom réel                                         | Nom satirique                                | ×puissance |
|:------------|:-------------------------------------------------|:---------------------------------------------|:-----------|
| 🟤 Entry    | Intel Core 2 Duo E4300 (1.8GHz, budget)          | **Kore-Deux E4-Troisième**                   | ×4.2       |
| 🎮 Gaming   | Intel Core 2 Duo E6600 + NVIDIA GeForce 8800 GTX | **Kore-Deux E6-Six-Cent + GéForse 8800 GTX** | ×5.8       |
| 🔵 Flagship | HP ProLiant DL380 G5 (Xeon 5160)                 | **H.P. ProLyant DéLée-TroisHuit G5**         | ×7.5       |
| 🟠 Dédié    | Hetzner EX6 (Core 2 Quad, lancé ~2007)           | **Hetzénaire EX-Six**                        | ×8.5       |
| ☁️ VPS      | Linode 360 (premier VPS SSD abordable)           | **Linn-Eau-De Nœud-360**                     | ×5.0       |

***

## Tier 6 — 2009, ère Nehalem / premier Cloud

| Type        | Nom réel                                         | Nom satirique                          | ×puissance |
|:------------|:-------------------------------------------------|:---------------------------------------|:-----------|
| 🟤 Entry    | Intel Core i5-750 (Lynnfield, premier i5)        | **Kore i5-Sept-Cinquante Linfield**    | ×7.5       |
| 🎮 Gaming   | Intel Core i7-920 (Bloomfield, roi de l'OC 2009) | **Kore i7-Neuf-Cent-Vingt Bloomfield** | ×10.0      |
| 🔵 Flagship | Dell PowerEdge M710 Blade (Xeon X5570 Nehalem)   | **Dell BladeauMille M-710**            | ×13.0      |
| 🟠 Dédié    | Hetzner EX8 (Xeon/i7 dédié)                      | **Hetzénaire EX-Huit**                 | ×15.0      |
| ☁️ VPS      | AWS EC2 m1.large (cloud grand public dès 2006)   | **Ausse EC2 em-Un-Large**              | ×8.5       |

***

## Tier 7 — 2012, ère Sandy Bridge

| Type        | Nom réel                                                 | Nom satirique                      | ×puissance |
|:------------|:---------------------------------------------------------|:-----------------------------------|:-----------|
| 🟤 Entry    | Intel Core i3-2120 (Sandy Bridge, budget)                | **Kore i3-Deux-Cent-Vingt Sandy**  | ×11.5      |
| 🎮 Gaming   | Intel Core i7-2600K (Sandy Bridge K, légende OC)         | **Kore i7-Deux-Mille-Six K Sandy** | ×16.0      |
| 🔵 Flagship | HP ProLiant BL460c Gen8 (Xeon E5-2670)                   | **H.P. BL-QuatreZéro GenHuit**     | ×21.0      |
| 🟠 Dédié    | Hetzner EX40 (très populaire, E3-1270)                   | **Hetzénaire EX-Quarante**         | ×24.0      |
| ☁️ VPS      | DigitalOcean Droplet SSD (lancé 2011, rupture du marché) | **DigitOcéane Gouttelette SSD**    | ×14.0      |

***

## Tier 8 — 2016, ère Skylake / Broadwell-EP

| Type        | Nom réel                                      | Nom satirique                         | ×puissance |
|:------------|:----------------------------------------------|:--------------------------------------|:-----------|
| 🟤 Entry    | Intel Core i5-6500 (Skylake)                  | **Kore i5-Six-Mille-Cinq Skylaque**   | ×19.0      |
| 🎮 Gaming   | Intel Core i7-6700K (Skylake K, 4GHz stock)   | **Kore i7-Six-Mille-Sept K Skylaque** | ×26.0      |
| 🔵 Flagship | Cisco UCS B200 M4 (Xeon E5-2680 v4 Broadwell) | **Cisko UCS B-DeuxCent M.4**          | ×34.0      |
| 🟠 Dédié    | OVH SYS SP-32 (dédié pro accessible)          | **OuvéHache SYS SP-TrenteDeux**       | ×39.0      |
| ☁️ VPS      | Scaleway C2 (cloud FR, lancé 2015)            | **Skalewé C2-Déluxe**                 | ×22.0      |

***

## Tier 9 — 2019, ère Zen 2 / EPYC Rome

| Type        | Nom réel                                                      | Nom satirique                        | ×puissance |
|:------------|:--------------------------------------------------------------|:-------------------------------------|:-----------|
| 🟤 Entry    | AMD Ryzen 5 3600 (meilleur rapport perf/prix de l'histoire)   | **Rizène 5 Trois-Mille-Six**         | ×32.0      |
| 🎮 Gaming   | Intel Core i9-9900K (roi du gaming 2018-2019, 5GHz boost)     | **Kore i9-Neuf-Mille-Neuf K**        | ×45.0      |
| 🔵 Flagship | Dell EMC PowerEdge R7515 (AMD EPYC 7702, 64 cores)            | **Dell EMC PouarHedge Épique R-750** | ×58.0      |
| 🟠 Dédié    | Hetzner AX101 (EPYC, lancé 2021, meilleur rapport dédié EPYC) | **Hetzénaire AX-Cent-Et-Un Épique**  | ×67.0      |
| ☁️ VPS      | AWS EC2 c5.2xlarge (Cascade Lake optimisé compute)            | **Ausse EC2 c-Cinq-DeuxXL**          | ×38.0      |

***

## Tier 10 — 2022, ère Alder Lake / EPYC Milan

| Type        | Nom réel                                                 | Nom satirique                                    | ×puissance |
|:------------|:---------------------------------------------------------|:-------------------------------------------------|:-----------|
| 🟤 Entry    | Intel Core i5-12400 (Alder Lake, value exceptionnelle)   | **Kore i5-DouzeMille-Quatre Auldeur**            | ×52.0      |
| 🎮 Gaming   | AMD Ryzen 7 5800X3D (3D V-Cache, roi gaming absolu 2022) | **Rizène 7 Cinq-Mille-Huit Triplé-Dé**           | ×73.0      |
| 🔵 Flagship | Supermicro AS-2024US (AMD EPYC 7763 Milan)               | **SuproMikro AS-Vingt-Quatrième Épique Ultreux** | ×95.0      |
| 🟠 Dédié    | Hetzner AX162R (EPYC 7702, 128 threads dédiés)           | **Hetzénaire AX-Cent-Soixante-Deux-R**           | ×108.0     |
| ☁️ VPS      | Hetzner Cloud CX41 (cloud FR/EU, excellent rapport)      | **Hetzénaire Kloud CX-Quarante-Et-Un**           | ×62.0      |

***

## Vue d'ensemble des multiplicateurs par type

| Tier | 🟤 Entry | 🎮 Gaming | 🔵 Flagship | 🟠 Dédié | ☁️ VPS |
|:-----|:---------|:----------|:------------|:---------|:-------|
| 1    | ×0.6     | —         | ×1.0        | —        | —      |
| 2    | ×1.0     | ×1.3      | ×1.7        | —        | —      |
| 3    | ×1.6     | ×2.1      | ×2.8        | ×3.2     | —      |
| 4    | ×2.5     | ×3.5      | ×4.5        | ×5.2     | ×3.0   |
| 5    | ×4.2     | ×5.8      | ×7.5        | ×8.5     | ×5.0   |
| 6    | ×7.5     | ×10.0     | ×13.0       | ×15.0    | ×8.5   |
| 7    | ×11.5    | ×16.0     | ×21.0       | ×24.0    | ×14.0  |
| 8    | ×19.0    | ×26.0     | ×34.0       | ×39.0    | ×22.0  |
| 9    | ×32.0    | ×45.0     | ×58.0       | ×67.0    | ×38.0  |
| 10   | ×52.0    | ×73.0     | ×95.0       | ×108.0   | ×62.0  |

La **logique des ratios** est cohérente : Dédié > Flagship > Gaming > VPS > Entry, avec un écart d'environ 15-20% entre
chaque type au sein d'un même tier. Le gaming est intentionnellement entre VPS et Flagship — bon pour le single-thread,
mais les désavantages (crashRate élevé ? consommation ? incompatibilité type de service ?) seront définis plus tard.

<div align="center">⁂</div>

[^2_1]: 8a4f95e4.md


---

# Est-ce qu'on a vraiment fait x100 en 30 ans sur les perfs ? J'arrive même pas à me rendre compte si c'est beaucoup ou pas...

Non, ×100 c'est une **massive sous-estimation**. Les chiffres réels sont bien plus fous. [^3_1][^3_2]

## Ce que disent les données

Le taux d'amélioration des CPU a varié par période [^3_2] :

- **1994→2003** : +52%/an → ×43 en 9 ans (âge d'or du scaling clock-speed)
- **2003→2011** : +23%/an → ×5.2 supplémentaires (fin de la course aux GHz)
- **2011→2022** : +7%/an → ×2.1 supplémentaires (post-Dennard scaling, le mur thermique)

Ce qui donne **×478 en single-thread** sur 28 ans. Et c'est sans compter les cœurs.

## Le vrai chiffre

| Métrique                                   | 486 DX2/66 (1994) | EPYC 7763 (2022)   | Ratio       |
|:-------------------------------------------|:------------------|:-------------------|:------------|
| Passmark single-thread                     | ~20               | ~3 200             | **×160**    |
| Passmark multi-thread                      | ~20 (1 core)      | ~52 000 (64 cores) | **×2 600**  |
| Throughput théorique (Moore's Law × cores) | baseline          | —                  | **×30 000** |

Un benchmark réel confirme d'ailleurs que l'EPYC 7763 dépasse un Athlon 64 X2 de *2005* de **+11 388%** [^3_3] — et le
486 de 1994 est bien en dessous de ça.

## Pourquoi ×95 reste correct pour le jeu

Notre échelle ×1→×95 couvre environ **60% du gain single-thread réel** — ce qui est honnête, parce que les workloads
simulés (un service web, une DB) ne scalent pas linéairement avec 64 cœurs. [^3_2] En pratique, un service applicatif
moyen bénéficie surtout du gain single-thread + 2-4 cœurs max.

Ce qui est vraiment drôle sur le plan satirique : **on sous-estime la réalité de ×27 à ×316 selon la métrique**. Le
joueur pense qu'il gère une infrastructure sérieuse en passant de ×1 à ×95... alors que la vraie industrie a fait ×2 600
dans le même temps, et continue à réinventer la complexité pour en consommer l'intégralité.

*"C'était mieux avant" — mais objectivement non, le matos est 2 600 fois plus rapide qu'en 1994.*
<span style="display:none">[^3_10][^3_11][^3_12][^3_13][^3_14][^3_15][^3_4][^3_5][^3_6][^3_7][^3_8][^3_9]</span>

<div align="center">⁂</div>

[^3_1]: https://en.wikipedia.org/wiki/I486

[^3_2]: https://en.wikipedia.org/wiki/Moore's_law

[^3_3]: https://technical.city/en/cpu/Athlon-64-X2-4200-plus-vs-EPYC-7763

[^3_4]: https://www.cpubenchmark.net/cpu.php?cpu=AMD+EPYC+7763\&id=4207

[^3_5]: https://valid.x86.fr/bench/n6rkgj

[^3_6]: https://www.cpu-monkey.com/fr/cpu-amd_epyc_7763

[^3_7]: https://www.cpubenchmark.net/compare/4207vs3618/AMD-EPYC-7763-vs-AMD-EPYC-7H12

[^3_8]: https://pc-builds.com/compare/cpu/02415R/athlon-ii-x2-215/epyc-7763

[^3_9]: https://umatechnology.org/moores-law-cpu-speed/

[^3_10]: https://technical.city/en/cpu/EPYC-7302P-vs-EPYC-7763

[^3_11]: https://www.youtube.com/watch?v=1Rj1B4M6yXM

[^3_12]: https://www.reddit.com/r/dataisbeautiful/comments/cynql1/moores_law_graphed_vs_real_cpus_gpus_1965_2019_oc/

[^3_13]: https://www.reddit.com/r/vintagecomputing/comments/tuxn92/what_would_be_a_modernday_486_equivalent_in_terms/

[^3_14]: https://versus.com/en/amd-epyc-4344p-vs-amd-epyc-7763

[^3_15]: https://ourworldindata.org/moores-law


---

# Alors on va discuter du point suivant : les hardwares ont deux autres propriétés hyper importantes :

- Leur coût récurrent qui pour le cas des serveurs achetés représentént leur consommation électrique (fixe/s, ça serait
  imbittable niveau UX si ça scalait avec la charge)
- Leur rendement max en K/s : si les services qui tiennent dessus produisent trop de K/s on scale down toute la
  production du serveur pour ne pas dépasser ce montant.
  Du coup ça répond un peu à la problématique des benchmarks mono-coeurs, je pense qu'on peut matcher le multiplicateur
  réel et après il faut que tout soit scale en fonction de ça.
  Du coup les serveurs produisent beaucoup plus de K/s en évoluant mais d'un autre côté le nombre de services qu'on peut
  faire tourner dessus reste plus on moins le même puisque tout scale avec ! Les services produisent plus de K/s mais
  les projets demandent encore plus de K/s.
  L'impératif de productivité explose a peu près autant que le multiplicateur de puissance.

Answer skipped.

---

# Alors on va discuter du point suivant : les hardwares ont deux autres propriétés hyper importantes :

- Leur coût récurrent qui pour le cas des serveurs achetés représentént leur consommation électrique (fixe/s, ça serait
  imbittable niveau UX si ça scalait avec la charge)
- Leur rendement max en K/s : si les services qui tiennent dessus produisent trop de K/s on scale down toute la
  production du serveur pour ne pas dépasser ce montant.
  Du coup ça répond un peu à la problématique des benchmarks mono-coeurs, je pense qu'on peut matcher le multiplicateur
  réel et après il faut que tout soit scale en fonction de ça.
  Du coup les serveurs produisent beaucoup plus de K/s en évoluant mais d'un autre côté le nombre de services qu'on peut
  faire tourner dessus reste plus on moins le même puisque tout scale avec ! Les services produisent plus de K/s mais
  les projets demandent encore plus de K/s.
  L'impératif de productivité explose a peu près autant que le multiplicateur de puissance et le fait que les stacks
  techniques demandent de plus en plus de services qui produisent/consomment de plus en plus font qu'au final on ne fait
  pas tourner beaucoup plus de projets par hardware.

Ton insight est correct et élégant. Mais avant de valider les valeurs, creusons la mécanique — il y a une implication
formulaire importante.

## La nouvelle formule

Avec `maxKps`, le `hardwareMultiplier` n'est plus global — il devient **local à chaque couple service/hardware**. Le cap
s'applique AVANT le `min()` :

```javascript
function computeLeafYield(leaf) {
    const assigned = services.filter(s => s.assignedTo === leaf.id && s.hardware);
    if (!allTypesSatisfied(assigned, leaf.requires)) return 0;

    const effectiveMults = assigned.map(s => {
        const raw = s.hardware.multiplier * s.yieldMultiplier;
        // Le cap convertit maxKps en multiplicateur effectif comparable
        return Math.min(raw, s.hardware.maxKps / leaf.baseYield);
    });

    return leaf.baseYield * Math.min(...effectiveMults);
}

// Chaque seconde, drain électricité sur tous les hardware déployés
game.kouraks -= deployedHardware.reduce((sum, hw) => sum + hw.runCostPerSec, 0);
```

La ligne clé : `Math.min(raw, hw.maxKps / leaf.baseYield)`. Elle convertit le cap absolu en multiplicateur relatif au
projet — ce qui le rend comparable au `hardware.multiplier` dans le `min()`.

***

## Ce que ça change sur le multiplicateur

**Hypothèse implicite à tester** : ton raisonnement sur le "même nombre de services par hardware" suppose que `maxKps`
scale à peu près comme `multiplier × baseYield_moyen`. Vérifions :

| Si baseYield projet | Sur Tier 1 (×1.0, maxKps=30) | Sur Tier 5 (×7.5, maxKps=300)  |
|:--------------------|:-----------------------------|:-------------------------------|
| 10 K/s (early)      | ×1.0, cap à 30 → **OK**      | ×7.5, cap à 300 → **OK**       |
| 50 K/s (mid)        | ×0.6 **throttlé**            | ×6.0 (80%) légèrement throttlé |
| 200 K/s (late)      | ×0.15 **étranglé**           | ×1.5 **throttlé**              |

Le cap crée une **pression à upgrader** sans être binaire. C'est exactement le bon comportement.

Et ça répond à ta question sur les benchmarks : **on peut maintenant utiliser le vrai ×160** au Tier 10. Le cap empêche
qu'un joueur abuse d'un matériel haut de gamme sur des projets cheap. Les multiplicateurs peuvent matcher la réalité.

***

## Valeurs proposées par tier

Les valeurs absolues dépendent de la balance finale, mais voici les **ratios structurants** :

| Tier | Mult | maxKps    | runCost/s | Ratio maxKps/mult | Ratio cost/prod* |
|:-----|:-----|:----------|:----------|:------------------|:-----------------|
| 1    | ×1.0 | 12 K/s    | 0.02 K/s  | 12                | ~2%              |
| 2    | ×1.7 | 22 K/s    | 0.05 K/s  | 13                | ~3%              |
| 3    | ×2.8 | 40 K/s    | 0.12 K/s  | 14                | ~4%              |
| 4    | ×4.5 | 70 K/s    | 0.3 K/s   | 15                | ~5%              |
| 5    | ×7.5 | 130 K/s   | 0.8 K/s   | 17                | ~6%              |
| 6    | ×13  | 250 K/s   | 2 K/s     | 19                | ~7%              |
| 7    | ×21  | 450 K/s   | 5 K/s     | 21                | ~7%              |
| 8    | ×34  | 800 K/s   | 12 K/s    | 23                | ~8%              |
| 9    | ×58  | 1 500 K/s | 28 K/s    | 26                | ~8%              |
| 10   | ×160 | 5 000 K/s | 80 K/s    | 31                | ~9%              |

*ratio cost/prod = `runCostPerSec / (mult × baseYield_moyen_de_10 K/s)`

Le **ratio maxKps/mult augmente** légèrement : les machines récentes sont plus efficaces (meilleure perf/watt, NVMe,
mémoire rapide). Le **ratio cost/prod augmente** aussi : en endgame, l'électricité grignote 8-9% par hardware déployé,
et avec 20 unités ça fait un drain réel.

***

## Modifieurs par type de hardware

| Type                | maxKps                       | runCostPerSec            | upfrontCost |
|:--------------------|:-----------------------------|:-------------------------|:------------|
| 🔵 Flagship (owned) | ×1.0                         | ×1.0 (élec)              | ×1.0        |
| 🟤 Entry (owned)    | ×0.7                         | ×0.6 (moins d'élec)      | ×0.4        |
| 🎮 Gaming (owned)   | ×0.8                         | ×1.3 (chaud, inefficace) | ×0.7        |
| 🟠 Dédié (loué)     | ×0.85                        | ×1.5 (abonnement)        | ×0          |
| ☁️ VPS (loué)       | ×0.55 (overhead hyperviseur) | ×2.0 (cloud premium)     | ×0          |

Le **gaming a plus d'électricité que ses perfs** — son désavantage est là, pas besoin d'une mécanique spéciale. Le **VPS
a le pire maxKps** (virtualisation = overhead), ce qui se traduit directement en pénalité de yield sur les projets
exigeants.

***

## Le piège à éviter

**Hypothèse implicite dans ton design** : "les projets demandent de plus en plus de K/s" implique que `leaf.baseYield`
doit scaler entre les tiers. Si le `baseYield` reste flat (tous les projets à 10-15 K/s), le cap ne presse jamais
vraiment le joueur à upgrader son hardware — le multiplicateur seul suffit. Il faut que les projets de Tier 7+ aient des
`baseYield` de 100-300 K/s pour que le `maxKps` d'un Tier 1 les étrangle véritablement.

---

# De toutes façons on va partir de ce multiplicateur hardware pour scale tout le reste :

Tiers 1 on est a x1, il faut pouvoir faire tourner tous les projets avec les services de base et on fera un calcul pour
vérifier que la production de Kouraks sur le trimestre permette de facilement passer au tiers 2 avec de la marge.
On fait ça pour chaque tiers et on est bon.
De toutes façons on a un objectif claire de production par projet par trimestre donc à partir de là on peut en déduire
tout le reste : le coût et la production de chaque service ou hardware.
Une fois qu'on aura un truc qui tourne on ajustera la difficulté avec la target production des projets.
Ça reste une équation à mille paramètres qu'il faut bien équilibrer pour rendre le jeu intéressant mais je pense qu'on a
une bonne marge de manœuvre avant que le jeu devienne chiant.

L'approche est solide — c'est exactement la méthode top-down utilisée dans les idle games qui tiennent leur balance.
Mais il y a **un paramètre caché** dans l'équation de progression.

## L'équation de base

```
temps_pour_passer_au_tier_N+1 = coût_total_tier_N+1 / K/s_nets_au_tier_N
```

Avec `K/s_nets = K/s_bruts - runCosts_cumulés`. C'est ce deuxième terme qui change tout en endgame : à tier 10 avec 20
hardwares déployés, le drain électrique peut représenter 30-40% de la prod brute. Si tu oublies ce terme dans le calcul
de balance, les tiers tardifs deviennent exponentiellement plus longs que prévu.

## Les 3 paramètres à fixer en premier

Tout le reste en découle :

| Paramètre | Description                                       | Suggestion                      |
|:----------|:--------------------------------------------------|:--------------------------------|
| `T(n)`    | Temps cible pour progresser du tier N au tier N+1 | 8 min (T1→T2) → 25 min (T9→T10) |
| `P(n)`    | Nombre de projets actifs au tier N                | 1 → 6 progressif                |
| `S(n)`    | Nombre de services par projet au tier N           | 2 → 4 progressif                |

À partir de là, pour chaque tier :

```
coût_total_upgrade(N+1)  = prix_hardware_tier_N+1 × P(N) × S(N)
K/s_bruts_requis(N)      = coût_total_upgrade(N+1) / T(N) + runCosts(N)
baseYield_projet(N)      = K/s_bruts_requis(N) / P(N) / multiplier(N)
```

Et `baseYield_projet(N)` te donne directement l'ancrage pour scaler tous les projets de ce tier.

## Le seul vrai risque

Le jeu a une **équation non-linéaire** à deux endroits :

1. **`P(n) × S(n)` grandit** → le coût d'upgrade n'est pas juste `prix_hw × 1`, il est multiplié par tous les services
   actifs. Un joueur en tier 6 avec 4 projets × 3 services doit acheter **12 unités** de tier 7. C'est le moment où la
   satire devient viscérale — et où le balance peut dérailler si le `T(n)` cible n'est pas ajusté en conséquence.
2. **`runCosts` compound** → chaque nouveau service/hardware ajoute un drain permanent. En endgame, le joueur qui "
   sur-scale" son infra se retrouve à brûler ses Kouraks plus vite qu'il n'en produit. Mécaniquement ça peut être drôle,
   satiriquement c'est parfait, mais il faut que ce soit *possible* à rattraper.

## Prochaine étape concrète

Il suffit de **fixer la courbe `T(n)`** — tout le reste se calcule. Quelque chose comme :

| Tiers  | Temps cible |
|:-------|:------------|
| 1 → 2  | 5 min       |
| 2 → 3  | 8 min       |
| 3 → 4  | 12 min      |
| 4 → 5  | 18 min      |
| 5 → 6  | 25 min      |
| 6 → 7  | 35 min      |
| 7 → 8  | 50 min      |
| 8 → 9  | 70 min      |
| 9 → 10 | 90 min      |

Soit ~6h30 de jeu total pour atteindre l'endgame — ce qui est une session longue mais pas démesurée pour un idle. Une
fois cette courbe validée, on peut générer automatiquement tous les `baseYield`, `buyCost` et `runCost` par tier avec un
simple script.

Tu veux qu'on code ce générateur de balance maintenant ?

---

# je me disais qu'on pourrait avoir une mécanique pour rattraper les erreurs : si à un moment le joueur arrive à 0K on reçoit un mail incendiaire du PDG qui nous insulte parce qu'on n'a pas réussi à tenir le budget.

Ça déclenche un truc pervers qui est qu'on peut emprunter des Kouraks sur le marché via un service : le service a un
coût de déploiement négatif donc pour que le joueur récupère une grande quantité de Kouraks d'un coup, par contre après
on a des intérêts à payer en coût récurrent.
C'est one shot et si le joueur revient à 0K après ça c'est game over.
De toutes façons l'idée c'est que ça reste un peu difficile quand même, ça augmente un peu la durée de vie du jeu.

La mécanique est bonne, mais j'ai **une réserve** à formuler avant d'aller plus loin.

## Ce qui fonctionne très bien

Le service à coût négatif est **élégant** — pas de système de dette séparé, juste un service comme les autres avec
`buyCost: -50000` et `runCostPerSec: positif`. Il s'intègre dans l'existant sans une ligne de code supplémentaire. Le
mail du PDG est parfaitement dans le ton satirique. [^7_1]

## Je maintiens une réserve sur le game over

Le game over "revenir à 0 après le prêt" crée un problème de **cliff asymétrique** : le joueur qui gère 12 services avec
des runCosts importants peut passer de +500 K/s à -50 K/s en quelques crashes simultanés. La dette absorbe le choc une
fois, mais le deuxième passage à zéro peut arriver en 30 secondes plutôt qu'en 30 minutes — le game over est alors
frustrant, pas mérité.

La question c'est : est-ce que le game over est là pour **punir une mauvaise gestion structurelle** (belle mort) ou pour
**punir un crash de malchance** (mort frustrante) ? Les deux peuvent arriver dans le même run.

## Alternative qui préserve le propos satirique

Au lieu d'un game over hard, un **debt spiral** :

```
0 K (premier passage)  → mail PDG insulte #1 + prêt déblocable
0 K (second passage)   → mail PDG insulte #2 + consultant arrive
                          → le consultant "aide" en supprimant 
                            aléatoirement 2 services pour "optimiser"
0 K (troisième passage) → game over + message final :
                          "Le projet a été externalisé à une ESN."
```

Ça donne **deux filets de sécurité** au lieu d'un, et chaque étape amplifie la satire. Le consultant qui supprime des
services pour "couper les coûts" est exactement le genre d'ironie que le jeu cherche. [^7_1]

## Structure du service de prêt

Dans tous les cas, voici comment ça se modélise proprement :

```yaml
- id: pret-marche-kourakal
  name: "Prêt MarchéKourakal Express"
  serviceType: financial   # nouveau type, pas assignable à un projet
  buyCost: -80000          # injecte 80 000 K immédiatement
  runCostPerSec: 15        # intérêts perpétuels ~1300 K/jour de jeu
  unlockAt: -1             # jamais visible en marketplace normale
  unlockedByEvent: "zero_kouraks"
  maxInstances: 1          # one-shot
  description: "Le marché vous fait confiance. Pour l'instant."
```

Le `serviceType: financial` ne se déploie sur aucun hardware — il échappe à la règle "chaque service tourne sur un
hardware". C'est d'ailleurs le seul service avec cette exception, ce qui le rend lisible dans le code. [^7_1]

Le taux d'intérêt de 15 K/s est calibré pour que le joueur **sente** la pression sans que ce soit immédiatement fatal —
à tier 5 c'est ~5% du drain total, à tier 3 c'est ~20%. Plus on emprunte tôt, plus c'est douloureux.

<div align="center">⁂</div>

[^7_1]: 8a4f95e4.md


---

# Alors pour aller plus loin dans la réflexion, je pense qu'il va il y avoir plusieurs mécaniques pour éviter un crash majeur qui vont apparaître lors de la progression :

- Les services deviennent plus stable avec le temps
- Certains services vont spécifiquement permettre de baisser le taux d'erreur par projet / globalement
- Certains services permettront de redémarrer automatiquement les services en erreur
  Donc à moins de vraiment prendre plein de décision dans le sens inverse, un joueur qui se retrouve sous pression pour
  stabiliser sa stack aura leviers visibles pour agir.
  Et sinon pendant que j'y pense, on peut élargir la notion de prêt / investissement (service opposé : coût d'achat
  élevé mais un rendement continu de K/s) et proposer ça à tous les joueurs à partir d'un certain tiers.
  Si on tri par défaut les services dans la marketplace du moins cher au plus cher le service de prêt va être
  naturellement tout en haut de la liste.

Tout ça s'articule bien. Prenons les deux sujets séparément.

## Mécanique de stabilité — la courbe de sérénité

Les trois leviers forment une progression naturelle qui correspond à l'évolution réelle des pratiques DevOps :

| Tier  | Levier                           | Exemple service satirique            | Effet                                          |
|:------|:---------------------------------|:-------------------------------------|:-----------------------------------------------|
| T2-T3 | Services intrinsèquement stables | `MoïSQL Pro` vs `MoïSQL 3.0`         | `crashRate` plus bas à l'achat                 |
| T4-T5 | Monitoring / observabilité       | `Prométhéos`, `Grapphane`            | Réduit `crashRate` globalement ou par projet   |
| T6-T7 | Auto-restart / watchdog          | `Kuzubernètes Lite`, `SuperviseurDX` | `restartDuration: 0` sur les services assignés |

L'équilibre critique : les services de monitoring réduisent le taux de crash **mais ne l'éliminent pas**. Ils tournent
eux-mêmes sur du hardware, consomment des ressources, et peuvent eux-mêmes crasher — ce qui est exactement ce qui se
passe en prod réelle. Un `Prométhéos` qui crash pendant un incident, c'est du lore qui se joue tout seul. [^8_1]

**Une faille à anticiper** : si `Kuzubernètes` auto-restart tous les services, le joueur ne surveille plus rien. Le jeu
perd sa tension. La solution : l'auto-restart a un `restartDuration` divisé par 2 plutôt que zéro, et ne fonctionne pas
si le service de watchdog lui-même est en état `degraded`.

***

## Services financiers — l'écosystème complet

Ton idée d'élargir à l'investissement crée une belle symétrie :

```
Prêt        : buyCost négatif  → runCost positif  (tu reçois maintenant, tu paies pour toujours)
Investissement : buyCost positif → runCost négatif  (tu paies maintenant, tu reçois pour toujours)
```

Les deux sont des `serviceType: financial`, sans hardware requis, hors du calcul de yield des projets.

```yaml
- id: pret-kourakal-express
  name: "Prêt KouraKal Express"
  serviceType: financial
  buyCost: -80000       # reçois 80K immédiatement
  runCostPerSec: 12     # intérêts perpétuels
  unlockAt: -1          # déclenché par event
  maxInstances: 1
  description: "Le marché vous fait confiance. Pour l'instant."

- id: obligations-kourakalistes
  name: "Obligations KouraKalistes 6.5%"
  serviceType: financial
  buyCost: 50000        # investis 50K
  runCostPerSec: -8     # rendement passif ~0.7K/s net
  unlockAt: 500000      # mid-game seulement
  maxInstances: 3       # limité pour ne pas trivialiser le jeu
  description: "Rendement garanti. Le prospectus mentionne 47 pages de risques."
```

**Le ROI de l'obligation** : 50 000 K / 8 K/s = breakeven en ~6 250s (~1h45). C'est long, ça récompense la planification
sans court-circuiter la production réelle.

***

## L'insight UX sur le tri — à double tranchant

Le prêt qui remonte naturellement en haut de liste par prix négatif est satiriquement parfait. Mais il y a un risque UX
concret : **un joueur débutant qui ne lit pas la description voit "−80 000 K" et pense que c'est une réduction de prix
**, pas un crédit. Il clique, reçoit 80K, et ne comprend pas pourquoi ses Kouraks baissent chaque seconde.

Deux options pour garder la satire sans piéger les nouveaux :

- **Option A** : Le prêt n'apparaît dans la marketplace qu'après le premier passage à 0 (ton idée originale). Le tri
  n'est pas le vecteur de découverte — l'événement l'est.
- **Option B** : Il est visible dès T3-T4, mais la description est explicitement prédatrice : *"Recevez 80 000 K
  maintenant. 12 K/s de frais. Pour toujours."* — le joueur est averti, et s'il clique quand même c'est son problème.
  C'est d'ailleurs exactement comment fonctionnent les vraies offres de crédit revolving.

L'option B est plus cohérente avec la philosophie du jeu : **le jeu ne te protège pas de toi-même**. [^8_1]

<div align="center">⁂</div>

[^8_1]: 8a4f95e4.md


---

# ok maintenant que tu as une bonne vision des mécaniques du jeu et des derniers ajustements sur les specs, est-ce qu'on peut passer aux services : même exercices que pour les hardwares mais en plus compliqué parce qu'il faut trouver les stacks typiques par époque avec pour chaque stack une variété de services différents qui correspondraient soit à une réalité historique soit à une mécanique de jeu qu'on veut pousser. À noter qu'on peut étendre la notion de services à des choses très éloignées de la notion de logiciel comme on l'a vu pour les prêts et investissements. Il faut faire en fonction des trends de chaque époque.

D'ailleurs juste pour info, les services ont déjà un flag requireHardware pour gérer tout ce qui est SaaS.

Avant la liste, il faut établir la **taxonomie des types de services** — c'est la décision de design la plus
structurante, parce que les `requires` des projets en découlent directement. [^9_1]

## Taxonomie des types

| Catégorie     | Types                                                                   | Rôle mécanique                                             |
|:--------------|:------------------------------------------------------------------------|:-----------------------------------------------------------|
| **Prod**      | `backend`, `database`, `cache`, `message-queue`, `search`, `storage`    | Contribuent au yield du projet                             |
| **Infra**     | `reverse-proxy`, `monitoring`, `orchestration`, `service-mesh`, `ci-cd` | Réduisent crashRate / restartDuration, pas de yield direct |
| **SaaS**      | `cdn`, `managed-db`, `serverless`                                       | `requireHardware: false`, runCost uniquement               |
| **Financial** | `financial`                                                             | `requireHardware: false`, buyCost/runCost inversés         |

Les types **Infra** sont optionnels pour les projets — ils ne sont dans aucun `requires`, mais leur absence se fait
sentir en crashRate. Le joueur les achète par douleur, pas par obligation. [^9_1]

***

## Tier 1 — 1994 | Web statique / CGI

*Stack type : NCSA HTTPd + MySQL + Perl CGI. Tout tourne sur du hardware owned, rien de SaaS n'existe encore.*

| Nom réel                  | Nom Kouraks              | Type            | reqHW |
|:--------------------------|:-------------------------|:----------------|:------|
| Perl CGI                  | **GRAs.pl**              | `backend`       | ✅     |
| NCSA HTTPd / Apache 0.6   | **Apacheux HTTPdi Zéro** | `reverse-proxy` | ✅     |
| MySQL 1.0                 | **MoïSQL 1.0**           | `database`      | ✅     |
| WU-FTPd (déploiement FTP) | **FaTéPé Workerot**      | `storage`       | ✅     |

***

## Tier 2 — 1997 | LAMP naissant

*Stack type : Apache + PHP 3 + MySQL. Premier vrai langage web "grand public".*

| Nom réel      | Nom Kouraks              | Type            | reqHW |
|:--------------|:-------------------------|:----------------|:------|
| PHP 3         | **PHP Troizième**        | `backend`       | ✅     |
| Apache 1.3    | **Apacheux 1.3 LTS**     | `reverse-proxy` | ✅     |
| MySQL 3.23    | **MoïSQL 3.0 Community** | `database`      | ✅     |
| Cold Fusion 3 | **FroïdFusion III**      | `backend`       | ✅     |

***

## Tier 3 — 2000 | Bulle dot-com / J2EE

*Stack type : Tomcat + Java + Oracle. L'ère où "Enterprise" justifiait tout. Premier SaaS (Akamai, 1999).*

| Nom réel   | Nom Kouraks             | Type         | reqHW |
|:-----------|:------------------------|:-------------|:------|
| Tomcat 3.0 | **TomKatt 3.0**         | `backend`    | ✅     |
| JBoss 2.0  | **JeuxBoss 2.0**        | `backend`    | ✅     |
| Oracle 8i  | **OraKleur 8i**         | `database`   | ✅     |
| Nagios 1.0 | **Nageois Alfa**        | `monitoring` | ✅     |
| Akamai CDN | **AkaMaï CDN Prestige** | `cdn`        | ❌     |

***

## Tier 4 — 2003 | PHP5 / Memcached

*Stack type : PHP 5 + MySQL + Memcached + Nagios. L'ère du cache comme solution à tout.*

| Nom réel                   | Nom Kouraks                        | Type            | reqHW |
|:---------------------------|:-----------------------------------|:----------------|:------|
| PHP 5                      | **PHP Cinq Community**             | `backend`       | ✅     |
| Memcached 1.0              | **MemCacheux 1.0**                 | `cache`         | ✅     |
| nginx 0.1                  | **N-Ginx Zéro-Un**                 | `reverse-proxy` | ✅     |
| MySQL 4.1                  | **MoïSQL 4.1 InnoDB**              | `database`      | ✅     |
| Nagios 2.0                 | **Nageois 2.0**                    | `monitoring`    | ✅     |
| *(premier prêt)*           | **Prêt KouraKal Express**          | `financial`     | ❌     |
| *(premier investissement)* | **Obligations KouraKalistes 6.5%** | `financial`     | ❌     |

***

## Tier 5 — 2006 | Web 2.0 / Ruby on Rails

*Stack type : Rails + PostgreSQL + Memcached + RabbitMQ. L'ère "convention over configuration" et des premiers message
queues open-source.*

| Nom réel          | Nom Kouraks               | Type            | reqHW |
|:------------------|:--------------------------|:----------------|:------|
| Ruby on Rails 1.2 | **Railzôt Framework**     | `backend`       | ✅     |
| Django 0.95       | **Diango Zéro-Neuf-Cinq** | `backend`       | ✅     |
| PostgreSQL 8.1    | **PostGrès 8.1**          | `database`      | ✅     |
| RabbitMQ 1.0      | **LapinMQ 1.0**           | `message-queue` | ✅     |
| Munin             | **Mougnin Agent**         | `monitoring`    | ✅     |
| Lighttpd          | **LighTéPéDé**            | `reverse-proxy` | ✅     |

***

## Tier 6 — 2009 | Node.js / NoSQL / premier Cloud

*Stack type : Node.js + MongoDB + Redis + RabbitMQ. L'ère "schemaless" et de l'event-loop. AWS S3 change la notion de
stockage.*

| Nom réel       | Nom Kouraks            | Type            | reqHW |
|:---------------|:-----------------------|:----------------|:------|
| Node.js 0.1    | **Nœud.js Zéro-Un**    | `backend`       | ✅     |
| MongoDB 1.0    | **MongueBD 1.0**       | `database`      | ✅     |
| Redis 1.0      | **Rédiss 1.0**         | `cache`         | ✅     |
| RabbitMQ 2.0   | **LapinMQ 2.0 Broker** | `message-queue` | ✅     |
| AWS S3         | **Ausse S3-Eau**       | `storage`       | ❌     |
| Graphite 0.9   | **Graphiteux 0.9**     | `monitoring`    | ✅     |
| Cloudflare 1.0 | **KloudFlair Basic**   | `cdn`           | ❌     |

***

## Tier 7 — 2012 | Big Data / Kafka / Docker

*Stack type : Java/Scala + Cassandra + Kafka + Elasticsearch. L'ère où "Big Data" justifiait tout (à la place de "
Enterprise").*

| Nom réel             | Nom Kouraks              | Type            | reqHW |
|:---------------------|:-------------------------|:----------------|:------|
| Docker 0.9           | **Docqueur Zéro-Neuf**   | `container`     | ✅     |
| Kafka 0.8            | **KafQuoi 0.8**          | `message-queue` | ✅     |
| Elasticsearch 1.0    | **ElasticRechèrche 1.0** | `search`        | ✅     |
| Cassandra 1.2        | **KassandraBD**          | `database`      | ✅     |
| ELK Stack (Logstash) | **ELKasse Stack**        | `monitoring`    | ✅     |
| HAProxy 1.5          | **HaïProxi 1.5**         | `reverse-proxy` | ✅     |
| AWS Lambda (proto)   | **Lambdeau Fonktion**    | `serverless`    | ❌     |

***

## Tier 8 — 2016 | Kubernetes / Prometheus / DevOps

*Stack type : Microservices + K8s + Prometheus/Grafana. L'ère où "microservices" justifiait tout (à la place de "Big
Data").*

| Nom réel             | Nom Kouraks                | Type            | reqHW |
|:---------------------|:---------------------------|:----------------|:------|
| Kubernetes 1.2       | **Kuzubernètes 1.2**       | `orchestration` | ✅     |
| Prometheus + Grafana | **Prométhéos + Grapphane** | `monitoring`    | ✅     |
| Redis Cluster        | **Rédiss Kluster**         | `cache`         | ✅     |
| Istio 0.2            | **Istiaux Service Mesh**   | `service-mesh`  | ✅     |
| Jenkins / GitLab CI  | **Djenkines Pipeline**     | `ci-cd`         | ✅     |
| Datadog SaaS         | **DataDogue Lite**         | `monitoring`    | ❌     |
| AWS DynamoDB         | **DinahmoBD**              | `managed-db`    | ❌     |

***

## Tier 9 — 2019 | GitOps / Serverless / Managed Everything

*Stack type : tout managed + ArgoCD + Terraform. L'ère où "serverless" justifiait tout (à la place de "microservices").*

| Nom réel              | Nom Kouraks                | Type            | reqHW |
|:----------------------|:---------------------------|:----------------|:------|
| ArgoCD 1.0            | **ArgueCéDé GitOpse**      | `ci-cd`         | ✅     |
| Terraform / Pulumi    | **TerraForme IaC**         | `ci-cd`         | ✅     |
| Confluent Kafka Cloud | **KafQuoiCloud Managed**   | `message-queue` | ❌     |
| Datadog Enterprise    | **DataDogue Enterprize**   | `monitoring`    | ❌     |
| Kubernetes Operators  | **Kuzubernètes OpéraTeur** | `orchestration` | ✅     |
| PlanetScale (Vitess)  | **PlanetSkale Proto**      | `managed-db`    | ❌     |
| Cloudflare Workers    | **KloudFlair Workerot**    | `serverless`    | ❌     |

***

## Tier 10 — 2022 | Platform Engineering / IA

*Stack type : IDP + OpenTelemetry + LLM. L'ère où "l'IA" justifiait tout (à la place de "serverless").*

| Nom réel             | Nom Kouraks             | Type           | reqHW |
|:---------------------|:------------------------|:---------------|:------|
| OpenTelemetry        | **OpennTéléMétrux**     | `monitoring`   | ✅     |
| Backstage (IDP)      | **BackStagueux IDP**    | `platform`     | ✅     |
| Cilium / eBPF mesh   | **Cilyoum Mesh eBPF**   | `service-mesh` | ✅     |
| OpenAI API / Bedrock | **GPTifié API**         | `serverless`   | ❌     |
| Neon / Turso         | **NéonBD Serverless**   | `managed-db`   | ❌     |
| FinOps tooling       | **KouraKostOptimizeur** | `financial`    | ❌     |

***

## Points structurants à noter

**L'évolution des `requireHardware: false`** suit la réalité : zéro SaaS au T1, un par-ci par-là au T3-T4, et en T9-T10
presque la moitié des services n'ont plus besoin de hardware owned. C'est le message le plus satirique du jeu — le
joueur finit par *louer* la quasi-totalité de sa stack à des tiers dont il ne contrôle rien.

**Le `KouraKostOptimizeur` (T10)** est un service financier spécial : il réduit les `runCost` de tous les autres
services d'un pourcentage — ironiquement, c'est le service le plus cher du jeu, et son ROI ne devient positif qu'après ~
2h de jeu. Exactement comme en vrai.

**La progression des types** introduit naturellement de la complexité : les projets de T7+ peuvent
`requires: [backend, database, search, container]` — quadrupler les services requis, donc quadrupler le coût hardware,
donc incarner parfaitement la dette technique. [^9_1]

<div align="center">⁂</div>

[^9_1]: 8a4f95e4.md


---

# Franchement ta liste est top, par contre ça me fait mal d'avoir l'impression d'avoir été en retard d'un ou deux tiers à chaque fois dans la vrai vie par rapport aux années que tu retiens ! J'ai l'impression que le tiers 4 c'était en 2008 par exemple. Le tiers 5 je l'aurai mis en 2010, etc.

Maintenant si on imagine qu'on a un ou deux nouveaux projets par tiers + un ou deux projets qui migrent du tiers
précédent - un ou deux projets qui disparaissent et que en gros on passe de 1 projet à une dizaine de projets à gérer il
faut proposer une grande variété de services pour architecturer tout ça, au tiers 10 il faut que je joueur se sente
perdu tellement il y a d'options possibles.
J'ajouterai que dans les tiers supérieur il faut bien exagérer sur la complexité des projets, on peut vite se retrouver
avec des stacks techniques avec un assortiment incroyable de technologies, surtout celles open-source qui sont devenues
fiables : ElasticSearch, PostgreSQL, Symfony, Caddy, FrankenPHP, Traefik, Redis, Mailchimp, Github Actions, ELK,
Authentik c'est une stack assez standard pour moi par exemple.

**114 services**, 21 types — voilà l'échelle du jeu. [^10_1] Les années sont recalées sur ta réalité terrain (+2 à +3
ans par rapport aux trends Silicon Valley). Voici la liste complète — seuls les services *nouveaux* sont listés à chaque
tier, tout le reste reste disponible en marketplace.

***

## Vue d'ensemble de la progression

| Tier | Époque | Projets actifs | Nouveaux services | Cumulé dispo | SaaS%   |
|:-----|:-------|:---------------|:------------------|:-------------|:--------|
| T1   | 1995   | 1              | 4                 | 4            | 0%      |
| T2   | 2000   | 2              | 5                 | 9            | 0%      |
| T3   | 2004   | 3              | 7                 | 16           | 12%     |
| T4   | 2008   | 4              | 8                 | 24           | 4%      |
| T5   | 2011   | 5              | 11                | 35           | 18%     |
| T6   | 2014   | 6              | 11                | 46           | 18%     |
| T7   | 2017   | 7              | 14                | 60           | 29%     |
| T8   | 2020   | 8              | 16                | 76           | 31%     |
| T9   | 2022   | 9              | 17                | 93           | 35%     |
| T10  | 2024   | 10             | 21                | **114**      | **38%** |

***

## T1 — 1995 | CGI / Web statique

| Nom réel                | Nom Kouraks              | Type            | reqHW |
|:------------------------|:-------------------------|:----------------|:------|
| Perl CGI                | **GRAs.pl**              | `backend`       | ✅     |
| Apache 0.6 / NCSA HTTPd | **Apacheux HTTPdi Zéro** | `reverse-proxy` | ✅     |
| MySQL 1.0               | **MoïSQL 1.0 Community** | `database`      | ✅     |
| WU-FTPd                 | **FaTéPé Workerot**      | `storage`       | ✅     |

***

## T2 — 2000 | LAMP / PHP 3

| Nom réel      | Nom Kouraks           | Type            | reqHW |
|:--------------|:----------------------|:----------------|:------|
| PHP 3         | **PHP Troizième**     | `backend`       | ✅     |
| Apache 1.3    | **Apacheux 1.3 LTS**  | `reverse-proxy` | ✅     |
| MySQL 3.23    | **MoïSQL 3.0 InnoDB** | `database`      | ✅     |
| Cold Fusion 3 | **FroïdFusion III**   | `backend`       | ✅     |
| Nagios 1.0    | **Nageois Alfa**      | `monitoring`    | ✅     |

***

## T3 — 2004 | J2EE / aftermath dot-com

| Nom réel       | Nom Kouraks                  | Type            | reqHW |
|:---------------|:-----------------------------|:----------------|:------|
| Tomcat 4       | **TomKatt 4.0 Catalina**     | `backend`       | ✅     |
| JBoss 3        | **JeuxBoss 3.0 EE**          | `backend`       | ✅     |
| Oracle 9i      | **OraKleur 9i Entreprize**   | `database`      | ✅     |
| Nginx 0.1      | **N-Ginx Zéro-Un**           | `reverse-proxy` | ✅     |
| Nagios 2.0     | **Nageois 2.0 Stable**       | `monitoring`    | ✅     |
| Akamai CDN     | **AkaMaï CDN Prestige** ☁️   | `cdn`           | ❌     |
| Prêt financier | **Prêt KouraKal Express** ☁️ | `financial`     | ❌     |

***

## T4 — 2008 | PHP 5 / Symfony 1 / Memcached

| Nom réel        | Nom Kouraks                           | Type         | reqHW |
|:----------------|:--------------------------------------|:-------------|:------|
| PHP 5.2         | **PHP Cinq Community**                | `backend`    | ✅     |
| Symfony 1.4 LTS | **Simphonie 1.4 LTS**                 | `backend`    | ✅     |
| Memcached 1.4   | **MemCacheux 1.4**                    | `cache`      | ✅     |
| MySQL 5.1       | **MoïSQL 5.1 Pakke**                  | `database`   | ✅     |
| PostgreSQL 8.3  | **PostGrès 8.3**                      | `database`   | ✅     |
| Postfix 2       | **PosTafixe Deux**                    | `email`      | ✅     |
| Munin           | **Mougnin Agent**                     | `monitoring` | ✅     |
| Obligations     | **Obligations KouraKalistes 6.5%** ☁️ | `financial`  | ❌     |

***

## T5 — 2011 | NoSQL / Rails / Node.js

| Nom réel         | Nom Kouraks                 | Type            | reqHW |
|:-----------------|:----------------------------|:----------------|:------|
| Ruby on Rails 3  | **Railzôt 3.0**             | `backend`       | ✅     |
| Django 1.3       | **Diango 1.3**              | `backend`       | ✅     |
| Node.js 0.6      | **Nœud.js Zéro-Six**        | `backend`       | ✅     |
| MongoDB 2.0      | **MongueBD 2.0**            | `database`      | ✅     |
| Redis 2.4        | **Rédiss 2.4**              | `cache`         | ✅     |
| RabbitMQ 2.0     | **LapinMQ 2.0 Broker**      | `message-queue` | ✅     |
| Solr 3           | **SolReau 3.0**             | `search`        | ✅     |
| HAProxy 1.4      | **HaïProxi 1.4**            | `reverse-proxy` | ✅     |
| Graphite 0.9     | **Graphiteux 0.9**          | `monitoring`    | ✅     |
| Cloudflare Basic | **KloudFlair Basic CDN** ☁️ | `cdn`           | ❌     |
| AWS S3           | **Ausse S3-Eau** ☁️         | `storage`       | ❌     |

***

## T6 — 2014 | Docker / Big Data / Symfony 2

| Nom réel          | Nom Kouraks                | Type            | reqHW |
|:------------------|:---------------------------|:----------------|:------|
| Symfony 2.7 LTS   | **Simphonie 2.7 LTS**      | `backend`       | ✅     |
| Laravel 4         | **Laravelo 4.0**           | `backend`       | ✅     |
| Docker 1.0        | **Docqueur 1.0**           | `container`     | ✅     |
| Elasticsearch 1.4 | **ElasticRechèrche 1.4**   | `search`        | ✅     |
| Kafka 0.8         | **KafQuoi 0.8**            | `message-queue` | ✅     |
| Cassandra 2.0     | **KassandraBD 2.0**        | `database`      | ✅     |
| ClickHouse alpha  | **KlikHousse Alpha**       | `database`      | ✅     |
| ELK Stack         | **ELKasse Stack 1.0**      | `monitoring`    | ✅     |
| OpenLDAP          | **LéDAPe Ouvert**          | `auth`          | ✅     |
| Mailchimp API     | **MailChimpanzé API** ☁️   | `email`         | ❌     |
| AWS RDS           | **Ausse RéDéS Managed** ☁️ | `managed-db`    | ❌     |

***

## T7 — 2017 | Kubernetes / Prometheus / API-first

| Nom réel             | Nom Kouraks                | Type            | reqHW |
|:---------------------|:---------------------------|:----------------|:------|
| Go 1.8               | **GoLangueux 1.8**         | `backend`       | ✅     |
| Symfony 4 Flex       | **Simphonie 4.0 Flex**     | `backend`       | ✅     |
| FastAPI (proto)      | **FastAïPI Proto**         | `backend`       | ✅     |
| Traefik 1.0          | **TréfikBal 1.0**          | `reverse-proxy` | ✅     |
| Kubernetes 1.6       | **Kuzubernètes 1.6**       | `orchestration` | ✅     |
| Prometheus + Grafana | **Prométhéos + Grapphane** | `monitoring`    | ✅     |
| Redis Cluster        | **Rédiss Kluster HA**      | `cache`         | ✅     |
| Keycloak 3           | **KeyKloaque 3.0**         | `auth`          | ✅     |
| Jenkins / GitLab CI  | **Djenkines PipeLaine**    | `ci-cd`         | ✅     |
| MinIO                | **MinioStorague**          | `storage`       | ✅     |
| Datadog SaaS         | **DataDogue Lite SaaS** ☁️ | `monitoring`    | ❌     |
| AWS DynamoDB         | **DinahmoBD Managed** ☁️   | `managed-db`    | ❌     |
| SendGrid             | **SéndGridosse** ☁️        | `email`         | ❌     |
| AWS Lambda           | **Lambdeau Fonktion** ☁️   | `serverless`    | ❌     |

***

## T8 — 2020 | GitOps / Service Mesh / Observabilité

| Nom réel           | Nom Kouraks                       | Type            | reqHW |
|:-------------------|:----------------------------------|:----------------|:------|
| Symfony 5 / PHP 8  | **Simphonie 5.0 Attributz**       | `backend`       | ✅     |
| Rust (Actix-web)   | **RustaCé Actixe**                | `backend`       | ✅     |
| FrankenPHP alpha   | **FrankenPéHache Alpha**          | `backend`       | ✅     |
| Caddy 2.0          | **KaddyBal 2.0**                  | `reverse-proxy` | ✅     |
| Istio 1.6          | **Istiaux 1.6 Mesh**              | `service-mesh`  | ✅     |
| ArgoCD 1.5         | **ArgueCéDé GitOpse**             | `ci-cd`         | ✅     |
| Terraform 0.13     | **TerraForme IaC**                | `ci-cd`         | ✅     |
| PostgreSQL 13      | **PostGrès 13 Partitionné**       | `database`      | ✅     |
| TimescaleDB        | **TimeskailDB**                   | `database`      | ✅     |
| Authentik 0.9      | **AuthentikExtra 0.9**            | `auth`          | ✅     |
| HashiCorp Vault    | **VaultSecretz**                  | `secret`        | ✅     |
| GitHub Actions     | **GuitHub Aksionne** ☁️           | `ci-cd`         | ❌     |
| Sentry SaaS        | **SéntryErreurz SaaS** ☁️         | `monitoring`    | ❌     |
| Confluent Cloud    | **KafQuoiCloud Managed** ☁️       | `message-queue` | ❌     |
| Cloudflare Workers | **KloudFlair Workerot** ☁️        | `serverless`    | ❌     |
| LaunchDarkly       | **LaunchDarkeau Feature Flag** ☁️ | `feature-flag`  | ❌     |

***

## T9 — 2022 | Platform Eng / Observabilité totale

| Nom réel               | Nom Kouraks                      | Type            | reqHW |
|:-----------------------|:---------------------------------|:----------------|:------|
| Bun.js 1.0             | **Bunsse.js 1.0**                | `backend`       | ✅     |
| Symfony 6 + FrankenPHP | **Simphonie 6.0 FrankenPéHache** | `backend`       | ✅     |
| Meilisearch 1.0        | **MeilleureRecherche 1.0**       | `search`        | ✅     |
| Typesense 0.24         | **TypeSensé 0.24**               | `search`        | ✅     |
| NATS.io 2.0            | **NATzSeau 2.0**                 | `message-queue` | ✅     |
| Pulsar 2.10            | **PulsarKaï 2.10**               | `message-queue` | ✅     |
| Cilium / eBPF          | **Cilyoum Mesh eBPF**            | `service-mesh`  | ✅     |
| Linkerd 2.0            | **LinkerDé 2.0**                 | `service-mesh`  | ✅     |
| OpenTelemetry 1.0      | **OpennTéléMétrux 1.0**          | `monitoring`    | ✅     |
| Kubernetes Operators   | **Kuzubernètes OpéraTeur**       | `orchestration` | ✅     |
| Unleash (self-hosted)  | **UnléashFlag OS**               | `feature-flag`  | ✅     |
| PlanetScale            | **PlanetSkale Vitesse** ☁️       | `managed-db`    | ❌     |
| Datadog Enterprise     | **DataDogue Enterprize** ☁️      | `monitoring`    | ❌     |
| Resend.com             | **RézéndOh** ☁️                  | `email`         | ❌     |
| Neon DB                | **NéonBD Serverless** ☁️         | `managed-db`    | ❌     |
| BunnyCDN               | **BunkeurCDN** ☁️                | `cdn`           | ❌     |
| KouraKost Optimizer    | **KouraKostOptimizeur** ☁️       | `financial`     | ❌     |

***

## T10 — 2024 | AI-augmented / Everything-as-Code

*Le joueur a 93 services disponibles. 21 nouveaux arrivent. C'est intentionnel.*

| Nom réel              | Nom Kouraks                   | Type            | reqHW |
|:----------------------|:------------------------------|:----------------|:------|
| Symfony 7             | **Simphonie 7.0 Ultimaute**   | `backend`       | ✅     |
| Rust (Axum)           | **RustaCé Axuome**            | `backend`       | ✅     |
| Hono.js (edge)        | **HonnoJS EdgeEdge**          | `backend`       | ✅     |
| Backstage IDP         | **BackStagueux IDP**          | `platform`      | ✅     |
| Valkey 7 (Redis fork) | **ValkéieCache 7.0**          | `cache`         | ✅     |
| DragonflyDB           | **DragonFlieBD**              | `cache`         | ✅     |
| Redpanda              | **RedPandaMQ Bête**           | `message-queue` | ✅     |
| ClickHouse 24         | **KlikHousse 24 OLAP**        | `database`      | ✅     |
| Qdrant (vector DB)    | **KadrantVecto**              | `database`      | ✅     |
| Grafana LGTM stack    | **GrapphaneTotal LGTM**       | `monitoring`    | ✅     |
| Pomerium / Zitadel    | **PoméRioum ZéroTruste**      | `auth`          | ✅     |
| Karpenter             | **KarpanteurK8z**             | `orchestration` | ✅     |
| Dagger.io             | **DaguioCI**                  | `ci-cd`         | ✅     |
| OpenAI / Bedrock API  | **GPTifié API** ☁️            | `serverless`    | ❌     |
| Turso / LibSQL        | **TursoLibSQL Edge** ☁️       | `managed-db`    | ❌     |
| Upstash Redis         | **UpstashRédiss Cloud** ☁️    | `cache`         | ❌     |
| Inngest               | **InnguésteEvent** ☁️         | `message-queue` | ❌     |
| Trigger.dev           | **TrigueurDév Workerot** ☁️   | `ci-cd`         | ❌     |
| Okta / WorkOS         | **OktaWée Enterprise SSO** ☁️ | `auth`          | ❌     |
| Infisical             | **InfissiKal Sekretz** ☁️     | `secret`        | ❌     |
| Unleash Enterprise    | **UnléashFlag Enterprize** ☁️ | `feature-flag`  | ❌     |

***

## Répartition finale par type (114 services)

| Type            | Nb | Satire incarnée                                          |
|:----------------|:---|:---------------------------------------------------------|
| `backend`       | 23 | Un nouveau framework par an, tous "révolutionnaires"     |
| `database`      | 12 | "NoSQL is dead. Long live NewSQL. Long live HTAP."       |
| `monitoring`    | 11 | On ne regarde jamais les dashboards de toute façon       |
| `message-queue` | 7  | Kafka pour envoyer des emails de contact                 |
| `ci-cd`         | 6  | Le pipeline qui build le pipeline qui deploy le pipeline |
| `cache`         | 6  | Mise en cache de la mise en cache                        |
| `auth`          | 5  | 5 systèmes d'auth pour une seule équipe de 3 devs        |
| `reverse-proxy` | 6  | Traefik devant Nginx devant Caddy, pourquoi pas          |

La **progression SaaS** passe de 0% (T1) à 38% (T10) : le joueur finit par louer le tiers de son infrastructure à des
tiers dont il ne contrôle rien, sans hardware assigné, avec uniquement un `runCostPerSec` qui croît [^10_1]. C'est le
message final du jeu avant même le dernier milestone.

<div align="center">⁂</div>

[^10_1]: 8a4f95e4.md


---

# Ok maintenant il faut considérer que par défaut TOUS les services vont rester dispos dans les tiers supérieurs mais certains seront dépréciés, on affichera clairement un truc en rouge du genre "dernière version en 20XX" et les propriétés seront globalement dissuasive par rapport aux nouveaux services. Du coup ma question est très simple : est-ce que dans le liste que tu as créé il y des services/technos qui sont mortes et si oui à quel tiers ?

Voici la réponse directe. En croisant les dates EOL réelles avec notre échelle de tiers :

## Technologies vraiment mortes (produit arrêté)

| Service       | Nom Kouraks          | Mort réellement en                                                        | Déprécié au tier |
|:--------------|:---------------------|:--------------------------------------------------------------------------|:-----------------|
| NCSA HTTPd    | Apacheux HTTPdi Zéro | 1996 (remplacé par Apache immédiatement)                                  | **T2**           |
| WU-FTPd       | FaTéPé Workerot      | ~2003 (failles critiques, jamais patché)                                  | **T4**           |
| PHP 3         | PHP Troizième        | 2000                                                                      | **T4**           |
| Cold Fusion 3 | FroïdFusion III      | ~2005 (le produit survit en zombie jusqu'en 2025 mais CF3 est un fossile) | **T5**           |
| Perl CGI      | GRAs.pl              | ~2006 (encore vivant mais aucun nouveau projet)                           | **T5**           |
| JBoss AS 3    | JeuxBoss 3.0 EE      | 2012 (rebrandé WildFly, JBoss AS abandonné)                               | **T6**           |
| Munin         | Mougnin Agent        | ~2016 (maintenance minimale, irrélevant post-Prometheus)                  | **T7**           |
| Graphite      | Graphiteux 0.9       | ~2016 (remplacé par Prometheus+Grafana)                                   | **T7**           |

## Versions mortes de technos vivantes

| Service                                  | Mort en              | Déprécié au tier |
|:-----------------------------------------|:---------------------|:-----------------|
| MySQL 1.0 (MoïSQL 1.0)                   | ~1997                | **T3**           |
| MySQL 3.23 (MoïSQL 3.0)                  | 2006                 | **T5**           |
| PostgreSQL 8.3 (PostGrès 8.3)            | Fév. 2013            | **T7**           |
| MySQL 5.1 (MoïSQL 5.1)                   | Déc. 2013            | **T7**           |
| Ruby on Rails 3 (Railzôt 3.0)            | Juin 2013 [^11_1]    | **T7**           |
| Django 1.3 (Diango 1.3)                  | Fév. 2013            | **T7**           |
| Node.js 0.6 (Nœud.js Zéro-Six)           | ~2013                | **T7**           |
| Symfony 1.4 (Simphonie 1.4 LTS)          | Fév. 2012 [^11_1]    | **T7**           |
| Nagios 1.0 (Nageois Alfa)                | ~2014 (version)      | **T7**           |
| Redis 2.4 (Rédiss 2.4)                   | ~2015                | **T8**           |
| Elasticsearch 1.4 (ElasticRechèrche 1.4) | 2016                 | **T8**           |
| Kafka 0.8 (KafQuoi 0.8)                  | ~2017                | **T8**           |
| PHP 5.x (PHP Cinq Community)             | 31 déc. 2018 [^11_2] | **T9**           |
| Symfony 2.7 (Simphonie 2.7 LTS)          | Mai 2019 [^11_1]     | **T9**           |
| Symfony 4.0 (Simphonie 4.0 Flex)         | Nov. 2020 [^11_3]    | **T9**           |
| Symfony 5.4 (Simphonie 5.0 Attributz)    | Nov. 2024 [^11_1]    | **T10**          |

## Ce qui survit (contre toute attente)

Quelques surprises qui ne devraient **pas** être dépréciées dans le jeu : [^11_4]

- **ColdFusion** → Adobe ColdFusion 2023 est encore supporté jusqu'en 2028. Zombie officiel.
- **Nagios** (l'outil, pas la v1.0) → encore maintenu, utilisé dans des DSI fossilisées
- **Apache HTTPd** → toujours très vivant (2.4.x actif)
- **Jenkins** → déclinant mais pas mort, toujours massivement déployé

***

## Implications design

Les dépréciations créent un **pic au T7** — c'est le tier où 8 services deviennent rouges simultanément. C'est cohérent
avec la réalité : 2017 est l'année où toute la stack "startup 2010" est devenue de la dette technique visible. Ça peut
être un moment narratif fort — un mail du PDG qui dit *"on m'a dit qu'on tourne encore sur des trucs EOL depuis 2013 ?"*
<span style="display:none">[^11_10][^11_11][^11_12][^11_13][^11_14][^11_15][^11_5][^11_6][^11_7][^11_8][^11_9]</span>

<div align="center">⁂</div>

[^11_1]: https://endoflife.software/programming-languages/frameworks/symfony

[^11_2]: https://www.digital4all.fr/end-php5/

[^11_3]: https://endoflife.date/symfony

[^11_4]: https://www.carehart.org/blog/2025/1/9/coldfusion2021_end_of_life_nov_2025

[^11_5]: https://www.php.net/supported-versions.php

[^11_6]: https://endoflife.date/php

[^11_7]: https://www.php.net/eol.php

[^11_8]: https://www.itomic.com.au/end-of-life-for-php-v5-is-31-dec-2018-what-does-this-mean-for-you/

[^11_9]: https://eosl.date/eol/product/symfony/

[^11_10]: https://www.digitalcanvas.com/blog/php-56-end-of-life-guide/

[^11_11]: https://www.lansweeper.com/blog/eol/adobe-coldfusion-end-of-life/

[^11_12]: https://tuxcare.com/blog/php-5-end-of-life/

[^11_13]: https://symfony.com/blog/symfony-maintenance-changes-for-standard-releases

[^11_14]: https://www.carehart.org/blog/2020/11/23/cf2016_support_ends_feb_2021

[^11_15]: https://www.zend.com/resources/php-versions


---

# je viens de penser à une mécanique toute simple pour justifier l'instabilité des anciennes versions de services : dans les messages d'erreur on met des attaques de pirates, des virus et autres truc du genre. Ils vont juste apparaître aléatoirement avec la même probabilité que les autres messages mais justifie plus facilement en terme de lore le fait qu'il faut absolument mettre à jour.

J'en ferais peut-être une mécanique à part plus tard avec des CVE aléatoires mais pour l'instant ça suffira avec juste
les messages.

Idée parfaite — zéro coût technique, impact narratif maximal. [^12_1]

## Ce que ça change (rien) et ce que ça apporte (beaucoup)

Mécaniquement c'est **exactement le même système de messages** que les crashes normaux — juste un pool de messages
supplémentaires qui s'activent sur les services avec `deprecated: true`. Pas de nouveau système, pas de CVE tracker, pas
de flag spécial. Une seule condition dans le générateur de message :

```javascript
function getCrashMessage(service) {
    const pool = service.deprecated
        ? [...crashMessages.generic, ...crashMessages.security]
        : crashMessages.generic;
    return pool[Math.floor(Math.random() * pool.length)];
}
```

## Banque de messages sécurité

Le ton reste le même — résignation sardonique — mais avec une couleur "on savait depuis 2 ans" : [^12_1]

**Sur services dépréciés génériques :**

- *"MoïSQL 3.0 a crashé. CVE-2009-2446. On en avait parlé en réunion."*
- *"PHP Cinq Community est tombé. Buffer overflow connu depuis 2017. Le ticket Jira est ouvert."*
- *"GRAs.pl a crashé. Injection SQL détectée. Surprise totale pour tout le monde."*
- *"Nageois Alfa s'est arrêté. Quelqu'un a scanné le port 80. C'était suffisant."*

**Sur services très anciens (T1-T3 encore en prod) :**

- *"FaTéPé Workerot a crashé. Accès anonyme activé par défaut depuis 1998. Personne n'avait vérifié."*
- *"FroïdFusion III est tombé. Adobe ne répond plus aux mails de support. Depuis 2009."*
- *"PHP Troizième a crashé. Le hacker avait 12 ans. Il apprenait."*
- *"JeuxBoss 3.0 EE s'est arrêté. RCE via JMX. Port 1099 ouvert sur l'internet public. Classique."*

**Sur la non-action :**

- *"MoïSQL 5.1 a crashé. EOL décembre 2013. On est en [année courante du jeu]."*
- *"Railzôt 3.0 est tombé. La migration vers Railzôt 4 était estimée à 3 sprints en 2014."*
- *"Simphonie 2.7 LTS a crashé. Le ticket de migration est dans le backlog depuis 4 ans. Priorité : basse."*

**Le coup de grâce (service EOL + proche du game over) :**

- *"GRAs.pl a crashé. C'était dans le rapport de sécurité de 2007. Page 47. Recommandation \#3."*

***

## Une subtilité à garder

Les messages de sécurité ne doivent **pas** être plus fréquents que les messages normaux — juste présents dans le pool.
Si le joueur voit trop de messages sécurité d'affilée ça devient une leçon de morale, pas une satire. Le ratio 50/50
generic/security sur les services dépréciés est suffisant pour que le message passe sans être moralisateur. [^12_1]

<div align="center">⁂</div>

