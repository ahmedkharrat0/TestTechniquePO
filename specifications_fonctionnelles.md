# Spécification Fonctionnelles:

## 1. Contexte:
Le client souhaite ajouter un module de gestion des projets à son application de gestion des tâches.
Le module de gestion de projets permettra de gérer les projets, les phases, les tâches, les budgets, les dépendances, les commentaires, et le suivi de performance via un dashboard.

## 2. Les Entités Principales:

### Projet:
les champs:
id, titre, description, date_début, date_fin, temps_estimé (heures), coût_estimé, chef_de_projet_id (utilisateur), statut (en_prép | Actif | En pause | Clôturé), créé_le, modifié_le

les champs obligatoires:
titre, chef_de_projet_id, date_début, date_fin, coût_estimé, temps_estimé

### Phase
les champs:
id, projet_id, titre, description, ordre, date_début, date_fin

les champs obligatoires:
titre, ordre, date_début, date_fin, projet_id

### Tâche
les champs:
id, phase_id, projet_id, titre, description, assignés (liste d’utilisateurs), temps_estimées, coût_estimé, heures_réelles, coût_réel, date_début, date_fin, statut (À faire | En cours | Bloquée | Terminée), dépendances (liste de tâches), nb_commentaires, nb_fichiers

les champs obligatoires:
titre, phase_id, projet_id, date_début, date_fin, assignés (au moins un utilisateur), temps_estimées, coût_estimé

### Commentaire
les champs:
id, tâche_id, utilisateur_id, texte, créé_le

les champs obligatoires:
texte, tâche_id, utilisateur_id

### Fichier
les champs:
id, tâche_id, nom, url, taille, utilisateur_id, créé_le

les champs obligatoires:
tâche_id, nom, url

### Notification
les champs:
id, utilisateur_id, type, contenu, lu, créé_le
  
les champs obligatoires:
utilisateur_id, type, contenu

## 3. Fonctionnalité "Gestion des Projets"

### Entrées
Formulaire de création / édition :
titre, description, dates, budgets, chef de projet

### Actions
Boutons : Créer, Modifier, Supprimer, Ajouter Phase, Ajouter Tâche
Options : Changer le statut, Réordonner les phases

### Résultats attendus
Projet créé et visible dans la liste
Le chef de projet reçoit une notification
Les phases apparaissent dans l’ordre défini
Validation des champs obligatoires

### Règles métier
Les dates de phase et de tâche doivent être incluses dans les dates du projet
Le budget total des tâches ≤ budget du projet
Un utilisateur ne peut pas être affecté à plus de 3 tâches actives sur un même projet
Dépendances sans cycle autorisé

## 4. Fonctionnalité "Planification des Tâches"

### Entrées
Titre, description, utilisateurs assignés, dates, dépendances

### Actions
Assigner un ou plusieurs utilisateurs
Modifier les dates selon dépendances
Ajouter commentaires et fichiers
Changer le statut de la tâche

### Résultats attendus
Les dépendances bloquent le démarrage prématuré d’une tâche
Les utilisateurs reçoivent une notification d’assignation
Les commentaires et fichiers sont enregistrés avec auteur et date

### Règles métier
Si une tâche est marquée “Terminée”, les tâches dépendantes deviennent “Débloquées”
Aucune tâche ne peut commencer avant la fin de ses dépendances
Cycle de dépendances interdit (vérification automatique)

## 5. Fonctionnalité "Suivi des Performances"

### Entrées
Heures réelles, coûts réels, statut des tâches

### Actions
Calcul automatique du pourcentage d’avancement
Génération d’alertes si :
  Budget réel > budget estimé
  Délai dépassé

### Résultats attendus
Tableau de bord affichant :
  % d’achèvement du projet
  Dépenses réelles vs estimées
  Alertes envoyées au chef de projet

## 6. Fonctionnalité "Règles Métier"

1. Affectation: un utilisateur =< 3 tâches actives par projet  
2. Budget global: le total ne peut dépasser un seuil défini. Sinon, alerte et blocage de nouvelles tâches  
3. Cycle interdit: aucune dépendance circulaire  
4. Dates cohérentes: toute tâche doit avoir une date de début >= fin de ses prédécesseurs

## 7. Fonctionnalités Non Fonctionnelles

Performance: Temps de réponse < 2 secondes pour 5000 tâches  
Sécurité: Authentification obligatoire, contrôle RBAC  
Compatibilité: Chrome, Firefox, Edge (2 dernières versions)  
Sauvegarde: Backup quotidien, rétention 30 jours  
Journalisation: Audit de toutes les actions

## 8. Validation des Spécifications
Chaque exigence doit avoir au moins un scénario de test réussi  
Les règles métier doivent être validées par tests unitaires ou manuels  
Les alertes et le tableau de bord doivent produire des résultats cohérents  
La sécurité et la performance sont testées avec des outils adaptés (Postman, JMeter, OWASP ZAP)
