# Cours

## Chapitre 1

### Exercice 1
```cs
using System;

public class P1C21
{
    public static void Main(string[] args)
    {
        // déclarer une variable int nommée allocationCourante
        int allocationCourante = 200;
        // déclarer une variable int epargne
        int epargne = 3000;

        // TODO : créer une variable int nommée prime avec pour valeur initiale 500.
        int prime = 500;

        // Afficher le résultat
        Console.WriteLine("Votre allocation courante est de " + allocationCourante);
        Console.WriteLine("Le montant de votre épargne est de " + epargne);
        Console.WriteLine("Vous bénéficiez d'une prime de " + prime);
    }
}
```

### Exercice 2
```cs
using System;

public class MaVariable
{
    public static void Main(string[] args)
    {
        int epargne = 3000;

        // TODO : modifier l'instruction suivante pour utiliser l'opérateur raccourci +=	
        //epargne = epargne + 500;
        epargne += 500;
        Console.WriteLine("Le montant de votre épargne est de : " + epargne);
    }
}
```

### Exercice 3
```cs
using System;

public class Revision
{
    public static void Main(string[] args)
    {
        // TODO, étape 1 :
        // Créer une variable nommée jourDeDepart avec pour valeur initiale 3
        int jourDeDepart = 3;

        // TODO, étape 2 :
        // Créer une constante nommée joursDansSemaine avec pour valeur 7
        const int joursDansSemaine = 7;

        // TODO, étape 3 :
        // Utiliser un opérateur de raccourci pour ajouter la valeur de la constante joursDansSemaine à la variable jourDeDepart
        jourDeDepart += joursDansSemaine;

        // Afficher le résultat 
        Console.WriteLine("Il y a " + joursDansSemaine + " jours dans la semaine.");
        Console.WriteLine("Votre jour de départ du mois est : " + jourDeDepart);
    }
}
```

## Chapitre 2

Pour représenter les nombres décimaux : `float`, `double` et `decimal`

Exemple :
```cs
float longueur = 1876.79F;
double largeur = 1876.79797657;
decimal cout = 300.5M;
```

### Exercice 1
```cs
using System;

public class MelangeDeTypes
{
    public static void Main(string[] args)
    {
        int numerateur = 10;
        int denominateur = 4;

        // TODO : modifier l'instruction ci-dessous pour que la réponse prenne une valeur décimale
        double reponse = (double)numerateur / (double)denominateur;

        // Afficher le résultat 
        Console.WriteLine(numerateur + " / " + denominateur + " = " + reponse);
    }
}
```

### Exercice 2
```cs
using System;

public class StringConcat
{
    public static void Main(string[] args)
    {
        string animals = "J'aime les chiens et les chats";
        animals += ", mais aussi les pingouins !";
        Console.WriteLine(animals);
    }
}
```

## Chapitre 3

### Exercice 1
```cs
using System;

public class Classes
{
    public static void Main(string[] args)
    {
        // TODO, étape 1 : instancier un objet de la classe Livre et affecter cet objet à une variable nommée monLivre
        Livre monLivre = new Livre();

       	// TODO, étape 2 : affe cter une valeur aux champs titre, auteur et nombre de pages votre objet
        monLivre.titre = "Le Seigneur des Anneaux";
        monLivre.auteur = "J.R.R. Tolkien";
        monLivre.nombreDePages = 500;


        // Afficher le contenu des champs de cet objet 
        Console.WriteLine("Le titre du livre est " + monLivre.titre);
        Console.WriteLine("Son auteur est " + monLivre.auteur);
        Console.WriteLine("Il compte " + monLivre.nombreDePages);
    }
}

class Livre
{
    public String titre { get; set; }
    public String auteur { get; set; }
    public int nombreDePages { get; set; }
}
```

## Chapitre 4

### Exercice 1
```cs
using System;

public class TableauDeCouleurs
{
    public static void Main(string[] args)
    {
        // TODO : Déclarer une variable nommée couleurs d'un array de chaînes de longueur 5
        string[] couleurs = new string[5] { "rouge", "jaune", "orange", "vert", "bleu" };

        // TODO : Remplir le tableau avec les couleurs demandées
        // couleurs[0] = "rouge";
        // couleurs[1] = "jaune";
        // couleurs[2] = "orange";
        // couleurs[3] = "vert";
        // couleurs[4] = "bleu";

        // TODO : Remplacer vert par émeraude dans le tableau
        couleurs[3] = "émeraude";

        // Afficher le contenu du tableau
        foreach (String couleur in couleurs)
        {
            Console.WriteLine(couleur);
        }
    }
}
```
```cs
// Créer un array multidimensionnel pour gérer tous les rangs d'un théâtre
string[,] mesSieges = new string[30,12];

// Rang 10, siège 6. N'oubliez pas que l'index commence à 0 !
mesSieges[9,5] = "James Logan";
```

#### L'interface `IList`
```cs
IList<int> maListe = new List<int>(); // -> []
maListe.Add(7); // -> [7]
maListe.Add(5); //-> [7, 5]
maListe.Insert(1,12); //-> [7, 12, 5]
maListe.RemoveAt(1); // Suppression du 12 -> [7, 5]
Console.WriteLine(maListe.Count); // -> 2
```

### Exercice 2
```cs
using System;
using System.Collections;
using System.Collections.Generic;

public class ListeDesInvites
{
    public static void Main(string[] args)
    {
        // TODO : Remplacer le ?? par le code approprié pour créer une liste de chaînes
        IList<string> invites = new List<string>();

        // TODO : Ajouter Joe, Martin et Marie à la liste.
        invites.Add("Joe");
        invites.Add("Martin");
        invites.Add("Marie");

        // TODO : Compléter l'instruction suivante en remplaçant le ?? pour afficher la taille de la liste
        Console.WriteLine(invites.Count);

        // TODO : Remplacer Martin par Jean dans la liste
        invites[1] = "Jean";

        // TODO : Retirer Joe de la liste
        invites.Remove("Joe");

        // Afficher le contenu de la liste
        Console.WriteLine("Les invités sont :");
        foreach (String invite in invites)
        {
            Console.WriteLine(invite);
        }
    }
}
```

#### L'interface ISet
```cs
ISet<string> ingredients = new HashSet<string>();
ingredients.Add("sel"); // Ajouter du sel dans la liste des ingrédients
ingredients.Remove("sel"); // Supprimer le sel de la liste des ingrédients
```

### Exercice 3
```cs
using System;
using System.Collections.Generic;

public class EnsembleIngredients
{
    public static void Main(string[] args)
    {
        ISet<string> ingredients = new HashSet<string>();
        ingredients.Add("sucre");
        ingredients.Add("chocolat");
        ingredients.Add("beurre");
        ingredients.Add("vanille");

        // TODO : ajouter un autre ingrédient à l'ensemble
        ingredients.Add("farine");

        // TODO : retirer la vanille de l'ensemble
        ingredients.Remove("vanille");

        // Afficher la liste des ingrédients
        Console.WriteLine("Voici la liste de nos ingrédients");
        foreach (String ingredient in ingredients)
        {
            Console.WriteLine(ingredient);
        }
    }
}
```

#### L'interface IDictionary

```cs
// Définir des clés en tant que constantes
const string cleJennifer = "Jennifer";
const string cleLivia = "Livia";
const string clePaul = "Paul";

// Utiliser des constantes comme clés
monDictionnaire.Add(cleJennifer, 34);
monDictionnaire.Add(cleLivia, 28);
monDictionnaire.Add(clePaul, 31);

// Accéder à un élément
Console.WriteLine(monDictionnaire[cleJennifer]); // -> 34
```

### Exercice 4
```cs
using System;
using System.Collections.Generic;

public class DictionnaireDeMois
{
    public static void Main(string[] args)
    {
        IDictionary<string, int> mois = new Dictionary<string, int>();

        // TODO : Remplacer les noms par des constantes de type chaine de caractères
        const string juin = "Juin";
        const string septembre = "Septembre";
        const string mars = "Mars";
        mois.Add(juin, 6);
        mois.Add(septembre, 9);
        mois.Add(mars, 5);

        // TODO : Corriger la valeur de Mars avec (3)
        mois[mars] = 3;

        // TODO : Retirer Juin
        mois.Remove(juin);

        // Afficher le contenu du dictionnaire
        Console.WriteLine("La liste des mois est :");
        foreach (KeyValuePair<string, int> clePaire in mois)
        {
            Console.WriteLine(clePaire.Key.ToString() + " est le numéro du mois de " + clePaire.Value + " de l'année ");
        }
    }
}
```

## Chapitre 5

#### Niveaux d'accès
`public` / `private` / `protected` / `internal` (restreint au package)