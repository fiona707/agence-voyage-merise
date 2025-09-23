# Dictionnaire de données – Agence de voyage
 
---
 
## CLIENT
 
| Entité | Attribut   | Type     | Longueur | Clé           | Description |
|--------|------------|----------|----------|---------------|-------------|
| CLIENT | id_client  | INT      | —        | Clé primaire  | Identifiant unique du client |
| CLIENT | nom        | VARCHAR  | 100      | —             | Nom du client |
| CLIENT | prenom     | VARCHAR  | 100      | —             | Prénom du client |
| CLIENT | email      | VARCHAR  | 255      | Unique        | Email du client (doit être unique) |
| CLIENT | telephone  | VARCHAR  | 20       | —             | Numéro de téléphone (optionnel) |
| CLIENT | adresse    | VARCHAR  | 255      | —             | Adresse postale (optionnel) |
---
 
## VILLE
 
| Entité | Attribut   | Type     | Longueur | Clé           | Description |
|--------|------------|----------|----------|---------------|-------------|
| VILLE  | id_ville   | INT      | —        | Clé primaire  | Identifiant unique de la ville |
| VILLE  | nom_ville  | VARCHAR  | 150      | Unique        | Nom distinct de la ville (RG3) |
| VILLE  | pays       | VARCHAR  | 100      | —             | Pays de la ville |
---
 
## HOTEL
 
| Entité | Attribut   | Type     | Longueur | Clé                | Description |
|--------|------------|----------|----------|--------------------|-------------|
| HOTEL  | id_hotel   | INT      | —        | Clé primaire       | Identifiant unique de l’hôtel |
| HOTEL  | id_ville   | INT      | —        | Clé étrangère, Unique | Ville de l’hôtel (1 hôtel par ville – RG2) |
| HOTEL  | nom_hotel  | VARCHAR  | 150      | —                  | Nom de l’hôtel |
| HOTEL  | categorie  | INT      | —        | —                  | Catégorie (1 à 5 étoiles) | 
---
 
## CIRCUIT
 
| Entité  | Attribut     | Type     | Longueur | Clé           | Description |
|---------|--------------|----------|----------|---------------|-------------|
| CIRCUIT | id_circuit   | INT      | —        | Clé primaire  | Identifiant unique du circuit |
| CIRCUIT | nom_circuit  | VARCHAR  | 150      | —             | Nom du circuit |
| CIRCUIT | description  | TEXT     | —        | —             | Description du circuit |
---
 
## ETAPE_CIRCUIT
 
| Entité        | Attribut   | Type | Longueur | Clé                           | Description      |
|---------------|------------|------|----------|-------------------------------|------------------|
| ETAPE_CIRCUIT | id_circuit | INT  | —        | Clé primaire, Clé étrangère   | Circuit concerné |
| ETAPE_CIRCUIT | ordre      | INT  | —        | Clé primaire                  | Numéro d’étape (1,2,3,…) |
| ETAPE_CIRCUIT | id_ville   | INT  | —        | Clé étrangère               | Ville visitée |
| ETAPE_CIRCUIT | nb_nuits   | INT  | —        | —                                     | Nombre de nuits (≥ 1) |
---
 
## ACCOMPAGNATEUR
 
| Entité          | Attribut    | Type     | Longueur | Clé           | Description |
|-----------------|-------------|----------|----------|---------------|-------------|
| ACCOMPAGNATEUR  | id_accomp   | INT      | —        | Clé primaire  | Identifiant unique de l’accompagnateur |
| ACCOMPAGNATEUR  | nom         | VARCHAR  | 100      | —             | Nom |
| ACCOMPAGNATEUR  | prenom      | VARCHAR  | 100      | —             | Prénom |
| ACCOMPAGNATEUR  | email       | VARCHAR  | 255      | Unique        | Email (doit être unique) |
| ACCOMPAGNATEUR  | telephone   | VARCHAR  | 20       | —             | Téléphone (optionnel) |
---
 
## VOYAGE
 
| Entité | Attribut          | Type    | Longueur | Clé           | Description |
|--------|-------------------|---------|----------|---------------|-------------|
| VOYAGE | id_voyage         | INT     | —        | Clé primaire  | Identifiant unique du voyage |
| VOYAGE | id_circuit        | INT     | —        | Clé étrangère | Circuit exécuté |
| VOYAGE | date_depart       | DATE    | —        | —             | Date de départ |
| VOYAGE | date_arrivee      | DATE    | —        | —             | Date d’arrivée |
| VOYAGE | ville_depart_id   | INT     | —        | Clé étrangère | Ville de départ |
| VOYAGE | ville_arrivee_id  | INT     | —        | Clé étrangère | Ville d’arrivée |
| VOYAGE | id_accomp         | INT     | —        | Clé étrangère | Accompagnateur (un seul par voyage – RG4) |
| VOYAGE | capacite          | INT     | —        | —             | Nombre total de places |
| VOYAGE | d1_limite_acompte | DATE    | —        | —             | Date limite acompte (D1 – RG13) |
| VOYAGE | d2_limite_solde   | DATE    | —        | —             | Date limite solde (D2 – RG14) |
---
 
## RESERVATION
 
| Entité      | Attribut      | Type     | Longueur | Clé           | Description |
|-------------|---------------|----------|----------|---------------|-------------|
| RESERVATION | id_resa       | INT      | —        | Clé primaire  | Identifiant unique de la réservation |
| RESERVATION | id_voyage     | INT      | —        | Clé étrangère | Voyage lié |
| RESERVATION | id_client     | INT      | —        | Clé étrangère | Client qui réserve |
| RESERVATION | nb_places     | INT      | —        | —             | Nombre de places réservées |
| RESERVATION | date_demande  | DATE     | —        | —             | Date de la demande |
| RESERVATION | montant_total | DECIMAL  | 10,2     | —             | Prix total prévu | 
---
 
## PAIEMENT

| Entité  | Attribut      | Type     | Longueur | Clé           | Description |
|---------|---------------|----------|----------|---------------|-------------|
| PAIEMENT| id_paiement   | INT      | —        | Clé primaire  | Identifiant unique du paiement |
| PAIEMENT| id_resa       | INT      | —        | Clé étrangère | Réservation liée |
| PAIEMENT| type          | VARCHAR  | 20       | —             | Type de paiement : acompte / solde / remboursement |
| PAIEMENT| date_paiement | DATE     | —        | —             | Date du paiement |
| PAIEMENT| montant       | DECIMAL  | 10,2     | —             | Montant payé |
---
 
