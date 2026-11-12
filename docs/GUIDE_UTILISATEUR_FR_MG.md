# Guide utilisateur — PâtissPro MG v0.1.0

## Français

### Démarrer
Ouvrez `index.html` dans un navigateur. Créez un produit dans **Produits & recettes**, puis saisissez les ingrédients et seuils dans **Stocks**. L’application conserve les données dans le stockage local du navigateur.

### Enregistrer une commande
Ouvrez **Commandes → Ajouter**. Renseignez référence, client, date prévue, produit, montant total, acompte, statut, canal et lieu de remise. Le tableau affiche le montant payé et le statut. Les paiements entrés ici contribuent aux encaissements du tableau de bord.

### Suivre le stock
Dans **Stocks**, ajoutez chaque matière avec quantité, coût par unité et seuil. Le badge « À commander » apparaît lorsque la quantité disponible atteint le seuil. **＋ Stock** enregistre une réception. Les réceptions d’ingrédients sont journalisées localement.

### Suivre la fabrication et les remises
Dans **Production**, ajoutez un ordre puis utilisez « Étape suivante » pour avancer de Planifiée à En cours, Prête, puis Clôturée. Dans **Livraisons**, « Confirmer remise » marque la commande livrée ; l’application demande confirmation si le solde reste dû.

### Ventes et dépenses
**Caisse & finances → Nouvelle vente** calcule le montant à partir du prix unitaire et de la quantité, puis diminue le stock si le produit existe au catalogue. Ajoutez les dépenses dans le journal. Les indicateurs de résultat restent estimatifs : les charges indirectes non saisies et la valorisation complète de stock ne sont pas calculées.

### Sauvegarder / restaurer
Dans **Paramètres**, exportez une sauvegarde JSON ou les commandes en CSV. Pour restaurer, choisissez un JSON exporté depuis PâtissPro MG. La restauration remplace le stockage local après confirmation. Les JSON de ce MVP ne sont pas chiffrés. Évitez les appareils partagés et conservez une copie sûre.

### Langue et démonstration
Le bouton MG/FR change l’interface. Pour effacer les données et repartir de l’exemple initial, utilisez **Effacer les données démo**. Faites une sauvegarde avant cette action.

## Malagasy

### Fanombohana
Sokafy amin’ny navigateur ny `index.html`. Ampidiro ao amin’ny **Vokatra sy recette** ny vokatra, ary ao amin’ny **Tahiry** ny akora sy ny fetra. Tehirizina eto amin’ny navigateur ny angona.

### Fampidirana baiko
Ao amin’ny **Baiko → Hanampy**, soraty ny laharana, anaran’ny mpanjifa, daty ilaina, vokatra, totalim-bola, vola efa voaloa, sata ary fomba fanaterana. Tafiditra amin’ny vola miditra aseho ny vola efa noraisina.

### Tahiry
Ampidiro ao amin’ny **Tahiry** ny akora, habetsany, vidiny isaky ny vondrona ary fetra. Miseho ny fampitandremana rehefa latsaka na mitovy amin’ny fetra ny tahiry. Ny bokotra **＋ Stock** dia mirakitra fandraisana entana.

### Famokarana sy fanaterana
Ao amin’ny **Famokarana**, mamoròna baiko famokarana ary tsindrio **Dingana manaraka** hanovana ny sata. Ao amin’ny **Fanaterana**, hamafiso ny fanomezana ny baiko; hangataka fanamafisana ny app raha mbola misy vola tsy voaloa.

### Varotra sy fandaniana
Ao amin’ny **Vola sy fandaniana**, ny varotra vaovao dia mampihena ny tahiry raha misy ilay vokatra, ary ampidirina ao amin’ny vola miditra. Soraty misaraka ny fandaniana. Tombana ihany ny vokatra satria mbola tsy tafiditra ny fandaniana rehetra.

### Tahiry angona
Ao amin’ny **Fikirana**, avoahy JSON ny tahiry na CSV ny baiko. Rehefa averina ny JSON dia soloina ny angona eo an-toerana rehefa voamarina. Tsy mbola voaaro amin’ny chiffrement ny JSON amin’ity MVP ity. Tehirizo amin’ny toerana azo antoka.

### Fiteny sy santionany
Tsindrio ny bokotra MG/FR hanovana fiteny. Ampiasao **Fafao ny santionany** raha te hiverina amin’ny angona ohatra; manaova tahiry aloha.
