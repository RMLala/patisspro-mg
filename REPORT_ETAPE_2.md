# PâtissPro MG — Rapport d’avancement Phase 2

**Date :** 12 novembre 2026  
**Branche :** `work/patisspro-mvp-2026-11-12`  
**Portée :** Premium — fiches recettes, sous-recettes et coût de revient.

## Réalisé dans le code

- Éditeur de recette en lignes FR/MG, avec sélection d’ingrédients ou de sous-recettes, quantité et unité.
- Conversion des quantités kg/g, L/mL et unités/pièces ; unités incompatibles signalées dans le coût.
- Calcul récursif du coût matière, puis ajout des coûts d’emballage, main-d’œuvre et charges indirectes.
- Coût affiché par lot et par portion, prix conseillé selon marge cible.
- Ajustement des quantités pour un rendement demandé.
- Historique d’une ancienne version à chaque modification significative (date, coût/portion et photographie des champs de recette).
- Garde contre les boucles de sous-recettes et valeurs par défaut pour les données des anciennes versions.
- Fichier Android embarqué aligné sur le HTML autonome. Documentation et guide FR/MG actualisés.

## Fichiers modifiés

- `index.html`
- `app/src/main/assets/index.html`
- `docs/CAHIER_DES_CHARGES_V1.0.md`
- `docs/GUIDE_UTILISATEUR_FR_MG.md`
- `CHANGELOG.md`
- `REPORT_ETAPE_2.md`

## Vérifications effectuées

- `node --check` sur le JavaScript intégré : réussi.
- Comparaison du fichier HTML autonome et de l’asset Android : identiques au moment de la synchronisation.
- Vérification des conversions et calculs : 8 assertions Node réussies (kg/g, L/mL, dimensions incompatibles, coût matière imbriqué, coût complet, unités de sous-recette et boucle).
- Copie HTML autonome / asset Android : identiques.
- Build Gradle local : indisponible, la commande `gradle` et le wrapper ne sont pas présents dans l’espace. GitHub Actions run #11 réussi le 12/11/2026 : les variantes `assembleApi23Debug` et `assembleApi29Debug` ont compilé et l’artefact Debug a été publié. Le job Release a été ignoré conformément au workflow.
- Vérification visuelle Playwright : non réalisée, exécutable Chromium absent ; aucun parcours navigateur n’est déclaré vérifié.

## Limites connues

- Le tableau de calcul de rendement affiche les lignes directes de la recette ; il ne développe pas encore récursivement la liste des matières des sous-recettes.
- Les prix matière sont basés sur le coût unitaire actuellement saisi dans l’article ; pas encore de coûts moyens calculés depuis les achats ou les lots.
- L’historique est consultable dans l’interface, sans fonction de restauration d’une version.
- Persistances locales seulement : aucun achat fournisseur complet, lot FIFO, sync Cloudflare/D1, licences AppForge, sauvegarde chiffrée ou multi-sites dans ce lot.

## Trois prochaines actions prioritaires

1. Ajouter achats/réceptions avec lots, dates de péremption, mouvements audités et consommation FIFO.
2. Compléter le planning et la production avec calcul des besoins sur les recettes et réservations de stock.
3. Ajouter des tests d’interface réels et consolider la PR avec la nouvelle version, sans fusionner `main`.
