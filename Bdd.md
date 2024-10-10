Voici une version du schéma de la base de données, avec les types de données précisés pour chaque colonne :

### 1. **Table `brands` (Marques)**

- **id** (PK) : `SERIAL` — Identifiant unique de la marque.
- **name** : `VARCHAR(255)` — Nom de la marque (ex : Ann Demeulemeester, Rick Owens).
- **description** : `TEXT` — Brève description de la marque.
- **country** : `VARCHAR(100)` — Pays d'origine de la marque.
- **founded_year** : `INTEGER` — Année de création de la marque.
- **website_url** : `VARCHAR(255)` — URL du site officiel.
- **logo** : `VARCHAR(255)` — URL de l’image du logo de la marque.
- **tags** : `TEXT[]` — Tableau de tags associés à la marque (ex : gothique, avant-garde).
- **theme** : `VARCHAR(100)` — Thème ou esthétique de la marque (ex : minimaliste, industriel).

### 2. **Table `products` (Produits)**

- **id** (PK) : `SERIAL` — Identifiant unique du produit.
- **brand_id** (FK) : `INTEGER` — Référence à l’identifiant de la marque dans `brands`.
- **name** : `VARCHAR(255)` — Nom du produit.
- **price** : `NUMERIC(10, 2)` — Prix du produit.
- **description** : `TEXT` — Description du produit.
- **image_url** : `VARCHAR(255)` — URL de l’image du produit.
- **purchase_url** : `VARCHAR(255)` — URL vers la page d’achat du produit.
- **scraped_at** : `TIMESTAMP` — Date et heure du scraping.
- **available** : `BOOLEAN` — Indique si le produit est toujours disponible.
- **source** : `VARCHAR(100)` — Source de la donnée (ex : Vestiaire Collective).

### 3. **Table `brand_associations` (Associations esthétiques)**

- **id** (PK) : `SERIAL` — Identifiant unique de l'association.
- **brand_id_1** (FK) : `INTEGER` — Référence à une première marque (liée à `brands`).
- **brand_id_2** (FK) : `INTEGER` — Référence à la seconde marque associée.
- **similarity_score** : `DECIMAL(3, 2)` — Score de similarité esthétique entre les deux marques (0.00 à 1.00).

### 4. **Table `images_search` (Recherche d’images)**

- **id** (PK) : `SERIAL` — Identifiant unique de la recherche.
- **user_id** (FK) : `INTEGER` — Référence à l’utilisateur ayant soumis l’image (optionnel).
- **image_url** : `VARCHAR(255)` — URL de l’image soumise pour la recherche.
- **search_results** : `JSONB` — Résultats de la recherche d'image sous forme de JSON (produits correspondants).
- **searched_at** : `TIMESTAMP` — Date et heure de la recherche.

### 5. **Table `brand_tags` (Tags des marques)**

- **id** (PK) : `SERIAL` — Identifiant unique.
- **brand_id** (FK) : `INTEGER` — Référence à la marque dans `brands`.
- **tag** : `VARCHAR(100)` — Nom du tag (ex : avant-garde, minimalisme).

### 6. **Table `users` (Utilisateurs)**

- **id** (PK) : `SERIAL` — Identifiant unique de l’utilisateur.
- **username** : `VARCHAR(150)` — Nom d’utilisateur.
- **email** : `VARCHAR(255)` — Adresse e-mail.
- **password_hash** : `VARCHAR(255)` — Hash du mot de passe.
- **created_at** : `TIMESTAMP` — Date de création du compte.
- **last_login** : `TIMESTAMP` — Date de dernière connexion.

### 7. **Table `user_preferences` (Préférences des utilisateurs)**

- **id** (PK) : `SERIAL` — Identifiant unique.
- **user_id** (FK) : `INTEGER` — Référence à l’utilisateur.
- **brand_id** (FK) : `INTEGER` — Référence à la marque favorite de l’utilisateur.
- **search_history** : `TEXT` — Historique des recherches de l’utilisateur.
- **created_at** : `TIMESTAMP` — Date et heure de la création de la préférence.

---

### Optimisations supplémentaires :

- **Indexation** :
  - `name` dans `brands` et `products` doit être indexé pour les recherches rapides.
  - Index sur `tags` pour la table `brand_tags`.
  - Index sur `brand_id_1` et `brand_id_2` pour optimiser les requêtes sur les associations esthétiques.

Ce schéma structuré facilite la gestion des relations entre les marques, produits, recherches et utilisateurs tout en gardant une flexibilité pour les futures extensions du projet.
