# AccessFlow
# AccessFlow

AccessFlow automatise le traitement des demandes d'accès reçues par email, du premier message jusqu'à la création du compte utilisateur.
C'est une réplique personnelle d'un projet professionnel : toutes les briques tournent sur des données et des systèmes simulés (une boîte mail de test, des documents générés, une application web fictive), pour pouvoir construire et tester chaque composant avant de l'adapter à un environnement réel.

## Fonctionnement

Une demande passe par sept étapes. Chaque étape a un point d'entrée unique, gère ses propres cas (pièce jointe manquante, formulaire incomplet, demande complémentaire...) et se termine sur une sortie unique, où le registre des demandes est mis à jour.

| # | Étape | Technique principale | État |
|---|-------|----------------------|------|
| 1 | Réception et classification du mail | LLM | En cours |
| 2 | Contrôle du formulaire signé (cachet, signature, nom de la concession) | Computer Vision, OCR | Prévu |
| 3 | Contrôle du fichier de données utilisateur | Règles sur données structurées | Prévu |
| 4 | Préparation du fichier d'import | Traitement de données | Prévu |
| 5 | Import de l'utilisateur dans l'application web | Automatisation web | Prévu |
| 6 | Contrôle du résultat de l'import | Automatisation web | Prévu |
| 7 | Réponse au demandeur | Modèles de mails | Prévu |

Les étapes sont orchestrées avec LangGraph. Un registre garde la trace de chaque demande et de l'étape où elle s'est arrêtée. Il permet aussi de reconnaître une demande complémentaire pour un utilisateur déjà connu.

## Partie 1 : classification des emails

Pour chaque mail reçu, un LLM open source exécuté en local détermine s'il s'agit d'une demande d'accès et extrait les informations utiles aux étapes suivantes.

```json
{
  "is_access_request": true,
  "request_type": "new",
  "company": "Concession A",
  "users": ["Julie Martin"]
}
```

Plusieurs modèles sont comparés sur le même jeu de test étiqueté, avec le même prompt et le même schéma de sortie. La comparaison porte sur la qualité de classification (precision, recall, F1), l'exactitude de chaque champ extrait, la part de sorties valides, la vitesse et la mémoire utilisée.

## Données

Tous les mails, documents, noms et concessions de ce dépôt sont fictifs.

## État du projet

En cours. La partie 1 est en développement ; les autres étapes seront ajoutées une par une.