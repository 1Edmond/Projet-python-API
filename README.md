# Livre API 

## Getting Started

### Installation des Dépendances

#### Python 3.10.0
#### pip 22.0.3 from C:\Users\hp\AppData\Local\Programs\Python\Python310\lib\site-packages\pip (python 3.10)

Suivez les instructions suivantes pour installer l'ancienne version de python sur la plateforme [python docs](https://www.python.org/downloads/windows/#getting-and-installing-the-latest-version-of-python)

#### Dépendances de PIP

Pour installer les dépendances,placez-vous dans le dossier de  `requirements.txt` et exécuter la commande suivante:

```bash ou powershell ou cmd
pip install -r requirements.txt
or
pip3 install -r requirements.txt
```

Nous passons donc à l'installation de tous les packages se trouvant dans le fichier `requirements.txt`.

##### clé de Dépendances

- [Flask](http://flask.pocoo.org/)  est un petit framework web Python léger, qui fournit des outils et des fonctionnalités utiles qui facilitent la création d’applications web en Python.

- [SQLAlchemy](https://www.sqlalchemy.org/) est un toolkit open source SQL et un mapping objet-relationnel écrit en Python et publié sous licence MIT. SQLAlchemy a opté pour l'utilisation du pattern Data Mapper plutôt que l'active record utilisés par de nombreux autres ORM

## Démarrer le serveur

Pour démarrer le serveur sur Linux ou Mac, executez:

```bash
export FLASK_APP=app.py
export FLASK_ENV=development
flask run
```
Pour le démarrer sur Windows, executez:

```bash
set FLASK_APP=app.py
set FLASK_ENV=development
flask run
``` 

## API REFERENCE

Getting starter

Base URL: At present this app can only be run locally and is not hosted as a base URL. The backend app is hosted at the default, http://localhost:5000; which is set as a proxy in frontend configuration.

## Type d'erreur
Les erreurs sont renvoyées sous forme d'objet au format Json:
{
    "success":False
    "error": 404
    "message":"Not found"
}

L'API vous renvoie 5 types d'erreur:
. 400: Bad request ou ressource non disponible
. 500: Internal server error
. 401: Unauthorized
. 404: Not found
. 405: Method Not Allowed

## Endpoints
. ## GET/livres

    GENERAL:
        Cet endpoint retourne la liste des livres, la valeur du succès et le total des livres. 
    
        
    EXEMPLE: curl http://localhost:5000/livres
```{
    "livres": [
        {
            "auteur": "Friedo",
            "categorie": {
                "id": 4,
                "libelle": "Exotique"
            },
            "date de publication": "Tue, 01 Feb 2022 00:00:00 GMT",
            "editeur": "Edmond",
            "id": 1,
            "isbn": "LDLV",
            "titre": "Livre de la vie"
        },
        {
            "auteur": "Supect 95 ft Josey",
            "categorie": {
                "id": 4,
                "libelle": "Exotique"
            },
            "date de publication": "Sat, 12 Feb 2022 00:00:00 GMT",
            "editeur": "Supect 95 officiel",
            "id": 2,
            "isbn": "S95-J",
            "titre": "Je suis fan je suis pas amoureux"
        },
        {
            "auteur": "Edmond",
            "categorie": {
                "id": 3,
                "libelle": "Roman"
            },
            "date de publication": "Sun, 13 Feb 2022 00:00:00 GMT",
            "editeur": "Wilfried",
            "id": 6,
            "isbn": "L2",
            "titre": "Livre 2"
        }
    ],
    "success": true,
    "total_livre": 3
}
```

.##GET/livres(live_id)
  GENERAL:
  Cet endpoint permet de récupérer les informations d'un livre particulier s'il existe par le biais de l'ID.

    EXEMPLE: http://localhost:5000/livres/2
```
  {
    "id": 2,
    "livre": {
        "auteur": "Supect 95 ft Josey",
        "categorie": {
            "id": 4,
            "libelle": "Exotique"
        },
        "date de publication": "Sat, 12 Feb 2022 00:00:00 GMT",
        "editeur": "Supect 95 officiel",
        "id": 2,
        "isbn": "S95-J",
        "titre": "Je suis fan je suis pas amoureux"
    },
    "success": true
}
```


. ## DELETE/livres (livre_id)

    GENERAL:
        Supprimer un element si l'ID existe. Retourne l'ID du livre supprimé, la valeur du succès et le nouveau total.

        EXEMPLE: curl -X DELETE http://localhost:5000/livres/1
```
   {
    "id_supprimee": 1,
    "success": true,
    "total_livre": 2
}
```

. ##PATCH/livres(livre_id)
  GENERAL:
  Cet endpoint permet de mettre à jour les champs d'un livre.
  Il retourne un livre mis à jour.

  EXEMPLE.....Avec Patch
  ``` curl -X PATCH http://localhost:5000/livres/6 -H "Content-Type:application/json" -d '{"auteur": "Azychika, Takumi Fukui","editeur": "Ki-oon","titre": "Jujutsu Kaisen"}'
  ```
  ```
   {
    "id": 6,
    "livre_modifie": {
        "auteur": "Azychika, Takumi Fukui",
        "categorie": {
            "id": 3,
            "libelle": "Roman"
        },
        "date de publication": "Sun, 13 Feb 2022 00:00:00 GMT",
        "editeur": "Ki-oon",
        "id": 6,
        "isbn": "L2",
        "titre": "Jujutsu Kaisen"
    },
    "success": true
}
    ```

. ## GET/categories

    GENERAL:
        Cet endpoint retourne la liste des categories de livres, la valeur du succès et le total des categories disponibles. 
    
        
    EXEMPLE: curl http://localhost:5000/categories
{
    "categories": [
        {
            "id": 2,
            "libelle": "Categorie 2"
        },
        {
            "id": 3,
            "libelle": "Roman"
        },
        {
            "id": 4,
            "libelle": "Exotique"
        },
        {
            "id": 5,
            "libelle": "Roman policier"
        }
    ],
    "nombre": 4,
    "success": true
}
```

.##GET/categories(categorie_id)
  GENERAL:
  Cet endpoint permet de récupérer les informations d'une categorie si elle existe par le biais de l'ID.

    EXEMPLE: http://localhost:5000/categories/5
```
   {
    "categorie": {
        "id": 5,
        "libelle": "Roman policier"
    },
    "id": 5,
    "success": true
}
```

. ## DELETE/categories (categories_id)

    GENERAL:
        Supprimer un element si l'ID existe. Retourne l'ID da la catégorie supprimé, la valeur du succès et le nouveau total.

        EXEMPLE: curl -X DELETE http://localhost:5000/categories/2
```
  {
    "id_supprimee": 2,
    "success": true,
    "total_categorie": 3
}
```

. ##PATCH/categories(categorie_id)
  GENERAL:
  Cet endpoint permet de mettre à jour le libelle ou le nom de la categorie.
  Il retourne une nouvelle categorie avec la nouvelle valeur.

  EXEMPLE.....Avec Patch
  ``` curl -X PATCH 'http://localhost:5000/categories/4' -H "Content-Type:application/json" -d '{"libelle_categorie": "Bandes Dessinées"}'
  ```
  ```
   {
    "categorie_modifie": {
        "id": 4,
        "libelle": "Bandes Dessinées"
    },
    "id": 4,
    "success": true
}

.##GET/livres/categories(categorie_id)
  GENERAL:
  Cet endpoint permet de lister les livres appartenant à une categorie donnée.
  Il renvoie la classe de la categorie et les livres l'appartenant.

    EXEMPLE: http://localhost:5000/livres/categories/4
```
{
    "categorie": {
        "id": 4,
        "libelle": "Bandes Dessinées"
    },
    "livres": [
        {
            "auteur": "Supect 95 ft Josey",
            "categorie": {
                "id": 4,
                "libelle": "Bandes Dessinées"
            },
            "date de publication": "Sat, 12 Feb 2022 00:00:00 GMT",
            "editeur": "Supect 95 officiel",
            "id": 2,
            "isbn": "S95-J",
            "titre": "Je suis fan je suis pas amoureux"
        }
    ],
    "nombre": 1,
    "success": true
}
```