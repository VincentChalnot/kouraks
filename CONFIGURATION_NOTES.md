# Configuration Finale - Notes de Conception

## Résumé

J'ai créé 4 fichiers YAML de configuration pour le jeu Kourasks, plus un document de résumé de progression :

### 1. hardware.yaml (45 items)
- **10 tiers** de hardware couvrant 1994-2022
- **Mix de types**: Entry-level, Gaming, Flagship, Dédié, VPS
- **Progression réaliste**: Multiplicateurs de ×0.6 à ×108
- **Coûts**: De gratuit (486DX) à 3M K (EPYC)
- **Float unlockAtTrimester**: De 0 à 14.2 pour déblocage progressif

### 2. services.yaml (114 services)
- **10 tiers** alignés avec l'histoire réelle de la tech
- **Types variés**: backend, database, cache, monitoring, cdn, etc.
- **Progression SaaS**: 0% (T1) → 38% (T10)
- **Services deprecated**: Marqués avec deprecatedAtTrimester
- **Services financiers**: Prêt (0K event), Obligations (passif), Optimizer (réduction coûts)

### 3. projects.yaml (10 projets)
- **Progression narrative**: Site perso → AI/ML platform
- **23 versions** au total réparties sur les projets
- **targetProduction calculé**: Basé sur 1 trimestre = 360 secondes
- **eventId par version**: Pour déclencher les mails correspondants
- **Requirements croissants**: De 1 service (T0) à 9 services (T17+)

### 4. mail.yaml (28+ mails)
- **Emails de lancement**: 1 mail par nouveau projet
- **Emails de migration**: Pour les upgrades forcées
- **Système Zero Kouraks**: 3 warnings progressifs → Game Over
- **Mails de strikes**: 1 par strike de projet
- **Milestones**: 100K, 1M, 10M Kouraks
- **Fin de jeu**: Victory (rachat entreprise) ou Game Over (faillite)

### 5. PROGRESSION_SUMMARY.md
Document récapitulatif avec timeline complète et tables de référence

## Points clés de la conception

### Timing & Balance
- **1 trimestre = 6 minutes** de jeu réel
- **T0 → T32**: ~3h12min pour compléter le jeu
- **Float unlockAtTrimester**: Permet un flux continu (0.8, 1.5, 2.3, etc.)
- **targetProduction**: Augmente exponentiellement avec la complexité

### Système d'événements
```yaml
# Dans projects.yaml
eventId: project-v1-launched

# Dans mail.yaml
unlockAtEvent: project-v1-launched
```
Les projets déclenchent des events, les mails s'y abonnent.

### Services deprecated
```yaml
deprecatedAtTrimester: 5.0
```
Après ce trimestre, le crashRate augmente progressivement, forçant la migration.

### Hardware types
- **Entry** (🟤): Pas cher, faible capacité
- **Gaming** (🎮): Bon single-thread, consommation élevée
- **Flagship** (🔵): Équilibré, référence de l'époque
- **Dédié** (🟠): Location, bon rapport, long provisioning
- **VPS** (☁️): Cloud, rapide à déployer, capacité limitée

### Services types
- **Production**: backend, database, cache → génèrent du yield
- **Infrastructure**: monitoring, proxy, orchestration → multiplicateurs
- **SaaS**: cdn, managed-db → requireHardware: false
- **Financial**: Mécaniques spéciales (loans, investments)

## Ajustements futurs possibles

### Si le jeu est trop difficile
1. Réduire les `targetProduction` dans projects.yaml (×0.8)
2. Augmenter les `baseYield` dans services.yaml (×1.2)
3. Réduire les `recurringCost` des hardware/services

### Si le jeu est trop facile
1. Augmenter les `targetProduction` (×1.3)
2. Augmenter les `crashRate` des services
3. Débloquer les projets plus tôt (plus de projets simultanés)

### Si la progression est trop lente
1. Réduire les valeurs de `unlockAtTrimester` (×0.8)
2. Augmenter les `baseYield` significativement
3. Réduire les `deployCost` des hardware

### Si la progression est trop rapide
1. Augmenter les `unlockAtTrimester` (×1.2)
2. Augmenter les coûts (deployCost, recurringCost)
3. Ajouter plus de requirements aux projets

## Données de référence rapide

### Hardware Flagship par tier
| Tier | Nom | Coût | Mult | MaxYield | Trim |
|------|-----|------|------|----------|------|
| 1 | Conpac 486DX | 0 | ×1.0 | 15 | 0 |
| 2 | PentiumPro 200 | 200 | ×1.7 | 25 | 1.5 |
| 3 | SPARC 20 | 800 | ×2.8 | 42 | 2.7 |
| 4 | Dell PE 265 | 3000 | ×4.5 | 70 | 4.3 |
| 5 | HP DL380 G5 | 10000 | ×7.5 | 130 | 5.8 |
| 6 | Dell M710 | 35000 | ×13 | 226 | 7.2 |
| 7 | HP Gen8 | 100000 | ×21 | 365 | 8.8 |
| 8 | Cisco UCS | 300000 | ×34 | 591 | 10.3 |
| 9 | Dell EPYC | 900000 | ×58 | 1008 | 11.8 |
| 10 | Supermicro | 3000000 | ×95 | 1652 | 13.8 |

### Projets et leurs versions
| Projet | v1 | v2 | v3 | Services finaux |
|--------|----|----|----|-----------------|
| Site Vitrine | T0 | T1.5 | - | 2 |
| Forum | T1.5 | T3.5 | - | 3 |
| E-commerce | T2.5 | T5 | - | 4 |
| SaaS | T4 | T6.5 | - | 5 |
| API Mobile | T5.5 | T8 | - | 5 |
| Streaming | T7 | T9.5 | - | 7 |
| Fintech | T8.5 | T11 | - | 7 |
| IoT | T10 | T12.5 | - | 6 |
| Social | T11.5 | T14 | - | 9 |
| AI/ML | T13 | T15.5 | T17.5 | 9 |

### Services par catégorie (114 total)
- **backend**: 23 services
- **database**: 12 services
- **monitoring**: 11 services
- **cache**: 6 services
- **message-queue**: 7 services
- **reverse-proxy**: 6 services
- **Autres**: 49 services (search, storage, cdn, auth, ci-cd, etc.)

## Architecture du système

### Calcul du yield (simplifié)
```
service_yield = baseYield × hardware.yieldMultiplier × service.yieldMultiplier
effective_yield = min(service_yield, hardware.maximumYield)
project_yield = MIN(tous les services assignés au projet)
total = SUM(tous les projets)
net_yield = total - SUM(recurringCost)
```

### Conditions de déblocage
1. **unlockAtTrimester**: Temps écoulé
2. **unlockAtEvent**: Event déclenché par un autre élément
3. **Les deux**: Débloqué dès que l'un des deux est satisfait

### Game Over conditions
1. **3 passages à 0 Kouraks**: Mail final → ESN prend le relais
2. **3 projets failed**: Même résultat
3. **Pas de game over si**: Le joueur maintient la prod et évite les strikes

### Victory condition
- **Atteindre T20+** avec succès
- **Mail de rachat** par un GAFAM
- **Prime de 10K€** et MacBook gravé

## Commentaires dans les YAML

Tous les fichiers YAML contiennent :
- Des commentaires explicatifs
- Des notes de conception en fin de fichier
- Des exemples de valeurs calculées
- Des références aux mécaniques de jeu

## Prochaines étapes suggérées

1. **Playtest**: Tester la progression complète
2. **Balance**: Ajuster targetProduction selon les retours
3. **Narrative**: Enrichir les mails si nécessaire
4. **Services**: Ajouter des versions intermédiaires si trop de gaps
5. **Hardware**: Ajuster les coûts si l'économie est déséquilibrée
6. **Events**: Ajouter des events pour plus de narrative (acquisitions, crashs majeurs, etc.)

## Fichiers générés

```
/home/runner/work/kourasks/kourasks/
├── hardware.yaml (45 hardware items)
├── services.yaml (114 services with versions)
├── projects.yaml (10 projects, 23 versions)
├── mail.yaml (28+ narrative emails)
├── PROGRESSION_SUMMARY.md (timeline & reference)
└── CONFIGURATION_NOTES.md (ce fichier)
```

Tous les fichiers sont prêts à être intégrés dans le jeu !
