# Rapport d’avancement — PâtissPro MG — étape 1

**Date :** 12 novembre 2026  
**État :** cahier des charges V1.0 rédigé ; MVP v0.1.0 développé en local.  
**Périmètre accompli :** HTML autonome responsive ; interface FR/MG ; dashboard calculé à partir des encaissements/dépenses saisis ; création/modification/suppression locale des produits, matières, commandes, recettes, ordres de production et dépenses ; réception de stock ; ventes directes ; statuts et remise ; sauvegarde JSON, restauration JSON et export commandes CSV ; guide utilisateur FR/MG ; squelette Android et workflow Actions.

## Fichiers préparés
- `docs/CAHIER_DES_CHARGES_V1.0.md`
- `index.html`
- `docs/GUIDE_UTILISATEUR_FR_MG.md`
- `app/` (WebView Java et HTML embarqué)
- `build.gradle`, `settings.gradle`, `.github/workflows/android.yml`

## Vérifications et preuves
- `node --check` sur le JavaScript inline : réussi le 12/11/2026.
- Tentative d’ouverture Chromium via Playwright : bloquée par l’environnement d’exécution (`socket() failed: Operation not permitted`), donc parcours navigateur non validé visuellement.
- Premier run GitHub Actions échoué sur le paquet SDK obsolète `tools`; workflow corrigé pour utiliser le SDK préinstallé.
- GitHub Actions run #4 : réussi ; `assembleApi23Debug` et `assembleApi29Debug` réussis ; artefact Debug `PatissProMG-Debug-API23-API29` créé.
- Dépôt privé `RMLala/patisspro-mg` ; branche distante `work/patisspro-mvp-2026-11-12` issue de `main`; PR #1 ouverte et non fusionnée.
- Releases signées API23/API29 non produites : la tâche Release est réservée au workflow manuel/tag et aucun run Release n’a été déclenché.

## Limites / anomalies ouvertes
- Le stockage du prototype HTML utilise `localStorage`; migration IndexedDB/base Android à faire avant usage réel intensif.
- Les imports JSON sont structurellement contrôlés mais les sauvegardes ne sont pas chiffrées.
- La caisse, le stock et le calcul de marge sont MVP : pas de clôture de caisse complète, lots/FIFO, réservation de matière, coût de recette multi-niveaux, facture fiscale, PDF, multi-sites ou rapprochement financier.
- Authentification, rôles, Cloudflare Workers/D1, résolution de conflits, AppForge, MVola validé manuellement, Google Drive et secrets release restent à intégrer.
- L’icône/les ressources graphiques Android sont à finaliser.

## Trois prochaines actions prioritaires
1. Faire valider le périmètre V1.0 puis compléter les flux d’achat/réception, lots, recettes multi-niveaux et ordres de fabrication avec écritures de stock cohérentes.
2. Rattacher le projet à `RMLala/patisspro-mg`, créer la branche `work/patisspro-mvp-2026-11-12` depuis `main`, pousser les sources et préparer une PR sans fusion.
3. Vérifier/configurer les secrets de signature dans le dépôt, lancer le build Release autorisé par le workflow puis contrôler les APK signées API23/API29.
