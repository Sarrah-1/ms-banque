# TP 8 : Spring @RestController — ms-banque

API REST de gestion de comptes bancaires avec Spring Boot 3, Spring Data JPA et une base H2 en mémoire.
Les réponses sont disponibles en **JSON** et en **XML**, et l'API est documentée avec **Swagger UI**.

## Structure du projet

```
ms-banque
├── pom.xml
└── src/main
    ├── java/ma/rest/spring
    │   ├── MsBanqueApplication.java        # classe principale + données initiales
    │   ├── controllers/CompteController.java
    │   ├── entities/Compte.java
    │   ├── entities/TypeCompte.java        # COURANT, EPARGNE
    │   └── repositories/CompteRepository.java
    └── resources/application.properties
```

## Modèle de données

`Compte` :

| Champ | Type | Remarque |
|---|---|---|
| `id` | Long | généré automatiquement |
| `solde` | double | |
| `dateCreation` | Date | date seule, sans heure |
| `type` | TypeCompte | `COURANT` ou `EPARGNE` (stocké en texte) |

## Exemples de requêtes (curl)

Lister les comptes en JSON :

```bash
curl -X GET "http://localhost:8082/banque/comptes" -H "Accept: application/json"
```

Lister les comptes en XML :

```bash
curl -X GET "http://localhost:8082/banque/comptes" -H "Accept: application/xml"
```

Créer un compte en JSON :

```bash
curl -X POST "http://localhost:8082/banque/comptes" \
  -H "Content-Type: application/json" \
  -d '{"solde": 1500.0, "dateCreation": "2024-11-01", "type": "COURANT"}'
```

Créer un compte en XML :

```bash
curl -X POST "http://localhost:8082/banque/comptes" \
  -H "Content-Type: application/xml" \
  -d '<Compte><solde>1500.0</solde><dateCreation>2024-11-01</dateCreation><type>COURANT</type></Compte>'
```

Modifier le compte 1 :

```bash
curl -X PUT "http://localhost:8082/banque/comptes/1" \
  -H "Content-Type: application/json" \
  -d '{"solde": 2000.0, "dateCreation": "2024-11-01", "type": "EPARGNE"}'
```

Supprimer le compte 1 :

```bash
curl -X DELETE "http://localhost:8082/banque/comptes/1"
```

Ces requêtes peuvent aussi être testées avec Postman, SoapUI ou directement depuis Swagger UI.

## Captures d'écran

### Console H2

<img width="706" height="281" alt="image" src="https://github.com/user-attachments/assets/97920502-0a98-408a-b55e-8754723a587c" />

### Swagger UI

<img width="880" height="365" alt="image" src="https://github.com/user-attachments/assets/c46a37f5-aa21-4358-ba06-2d7031a8ff55" />

### GET /banque/comptes en JSON

<img width="822" height="352" alt="image" src="https://github.com/user-attachments/assets/04c0b73a-41f7-4645-8540-da91b580ca1e" />

### GET /banque/comptes en XML
<img width="832" height="326" alt="image" src="https://github.com/user-attachments/assets/7ba6165e-d76e-4d6e-b70d-2027586d33fb" />

- Le projet utilise Spring Boot 3, donc les imports JPA sont en `jakarta.persistence.*` (et non `javax.persistence.*`).
- L'élément racine XML est `<Compte>` (nom de la classe).
- Pour changer le port, modifier `server.port` dans `application.properties`.
