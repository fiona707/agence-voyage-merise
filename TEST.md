
## CLIENT
| Entité | Attribut   | Type     | Longueur | Clé     | Description |
|--------|------------|----------|----------|---------|-------------|
| CLIENT | id_client  | INT      | —        | clé primaire    | Identifiant unique client |
| CLIENT | nom        | VARCHAR  | 100      | —       | Nom du client |
| CLIENT | prenom     | VARCHAR  | 100      | —       | Prénom du client |
| CLIENT | email      | VARCHAR  | 255      | Unique  | Email du client |
| CLIENT | telephone  | VARCHAR  | 20       | —       | Numéro de téléphone |

---

## VILLE
| Entité | Attribut   | Type     | Longueur | Clé     | Description |
|--------|------------|----------|----------|---------|-------------|
| VILLE  | id_ville   | INT      | —        | clé primaire     | Identifiant unique ville |
| VILLE  | nom_ville  | VARCHAR  | 150      | Unique  | Nom distinct de la ville |
| VILLE  | pays       | VARCHAR  | 100      | —       | Pays de la ville |

---

## HOTEL
| Entité | Attribut   | Type     | Longueur | Clé            | Description |
|--------|------------|----------|----------|----------------|-------------|
| HOTEL  | id_hotel   | INT      | —        | clé primaire        | Identifiant hôtel |
| HOTEL  | id_ville   | INT      | —        | clé etrangère : ville  | Ville où se trouve l’hôtel (1 hôtel par ville) |
| HOTEL  | nom_hotel  | VARCHAR  | 150      | —              | Nom de l’hôtel |
| HOTEL  | categorie  | INT      | —        | —              | Catégorie (1 à 5 étoiles) |

---

## CIRCUIT
| Entité  | Attribut     | Type     | Longueur | Clé     | Description |
|---------|--------------|----------|----------|---------|-------------|
| CIRCUIT | id_circuit   | INT      | —        | clé primaire  | Identifiant circuit |
| CIRCUIT | nom_circuit  | VARCHAR  | 150      | —       | Nom du circuit |
| CIRCUIT | description  | TEXT     | —        | —       | Description |

---

## ETAPE_CIRCUIT
| Entité        | Attribut   | Type | Longueur | Clé                          | Description |
|---------------|------------|------|----------|------------------------------|-------------|
| ETAPE_CIRCUIT | id_circuit | INT  | —        | **PK(part1), FK→CIRCUIT**    | Circuit concerné |
| ETAPE_CIRCUIT | ordre      | INT  | —        | **PK(part2)**                | Numéro d’étape (1,2,3,…) |
| ETAPE_CIRCUIT | id_ville   | INT  | —        | **FK→VILLE**                 | Ville visitée |
| ETAPE_CIRCUIT | nb_nuits   | INT  | —        | —                            | Nombre de nuits (≥1) |

---

## ACCOMPAGNATEUR
| Entité        | Attribut    | Type     | Longueur | Clé     | Description |
|---------------|-------------|----------|----------|---------|-------------|
| ACCOMPAGNATEUR| id_accomp   | INT      | —        | **PK**  | Identifiant accompagnateur |
| ACCOMPAGNATEUR| nom         | VARCHAR  | 100      | —       | Nom |
| ACCOMPAGNATEUR| prenom      | VARCHAR  | 100      | —       | Prénom |
| ACCOMPAGNATEUR| email       | VARCHAR  | 255      | Unique  | Email |
| ACCOMPAGNATEUR| telephone   | VARCHAR  | 20       | —       | Téléphone |

---

## VOYAGE
| Entité | Attribut          | Type    | Longueur | Clé                      | Description |
|--------|------------------|---------|----------|--------------------------|-------------|
| VOYAGE | id_voyage        | INT     | —        | **PK**                   | Identifiant voyage |
| VOYAGE | id_circuit       | INT     | —        | **FK→CIRCUIT**           | Circuit exécuté |
| VOYAGE | date_depart      | DATE    | —        | —                        | Date de départ |
| VOYAGE | date_arrivee     | DATE    | —        | —                        | Date d’arrivée |
| VOYAGE | ville_depart_id  | INT     | —        | **FK→VILLE**             | Ville de départ |
| VOYAGE | ville_arrivee_id | INT     | —        | **FK→VILLE**             | Ville d’arrivée |
| VOYAGE | id_accomp        | INT     | —        | **FK→ACCOMPAGNATEUR**    | Accompagnateur |
| VOYAGE | capacite         | INT     | —        | —                        | Nombre total de places |
| VOYAGE | d1_limite_acompte| DATE    | —        | —                        | Date limite acompte (D1) |
| VOYAGE | d2_limite_solde  | DATE    | —        | —                        | Date limite solde (D2) |
| VOYAGE | etat             | ENUM    | —        | —                        | Prévu / Confirmé / Annulé |

---

## RESERVATION
| Entité     | Attribut       | Type     | Longueur | Clé                  | Description |
|------------|----------------|----------|----------|----------------------|-------------|
| RESERVATION| id_resa        | INT      | —        | **PK**               | Identifiant réservation |
| RESERVATION| id_voyage      | INT      | —        | **FK→VOYAGE**        | Voyage lié |
| RESERVATION| id_client      | INT      | —        | **FK→CLIENT**        | Client qui réserve |
| RESERVATION| nb_places      | INT      | —        | —                    | Nombre de places |
| RESERVATION| statut         | ENUM     | —        | —                    | en_attente / acompte_versé / définitive / annulée |
| RESERVATION| date_demande   | DATE     | —        | —                    | Date de demande |
| RESERVATION| montant_total  | DECIMAL  | —        | —                    | Prix total prévu |

---

## PAIEMENT
| Entité  | Attribut      | Type     | Longueur | Clé              | Description |
|---------|---------------|----------|----------|------------------|-------------|
| PAIEMENT| id_paiement   | INT      | —        | **PK**           | Identifiant paiement |
| PAIEMENT| id_resa       | INT      | —        | **FK→RESERVATION**| Réservation liée |
| PAIEMENT| type          | ENUM     | —        | —                | acompte / solde / remboursement |
| PAIEMENT| date_paiement | DATE     | —        | —                | Date du paiement |
| PAIEMENT| montant       | DECIMAL  | —        | —                | Montant payé |


## misbaou
| Entité  | Attribut      | Type     | Longueur | Clé              | Description |
|---------|---------------|----------|----------|------------------|-------------|
|  misbaou|    personne   | homme    |    175cm |      pk          | from africa  |
