# PâtissPro MG — Cahier des charges V1.0

**Produit :** application unique Premium & Pro pour les pâtisseries, boulangeries-pâtisseries, fabricants de gâteaux personnalisés, traiteurs sucrés et vendeurs de pâtisseries à Madagascar.  
**Langues :** français et malagasy. **Devise :** MGA. **Date :** 12 novembre 2026.  
**Statut :** spécifications validées pour le démarrage du MVP. Les modules cloud, paiement et Android restent des intégrations à réaliser et vérifier.

## 1. Objectifs et utilisateurs

Couvrir le cycle opérationnel Achats → Stocks → Recettes → Coûts → Commandes → Production → Ventes → Livraisons → Finances → Rentabilité. Le mode Premium vise un commerce indépendant ; le mode Pro ajoute plusieurs points de vente/ateliers, rôles, permissions, utilisateurs et consolidation. Les deux modes utilisent la même application et les mêmes données ; les accès et options Pro sont affichés clairement.

Rôles de départ : propriétaire/administrateur, responsable de production, vendeur/caisse, magasinier, livreur et consultation/finance. Toutes les opérations sensibles doivent garder auteur, date et référence.

## 2. Périmètre fonctionnel

### 2.1 Tableau de bord
KPI CA encaissé, commandes, dépenses, marge estimée et solde de caisse ; filtres jour/semaine/mois/année/période ; volumes par statut ; alertes de seuil, péremption et urgence ; rentabilité ventilée par produit, commande et canal. Les montants de marge sont identifiés comme estimations lorsqu'ils reposent sur un coût standard.

### 2.2 Catalogue, recettes et coûts
Fiches produit avec famille, variante, portion/taille, prix, photo et actif/inactif. Recette versionnée comportant ingrédients et sous-recettes, quantités normalisées, unités, étapes, rendement et pertes. Le recalcul de rendement multiplie chaque quantité par rendement demandé/rendement de référence. Coût matière = somme quantité normalisée × coût moyen de stock ; ajouter emballage, main-d'œuvre et charges paramétrées. Prix suggéré selon marge cible ; marge brute = prix − coût ; taux de marque = marge/prix. Toute modification conserve une version datée.

### 2.3 Achats et stocks
Articles matière, emballages, consommables et produits finis ; fournisseur, commande d'achat, réception partielle/totale, facture et règlement. Unités de base et conversions contrôlées (kg/g, L/mL, pièce/paquet/carton configurables). Lots, coût unitaire, date de péremption, inventaires, pertes, corrections avec motif. FIFO par lot pour suggérer la consommation. Besoins à acheter issus des ordres de fabrication et du stock disponible.

### 2.4 Clients et commandes
Client avec nom, téléphone, adresse, préférences et historique. Commande directe ou personnalisée : canal, articles, tailles, parfum, décoration, inscription, photo de référence, date/heure et lieu de retrait/livraison. Devis, remise autorisée, acompte, solde et reçu/facture. Statuts : brouillon, confirmée, à produire, en production, prête, livrée/retirée, annulée. Calendrier et bons imprimables/partageables.

### 2.5 Production
Ordres de fabrication liés à une ou plusieurs commandes ou au stock prévisionnel. Calcul des besoins selon rendement, contrôle de disponibilité, réservation distincte de la consommation, responsable, étapes, quantités produites, rebuts, pertes, lots et contrôle qualité. Une annulation libère les réservations ; une clôture enregistre consommation réelle et produit fini.

### 2.6 Caisse et ventes
Écran caisse multi-produits, quantités, remises, paiements en plusieurs fois et vente à crédit avec plafond/autorisation. Moyens paramétrables (espèces, MVola, Orange Money, Airtel Money, autres). Ticket, retour avec motif, ouverture/clôture de session et rapprochement théorique/réel. Une vente validée met à jour les encaissements et mouvements de stock sans double comptabilisation.

### 2.7 Livraison
Liste et planning retrait/livraison, livreur, adresse, frais, statut, preuve de réception et encaissement à la livraison. Le statut de livraison ne modifie pas deux fois la commande ni le paiement.

### 2.8 Finances et rapports
Recettes/dépenses catégorisées, créances clients, dettes fournisseurs, prévision et budget. Résultat estimé = ventes nettes − coûts directs − charges saisies. Filtres par période, activité, boutique et produit. Exports CSV/Excel compatibles et rapports PDF imprimables.

### 2.9 Paramètres, sécurité et guide
Identité commerciale, logo, MGA, format jj/mm/aaaa, catégories, tailles de police, thèmes clair/sombre, FR/MG, boutiques/ateliers/dépôts. Comptes, permissions minimales et journal d'audit. Données de démonstration supprimables sans toucher aux données réelles. Guide FR/MG intégré, sauvegarde/restauration chiffrée.

## 3. Architecture et données

- **Client offline-first :** HTML/CSS/JavaScript autonome pour le navigateur ; Android enveloppe WebView/Capacitor. Source de vérité locale durable (IndexedDB dans la version web ; base locale Android dans l'intégration finale). Le prototype MVP emploie localStorage et doit migrer vers IndexedDB avant données volumineuses.
- **Entités principales :** Organization, User, Role, Site, Warehouse, Customer, Supplier, Product, Recipe, RecipeVersion, Ingredient, UnitConversion, StockLot, StockMovement, Purchase, PurchaseLine, Order, OrderLine, Payment, ProductionOrder, ProductionStep, Delivery, CashSession, Expense, AuditEvent, SyncChange, License.
- **Clés :** UUID local, organization_id obligatoire, site_id facultatif, created_at/updated_at, deleted_at, revision, device_id. Montants entiers MGA ; quantités en décimal base-unit ; timestamps ISO 8601 UTC, affichage local.
- **Cloud :** API Cloudflare Workers + D1 ; authentification/autorisation serveur ; tenant isolation à chaque requête ; journal de changements idempotent avec cursor ; conflits avec stratégie explicite (mouvements financiers et stocks append-only, fiches maître révisionnées avec résolution et historique). TLS, rate limiting, validation d'entrée, audit, sauvegardes D1 et restauration documentée. Aucun secret côté client.
- **Google Drive :** option sauvegarde utilisateur après consentement OAuth ; chiffrement avant export ; rotation et confirmation de restauration. Drive ne sert pas de base transactionnelle/synchronisation.

## 4. Licences et paiement

Essai de 3 jours accordé seulement après validation serveur ; licences mensuelle, annuelle, à vie et éditeur. Vérification en ligne au lancement et périodique ; cache signé limité pour usage hors ligne, révocation appliquée à la prochaine vérification. MVola Madagascar : 034 85 874 58 ; client enregistre référence et preuve, activation seulement après validation manuelle dans AppForge Studio. Secrets, clés de signature et tokens exclusivement côté serveur/GitHub Secrets.

## 5. Non-fonctionnels

Responsive téléphone/tablette/PC ; saisie utilisable au tactile ; navigation clavier ; contraste accessible ; chargement du cœur sans réseau ; sauvegarde avant migration ; déduplication des opérations rejouées ; performances testées sur Android 6+ ; langues intégrales ; aucune donnée client envoyée sans autorisation. Le prototype ne traite pas de paiement MVola automatiquement.

## 6. Critères d'acceptation V1.0 / MVP

1. Créer, modifier et supprimer (avec confirmation) produit, recette, ingrédient, client et commande ; persistance après rechargement hors ligne.
2. Calculer un coût de recette et un prix conseillé depuis les articles renseignés.
3. Enregistrer réception et vente, refléter les mouvements et signaler stock négatif/rupture.
4. Enregistrer acompte/solde, déterminer le restant dû et alimenter le CA encaissé uniquement à hauteur des paiements.
5. Filtrer la liste des commandes par recherche/statut/date, modifier statut et imprimer un bon.
6. Exporter et restaurer une sauvegarde JSON ; restaurer après confirmation et valider le format.
7. Vérifier bascule FR/MG, mise en page mobile, et fermeture/réouverture sans perte de données.
8. Tests de sécurité : échapper les textes, refuser import JSON mal formé, aucune clé secrète dans le HTML, validation des montants et permissions côté serveur lors de l'intégration.

## 7. Découpage et hors périmètre du premier MVP

**MVP v0.1 :** interface responsive, dashboard, catalogue/recettes, matières et inventaire simplifié, commandes/clients/paiements, mouvements de caisse/dépenses, production et livraison en statuts, stockage local, sauvegarde JSON et guide.  
**Étape suivante :** conversions unitaires avancées, lots/FIFO, achats/fournisseurs complets, rôles, multi-sites, rapports Excel/PDF, sync Workers/D1, AppForge Cloud, sauvegarde chiffrée/Drive et Android signé. Ces intégrations ne sont pas réputées disponibles avant réalisation et preuves de tests.

## 8. Livraison et contrôle

Dépôt dédié RMLala/patisspro-mg visé ; branche unique par Work depuis main ; PR obligatoire, aucune fusion sans autorisation. Actions : lint/tests JS, builds Debug, Release API23 et API29 ; secrets via GitHub Actions ; `versionName` inchangé entre variantes et `versionCode` augmenté uniquement pour livraison distribuée. Livrables : HTML autonome, sources Android, APK Debug, deux APK Release signées, guide FR/MG, changelog et rapport de tests. Une APK n'est déclarée construite, signée, installée ou testée qu'avec preuve de build/installation correspondante.


## 9. Extension Premium — Phase 2 (12 novembre 2026)

Le lot Phase 2 approfondit le module recettes et coûts :

- Éditeur de recette avec lignes choisies dans le catalogue matière ou parmi les sous-recettes existantes ; quantité et unité sont saisies par ligne.
- Unités normalisées compatibles : kg/g, L/mL et pièce(s). Une unité inconnue n'est convertie qu'avec une unité strictement identique ; les dimensions incompatibles sont signalées.
- Calcul récursif du coût matière des sous-recettes, puis ajout de l'emballage, de la main-d'œuvre et des charges indirectes par lot.
- Affichage du coût total par lot, coût par portion et prix de vente suggéré à partir d'un taux de marge cible (formule : coût unitaire / (1 − taux cible)). Le prix conseillé reste indicatif.
- Ajustement proportionnel des besoins à un rendement souhaité et sauvegarde d'une version antérieure datée à chaque modification significative de la fiche.
- Détection côté client d'une tentative de boucle de sous-recette ; les anciens enregistrements sont chargés avec des valeurs par défaut compatibles.

Cette extension s'appuie encore sur la persistance locale du MVP. Elle ne remplace pas les achats avec fournisseurs, lots FIFO, droits multiutilisateurs, synchronisation Cloudflare, sauvegarde chiffrée ou intégration AppForge.
