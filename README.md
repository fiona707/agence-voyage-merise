# agence-voyage-merise
Projet MERISE – Agence de voyage (BUT Info R3.10)

## Dictionnaire de données
Le dictionnaire est structuré sous forme de tableau par entité :  
- Les clés sont précisées : Clé primaire et Clé étrangère.

---

### ETAPE 2
#### Epuration
Lors de l’étape d’épuration, les attributs redondants ou calculables ont été retiré comme "etat" dans VOYAGE et "statut" dans RESERVATION, afin d’éviter les incohérences.  
les noms et les types ont été harminisé pour plus de clarté (par exemple `id_client`, `VARCHAR` pour les chaînes, `DECIMAL(10,2)` pour les montants, `DATE` pour les dates).  
Un champ "adresse" a ete ajouté au CLIENT et  certains champs comme `telephone` restent facultatifs.  
Enfin, nous avons intégré les règles d’unicité issues du métier comme l’unicité des noms de ville (RG3), l’unicité de l’hôtel par ville (RG2) et l’unicité des emails pour CLIENT et ACCOMPAGNATEUR. 

 ---
### ETAPE 3

Dans cette étape, nous avons enrichi le dictionnaire de données de l’agence de voyage en précisant les contraintes et les dépendances fonctionnelles.  
 Les dépendances fonctionnelles ont été établies afin de montrer quels attributs sont déterminés par la clé primaire ou par une clé candidate. Par exemple, dans CLIENT :  
id_client > nom, prenom, email, telephone, adresse et email > id_client.  


