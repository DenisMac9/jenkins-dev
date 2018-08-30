Chaîne d'intégration
====================

Configuration Jenkins
---------------------

**Ajout des crédentials**

Dans **Credentials > Jenkins > Global Credentials** (pour des données de connexion globales), faire **Add credentials**, et remplir le formulaire avec les champs suivants :
- **Kind** : **Secret text**
- **Scope** : Choisir le scope adapté
- **Secret** : La valeur du credential
- **ID** : La clé du crediential

Dans un Jenkinsfile, on peut récupèrer une valeur de ce type de la façon suivante dans une variable d'environnement :

```
environment {
    VALUE = credentials("key")
}
```


Cas d'usage
-----------

Ce type de dépôt sert à faire le build des images Docker qui seront ensuite envoyées dans le cluster.
