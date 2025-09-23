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

**Contraintes**   
Clé primaire = id_client ; email obligatoire et unique ; nom et prénom obligatoires ; téléphone et adresse facultatifs  

**Dépendances fonctionnelles** 
id_client > nom, prenom, email, telephone, adresse
email > id_client

---
 
## VILLE
 
| Entité | Attribut   | Type     | Longueur | Clé           | Description |
|--------|------------|----------|----------|---------------|-------------|
| VILLE  | id_ville   | INT      | —        | Clé primaire  | Identifiant unique de la ville |
| VILLE  | nom_ville  | VARCHAR  | 150      | Unique        | Nom distinct de la ville (RG3) |
| VILLE  | pays       | VARCHAR  | 100      | —             | Pays de la ville |

**Contraintes**  
Clé primaire = id_ville ; nom_ville obligatoire et unique ; pays obligatoire  

**Dépendances fonctionnelles**  
id_ville > nom_ville, pays  
nom_ville > id_ville  

---
 
## HOTEL
 
| Entité | Attribut   | Type     | Longueur | Clé                | Description |
|--------|------------|----------|----------|--------------------|-------------|
| HOTEL  | id_hotel   | INT      | —        | Clé primaire       | Identifiant unique de l’hôtel |
| HOTEL  | id_ville   | INT      | —        | Clé étrangère, Unique | Ville de l’hôtel (1 hôtel par ville – RG2) |
| HOTEL  | nom_hotel  | VARCHAR  | 150      | —                  | Nom de l’hôtel |
| HOTEL  | categorie  | INT      | —        | —                  | Catégorie (1 à 5 étoiles) | 

**Contraintes**  
Clé primaire = id_hotel ; clé étrangère = id_ville ; un hôtel par ville (unique sur id_ville) ; catégorie entre 1 et 5  

**Dépendances fonctionnelles**  
id_hotel > id_ville, nom_hotel, categorie  
id_ville > id_hotel  

---
 
## CIRCUIT
 
| Entité  | Attribut     | Type     | Longueur | Clé           | Description |
|---------|--------------|----------|----------|---------------|-------------|
| CIRCUIT | id_circuit   | INT      | —        | Clé primaire  | Identifiant unique du circuit |
| CIRCUIT | nom_circuit  | VARCHAR  | 150      | —             | Nom du circuit |
| CIRCUIT | description  | TEXT     | —        | —             | Description du circuit |

**Contraintes**  
Clé primaire = id_circuit ; nom obligatoire ; doit inclure au moins deux villes (RG6 – contrôle applicatif)  

**Dépendances fonctionnelles**  
id_circuit > nom_circuit, description 

---
 
## ETAPE_CIRCUIT
 
| Entité        | Attribut   | Type | Longueur | Clé                                   | Description |
|---------------|------------|------|----------|---------------------------------------|-------------|
| ETAPE_CIRCUIT | id_circuit | INT  | —        | Clé primaire, Clé étrangère | Circuit concerné |
| ETAPE_CIRCUIT | ordre      | INT  | —        | Clé primaire              | Numéro d’étape (1,2,3,…) |
| ETAPE_CIRCUIT | id_ville   | INT  | —        | Clé étrangère                         | Ville visitée |
| ETAPE_CIRCUIT | nb_nuits   | INT  | —        | —                                     | Nombre de nuits (≥ 1) |

**Contraintes**  
Clé primaire = (id_circuit, ordre) ; clé étrangère = id_ville ; nb_nuits ≥ 1 ; au moins deux étapes par circuit  

**Dépendances fonctionnelles**  
(id_circuit, ordre) > id_ville, nb_nuits 

---
 
## ACCOMPAGNATEUR
 
| Entité          | Attribut    | Type     | Longueur | Clé           | Description |
|-----------------|-------------|----------|----------|---------------|-------------|
| ACCOMPAGNATEUR  | id_accomp   | INT      | —        | Clé primaire  | Identifiant unique de l’accompagnateur |
| ACCOMPAGNATEUR  | nom         | VARCHAR  | 100      | —             | Nom |
| ACCOMPAGNATEUR  | prenom      | VARCHAR  | 100      | —             | Prénom |
| ACCOMPAGNATEUR  | email       | VARCHAR  | 255      | Unique        | Email (doit être unique) |
| ACCOMPAGNATEUR  | telephone   | VARCHAR  | 20       | —             | Téléphone (optionnel) |

**Contraintes**  
Clé primaire = id_accomp ; email obligatoire et unique ; nom et prénom obligatoires  

**Dépendances fonctionnelles**  
id_accomp > nom, prenom, email, telephone  
email > id_accomp

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

**Contraintes**  
Clé primaire = id_voyage ; clés étrangères = id_circuit, ville_depart_id, ville_arrivee_id, id_accomp ; départ différent de l’arrivée ; unique (date_depart, ville_depart_id) et (date_arrivee, ville_arrivee_id) (RG8) ; capacité ≥ 1  

**Dépendances fonctionnelles**  
id_voyage > id_circuit, date_depart, date_arrivee, ville_depart_id, ville_arrivee_id, id_accomp, capacite, d1_limite_acompte, d2_limite_solde 

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

**Contraintes**  
Clé primaire = id_resa ; clés étrangères = id_voyage, id_client ; nb_places ≥ 1 ; montant_total ≥ 0  

**Dépendances fonctionnelles**  
id_resa > id_voyage, id_client, nb_places, date_demande, montant_total 

---
 
## PAIEMENT

| Entité  | Attribut      | Type     | Longueur | Clé           | Description |
|---------|---------------|----------|----------|---------------|-------------|
| PAIEMENT| id_paiement   | INT      | —        | Clé primaire  | Identifiant unique du paiement |
| PAIEMENT| id_resa       | INT      | —        | Clé étrangère | Réservation liée |
| PAIEMENT| type          | VARCHAR  | 20       | —             | Type de paiement : acompte / solde / remboursement |
| PAIEMENT| date_paiement | DATE     | —        | —             | Date du paiement |
| PAIEMENT| montant       | DECIMAL  | 10,2     | —             | Montant payé |

**Contraintes**  
Clé primaire = id_paiement ; clé étrangère = id_resa ; type ∈ {acompte, solde, remboursement} ; montant ≥ 0  

**Dépendances fonctionnelles**  
id_paiement > id_resa, type, date_paiement, montant  

 
