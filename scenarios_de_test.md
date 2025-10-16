# Scénarios de Test Manuels — Module de Gestion de Projets

## Gestion des Projets

**T-PROJ-01 : Création de projet**  
Étapes :  
1. Se connecter en tant que chef de projet.  
2. Ouvrir le formulaire de création.  
3. Remplir les champs obligatoires.  
4. Soumettre le formulaire.  
Résultat attendu : le projet est créé et visible dans la liste.  
Critère de validation : le projet est enregistré et une notification est reçue par le chef de projet.  

**T-PROJ-02 : Dates incohérentes**  
Étapes : créer un projet avec une date de début supérieure à la date de fin.  
Résultat attendu : message d’erreur de validation.  
Critère de validation : aucun projet n’est créé.  

**T-PROJ-03 : Dépassement du budget**  
Étapes : créer un projet puis ajouter des tâches qui dépassent le budget total du projet.  
Résultat attendu : une alerte est générée.  
Critère de validation : un message d’erreur s’affiche.  

## Planification des Tâches

**T-TASK-01 : Limite d’assignation**  
Étapes : affecter un même utilisateur à 4 tâches actives dans le même projet.  
Résultat attendu : la 4e assignation est refusée.  
Critère de validation : un message d’erreur est affiché.  

**T-TASK-02 : Dépendance**  
Étapes : créer une tâche B dépendante de la tâche A, puis modifier les dates de A.  
Résultat attendu : message d’erreur ou ajustement automatique des dates.  
Critère de validation : aucune incohérence dans les dépendances.  

**T-TASK-03 : Commentaires**  
Étapes : ajouter un commentaire sur une tâche existante.  
Résultat attendu : le commentaire s’affiche avec l’auteur et la date.  
Critère de validation : affichage correct du commentaire.  

## Suivi des Performances

**T-DASH-01 : Calcul du pourcentage d’avancement**  
Étapes : créer trois tâches dont une terminée.  
Résultat attendu : le pourcentage d’avancement du projet est calculé et affiché correctement.  
Critère de validation : la valeur affichée correspond aux tâches terminées.  

**T-ALERT-01 : Dépassement de budget**  
Étapes : enregistrer un coût réel supérieur au coût estimé.  
Résultat attendu : une notification est envoyée au chef de projet.  
Critère de validation : l’alerte est reçue.  

## Zones de Risque Potentielles

Dépendances : risque de boucle ou blocage.  
  Test par création de dépendances en chaîne.  
Affectations : risque d’erreurs simultanées.  
  Test de plusieurs assignations en même temps.  
Budget : risque de calcul incorrect.  
  Test avec valeurs extrêmes et dépassement de seuil.  
Notifications : risque de doublon ou absence d’envoi.  
  Vérification dans les journaux système.  
Sécurité : risque de fichier dangereux.  
  Test d’upload de fichiers non autorisés.  

## Détection des Bugs

Tests fonctionnels pour chaque scénario utilisateur.  
Tests de performance sur le tableau de bord.  
Tests de sécurité sur les fichiers et l’accès aux données.  
Tests de régression après modifications.  
Revue des logs pour repérer les erreurs et exceptions.  

## Validation des Spécifications

Les spécifications sont validées en comparant les résultats obtenus avec les résultats attendus pour chaque scénario.  
Les outils utilisés peuvent inclure des rapports d’erreurs et des logs pour confirmer les alertes et les performances.  
La conformité, la performance et la sécurité doivent être respectées avant validation finale.  
