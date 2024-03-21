# C++ POO

## Notion de POO

### Le type `string` est un objet
```cpp
#include <iostream>
#include <string> // Obligatoire pour pouvoir utiliser les objets string
 
using namespace std;
 
 
int main()
{
    string maChaine("Bonjour !");
    cout << maChaine << endl;
    
    maChaine = "Bien le bonjour !";
    cout << maChaine << endl;

    // ---------------------------------------------------------- //

    string chaine1("Bonjour !");
    string chaine2("Comment allez-vous ?");
    string chaine3;
 
    chaine3 = chaine1 + chaine2; // 3... 2... 1... Concaténatioooooon
    cout << chaine3 << endl;

    // ---------------------------------------------------------- //

    string chaine1("Bonjour !");
    string chaine2("Comment allez-vous ?");
 
    if (chaine1 == chaine2) // Faux
    {
        cout << "Les chaines sont identiques." << endl;
    }
    else
    {
        cout << "Les chaines sont differentes." << endl;
    }

    // ---------------------------------------------------------- //

    string maChaine("Bonjour !");
    cout << "Longueur de la chaine : " << maChaine.size();  // taille de `maChaine`

    maChaine.erase();   // Supprime tout le contenu de `maChaine` (equivalent à `maChaine = "";`)
    cout << "La chaine contient : " << maChaine << endl;
 
    return 0;
}
```

### Méthode substr()
```cpp
int main()
{
    string chaine("Bonjour !");
    cout << chaine.substr(3) << endl;   // affiche "jour !"     : 3 pour afficher à partir de 3 caractères
                                        //                        donc enlève "Bon"
    cout << chaine.substr(3, 4) << endl;    // affiche "jour"   : 4 pour ne prendre que 4 caractères à partir 
                                            //                    de 3 carac donc enlève "Bon" et ne prend que "jour"
 
    return 0;
}
```

## Créer une classe

### Attributs
```cpp
class Personnage
{
    int m_vie;  // m_nom-attrib pas obligatoire, mais permet de différencier facilement un attrib d'une variable
    int m_mana;
    string m_nomArme;
    int m_degatsArme;
};
```

### Methodes
```cpp
class Personnage
{
     // Attributs
    int m_vie;
    int m_mana;
    string m_nomArme;
    int m_degatsArme;  

    // Méthodes
    void recevoirDegats(int nbDegats)
    {

    }

    void attaquer(Personnage &cible)
    {

    }

    void boirePotionDeVie(int quantitePotion)
    {

    }

    void changerArme(string nomNouvelleArme, int degatsNouvelleArme)
    {

    }

    bool estVivant()
    {

    }  
};
```

## Accès et encapsulation
```cpp
int main()
{
    Personnage david, goliath;
    //Création de 2 objets de type Personnage : david et goliath
 
    goliath.attaquer(david); //goliath attaque david
    david.boirePotionDeVie(20); //david récupère 20 de vie en buvant une potion
    goliath.attaquer(david); //goliath attaque david
    david.attaquer(goliath); //david contre-attaque... c'est assez clair non ?
    
    goliath.changerArme("Double hache tranchante veneneuse de la mort", 40);
    goliath.attaquer(david);
 
 
    return 0;
}
```

### Droits d'accès
`private` et `public`

```cpp
class Personnage
{
    // Tout ce qui suit est prive (inaccessible depuis l'extérieur)
    private:
    
    int m_vie;
    int m_mana;
    string m_nomArme;
    int m_degatsArme;

    // Tout ce qui suit est public (accessible depuis l'extérieur)
    public:
    
    void recevoirDegats(int nbDegats)
    {
 
    }
 
    void attaquer(Personnage &cible)
    {
 
    }
 
    void boirePotionDeVie(int quantitePotion)
    {
 
    }
 
    void changerArme(string nomNouvelleArme, int degatsNouvelleArme)
    {
 
    }
 
    bool estVivant()
    {
 
    }
};
```

### Séparer prototypes et définitions

`Personnage.hpp`
```cpp
#ifndef DEF_PERSONNAGE
#define DEF_PERSONNAGE

#include <string>

class Personnage
{
    public:

    void recevoirDegats(int nbDegats);
    void attaquer(Personnage &cible);
    void boirePotionDeVie(int quantitePotion);
    void changerArme(std::string nomNouvelleArme, int degatsNouvelleArme);
    bool estVivant();

    private:

    int m_vie;
    int m_mana;
    std::string m_nomArme; //Pas de using namespace std, il faut donc mettre std:: devant string
    int m_degatsArme;
};

#endif
```

`Personnage.cpp`
```cpp
#include "Personnage.hpp"

using namespace std;

void Personnage::recevoirDegats(int nbDegats)
{
    m_vie -= nbDegats;
    //On enlève le nombre de dégâts reçus à la vie du personnage

    if (m_vie < 0) //Pour éviter d'avoir une vie négative
    {
        m_vie = 0; //On met la vie à 0 (cela veut dire mort)
    }
}

void Personnage::attaquer(Personnage &cible)
{
    cible.recevoirDegats(m_degatsArme);
    //On inflige à la cible les dégâts que cause notre arme
}

void Personnage::boirePotionDeVie(int quantitePotion)
{
    m_vie += quantitePotion;

    if (m_vie > 100) //Interdiction de dépasser 100 de vie
    {
        m_vie = 100;
    }
}

void Personnage::changerArme(string nomNouvelleArme, int degatsNouvelleArme)
{
    m_nomArme = nomNouvelleArme;
    m_degatsArme = degatsNouvelleArme;
}

bool Personnage::estVivant()
{
    return m_vie > 0;
}
```

`main.cpp`
```cpp
#include <iostream>
#include "Personnage.hpp" //Ne pas oublier

using namespace std;

int main()
{
    Personnage david, goliath;
    //Création de 2 objets de type Personnage : david et goliath

    goliath.attaquer(david); //goliath attaque david
    david.boirePotionDeVie(20); //david récupère 20 de vie en buvant une potion
    goliath.attaquer(david); //goliath attaque david
    david.attaquer(goliath); //david contre-attaque... c'est assez clair non ? 
    goliath.changerArme("Double hache tranchante veneneuse de la mort", 40);
    goliath.attaquer(david);

    return 0;
}
```

## Initialiser objet

`Personnage.hpp`
```cpp
#include <string>
 
class Personnage
{
    public:
 
    Personnage(); //Constructeur
    void recevoirDegats(int nbDegats);
    void attaquer(Personnage &cible);
    void boirePotionDeVie(int quantitePotion);
    void changerArme(std::string nomNouvelleArme, int degatsNouvelleArme);
    bool estVivant();
 
 
    private:
 
    int m_vie;
    int m_mana;
    std::string m_nomArme;
    int m_degatsArme;
};
```

`Personnage.cpp`
```cpp
Personnage::Personnage()
{
    m_vie = 100;
    m_mana = 100;
    m_nomArme = "Epee rouillee";
    m_degatsArme = 10;
}

// OU ALORS

Personnage::Personnage() : m_vie(100), m_mana(100), m_nomArme("Epee rouillee"), m_degatsArme(10) {}

// Les deux constructeurs sont équivalents
```

### Surcharge

`Personnage.hpp`
```cpp
// On rajoute ce constructeur en plus du précédent
Personnage(std::string nomArme, int degatsArme);
```

`Personnage.cpp`
```cpp
// Pareil ici, on le rajoute
Personnage::Personnage(string nomArme, int degatsArme) : m_vie(100), m_mana(100),m_nomArme(nomArme),
m_degatsArme(degatsArme) {}
```

`main.cpp`
```cpp
// On peut donc maintenant utiliser deux constructeurs différents
Personnage david, goliath("Epee aiguisee", 20);
```

### Constructeur de copie

Créé par défaut par C++

`main.cpp`
```cpp
Personnage goliath("Epee aiguisee", 20);  //On crée goliath en utilisant un constructeur normal

Personnage david(goliath);                //On crée david en copiant tous les attributs de goliath
```

Mais modifiable !

`Personnage.hpp`
```cpp
Personnage(Personnage const& autre);
```

`Personnage.cpp`
```cpp
Personnage::Personnage(Personnage const& autre): m_vie(autre.m_vie), m_mana(autre.m_mana),
m_nomArme(autre.m_nomArme), m_degatsArme(autre.m_degatsArme) {}
```

### Destructeur

Inverse de constructeur, il est appelé un objet est supprimé de la mémoire, donc son rôle est de désallouer la mémoire (avec des delete) qui a été allouée dynamiquement.

`Personnage.hpp`
```cpp
~Personnage();
```

`Personnage.cpp`
```cpp
Personnage::~Personnage()
{
    /* Rien à mettre ici car on ne fait pas d'allocation dynamique
    dans la classe Personnage. Le destructeur est donc inutile mais
    je le mets pour montrer à quoi cela ressemble.
    En temps normal, un destructeur fait souvent des delete et quelques
    autres vérifications si nécessaire avant la destruction de l'objet. */
}
```

### Methodes constantes

= Méthodes qui ne modifie pas l'objet (exemple : getters)

```cpp
//Prototype de la méthode (dans le .hpp) :
void maMethode(int parametre) const;
 
 
//Déclaration de la méthode (dans le .cpp) :
void MaClasse::maMethode(int parametre) const
{
 
}

// EXEMPLE
bool Personnage::estVivant() const
{
    return m_vie > 0;
}
```

## Associer classes entre elles

### Classe `Arme`

`Arme.hpp`
```cpp
#ifndef DEF_ARME
#define DEF_ARME

#include <iostream>
#include <string>
 
class Arme
{
    public:
 
    Arme();
    Arme(std::string nom, int degats);
    void changer(std::string nom, int degats);
    void afficher() const;
 
    private:
 
    std::string m_nom;
    int m_degats;
};
 
#endif
```

`Arme.cpp`
```cpp
#include "Arme.hpp"
 
using namespace std;
 
Arme::Arme() : m_nom("Epee rouillee"), m_degats(10)
{
 
}
 
Arme::Arme(string nom, int degats) : m_nom(nom), m_degats(degats)
{
 
}
 
void Arme::changer(string nom, int degats)
{
    m_nom = nom;
    m_degats = degats;
}
 
void Arme::afficher() const
{
    cout << "Arme : " << m_nom << " (Degats : " << m_degats << ")" << endl;
}
```

### Adapter la classe Personnage pour utiliser la classe Arme + un peu d'affichage

`Personnage.hpp`
```cpp
#ifndef DEF_PERSONNAGE
#define DEF_PERSONNAGE

#include <iostream>
#include <string>
#include "Arme.hpp"

class Personnage
{
    public:

    Personnage();
    Personnage(std::string nom, std::string nomArme, int degatsArme);
    ~Personnage();
    void recevoirDegats(int nbDegats);
    void attaquer(Personnage &cible);
    void attaqueMagique(Personnage &cible);
    void boirePotionDeVie(int quantitePotion);
    void changerArme(std::string nomNouvelleArme, int degatsNouvelleArme);
    bool estVivant();
    void afficherEtat();
    std::string getNom();

    private:

    std::string m_nom;
    int m_vie;
    int m_mana;
    Arme m_arme;
};

#endif
```

`Personnage.cpp`
```cpp
#include "Personnage.hpp"

using namespace std;

Personnage::Personnage() : m_nom("NoName"), m_vie(100), m_mana(100)
{
}

Personnage::Personnage(string nom, string nomArme, int degatsArme) : m_nom(nom),
                  m_vie(100),
                  m_mana(100),
                  m_arme(nomArme, degatsArme)
{
}

Personnage::~Personnage()
{
}

void Personnage::recevoirDegats(int nbDegats)
{
    cout << m_nom << " subit " << nbDegats << " points de dégâts." << endl;
    m_vie -= nbDegats;

    if (m_vie < 0)
    {
        m_vie = 0;
        cout << m_nom << " est mort." << endl;
    }
    cout << m_nom << " a " << m_vie << " point de vie.\n" << endl;
}

void Personnage::attaquer(Personnage &cible)
{
    cout << m_nom << " attaque " << cible.getNom() << "." << endl;
    cible.recevoirDegats(m_arme.getDegats());
}

void Personnage::boirePotionDeVie(int quantitePotion)
{
    cout << m_nom << " boit une potion de " << quantitePotion << " points de vie." << endl;
    m_vie += quantitePotion;

    if (m_vie > 100)
    {
        m_vie = 100;
    }
    cout << m_nom << " a " << m_vie << " point de vie.\n" << endl;
}

void Personnage::changerArme(string nomNouvelleArme, int degatsNouvelleArme)
{
    cout << m_nom << " change d'arme. Nouvelle arme : " << endl;
    m_arme.changer(nomNouvelleArme, degatsNouvelleArme);
    m_arme.afficher();
    cout << endl;
}

bool Personnage::estVivant()
{
    if (m_vie > 0)
    {
        return true;
    }
    else
    {
        return false;
    }
}

void Personnage::afficherEtat()
{
    cout << m_nom << " infos : " << endl;
    cout << "Vie : " << m_vie << endl;
    cout << "Mana : " << m_mana << endl;
    m_arme.afficher();
    cout << endl;
}

std::string Personnage::getNom()
{
    return m_nom;
}

void Personnage::attaqueMagique(Personnage &cible)
{
    const int mana = 10;
    cout << m_nom << " attaque " << cible.getNom() << "." << endl;
    cible.recevoirDegats(mana);
    m_mana -= mana;
}
```

`Arme.hpp`
```cpp
#ifndef DEF_ARME
#define DEF_ARME

#include <iostream>
#include <string>

class Arme
{
    public:

    Arme();
    Arme(std::string nom, int degats);
    void changer(std::string nom, int degats);
    void afficher();
    int getDegats() const;

    private:

    std::string m_nom;
    int m_degats;
};

#endif
```

`Arme.cpp`
```cpp
#include "Arme.hpp"

using namespace std;

Arme::Arme() : m_nom("Epée rouillée"), m_degats(10)
{
}

Arme::Arme(string nom, int degats) : m_nom(nom), m_degats(degats)
{
}

void Arme::changer(string nom, int degats)
{
    m_nom = nom;
    m_degats = degats;
}

void Arme::afficher()
{
    cout << "Arme : " << m_nom << " (Dégâts : " << m_degats << ")" << endl;
}

int Arme::getDegats() const
{
    return m_degats;
}
```

`main.cpp`
```cpp
#include <iostream>
#include <string>
#include "Personnage.hpp"

using namespace std;

int main()
{
    // Création des personnages
    Personnage david("David", "Aiguille", 25),
               goliath("Goliath", "Epée aiguisée", 20),
               mathieu("Mathieu", "Crocobur", 50);

    // Au combat !
    goliath.attaquer(david);
    david.boirePotionDeVie(20);
    goliath.attaquer(david);
    david.attaquer(goliath);
    goliath.changerArme("Double hache tranchante vénéneuse de la mort", 40);
    goliath.attaquer(david);

    // Temps mort ! Voyons voir la vie de chacun...
    david.afficherEtat();
    goliath.afficherEtat();
    mathieu.afficherEtat();
    
    // Au combat !
    mathieu.attaqueMagique(david);
    goliath.attaquer(mathieu);
    mathieu.attaquer(david);
    
    // Infos
    david.afficherEtat();
    goliath.afficherEtat();
    mathieu.afficherEtat();
    
    // Au combat !
    mathieu.attaquer(goliath);
    goliath.boirePotionDeVie(20);
    goliath.attaqueMagique(mathieu);
    mathieu.attaquer(goliath);
    
    // Infos
    david.afficherEtat();
    goliath.afficherEtat();
    mathieu.afficherEtat();
    
    return 0;
}
```

## Opérateurs de comparaison

### Surcharge d'opérateur

`Duree.hpp`
```cpp
#ifndef DEF_DUREE
#define DEF_DUREE
 
class Duree
{
    public:
 
    Duree(int heures = 0, int minutes = 0, int secondes = 0);
 
    private:
 
    int m_heures;
    int m_minutes;
    int m_secondes;
};
 
#endif
```

`Duree.cpp`
```cpp
#include "Duree.hpp"
 
Duree::Duree(int heures, int minutes, int secondes) : m_heures(heures), m_minutes(minutes), m_secondes(secondes)
{
}
```

`main.cpp`
```cpp
int main()
{
    Duree duree1(0, 10, 28), duree2(0, 15, 2);
 
    return 0;
}
```

### Operateurs de comparaisons

On commence par l'opérateur `==`

`Duree.hpp`
```cpp
// A rajouter en dehors de la classe (ce n'est pas une méthode !!!)
bool operator==(Duree const& a, Duree const& b);
```

Grâce à ça on peut comparer deux durées :
```cpp
if(duree1 == duree2)
{
     std::cout << "Les deux durees sont egales !" << std::endl;
}
```

Implémentation de l'opérateur :  
On peut commencer par implémenter une méthode `estEgal`

`Duree.cpp`
```cpp
bool Duree::estEgal(Duree const& b) const
{
    return (m_heures == b.m_heures && m_minutes == b.m_minutes && m_secondes == b.m_secondes);
    //Teste si a.m_heure == b.m_heure etc.  
}
```

Et ensuite on peut s'en servir pour l'opérateur (et cela évite de créer des getters vu que la fonction est en dehors de la classe)
```cpp
bool operator==(Duree const& a, Duree const& b)
{
    return a.estEgal(b);
}
```

#### Autres opérateurs de comparaisons

Le principe est exactement le même que pour `==` :  
- `bool operator>(Duree const &a, Duree const& b)`
- `bool operator<=(Duree const &a, Duree const& b)`
- `bool operator>=(Duree const &a, Duree const& b)`

## Opérateurs arithmétiques et de flux

### Opérateur `+`

```cpp
Duree operator+(Duree const& a, Duree const& b);
```

Type d'implémentation possible (comme précédemment) :
```cpp
Duree operator+(Duree const& a, Duree const& b)
{
    Duree resultat;
    resultat = a.calculeAddition(b);   //Utilise une méthode de Duree pour effectuer l'addition
    return resultat;
}
```

Mais ce n'est pas la plus optimale.

Il y a une autre méthode, les opérateurs raccourcis :
```cpp
Duree& Duree::operator+=(const Duree& a)
{
    //1 : ajout des secondes
    m_secondes += a.m_secondes;
    //Si le nombre de secondes dépasse 60, on rajoute des minutes
    //Et on met un nombre de secondes inférieur à 60
    m_minutes += m_secondes / 60;
    m_secondes %= 60;

    //2 : ajout des minutes
    m_minutes += a.m_minutes;
    //Si le nombre de minutes dépasse 60, on rajoute des heures
    //Et on met un nombre de minutes inférieur à 60
    m_heures += m_minutes / 60;
    m_minutes %= 60;

    //3 : ajout des heures
    m_heures += a.m_heures;

    return *this;
}
```

De plus, nous avons ici une méthode et non une fonction, les attributs sont donc facilement accessibles !

Maintenant pour revenir à l'addition de base, nous pouvons enfin la faire :
```cpp
Duree operator+(Duree const& a, Duree const& b)
{
    Duree copie(a);   //On utilise le constructeur de copie de la classe Duree !
    copie += b;       //On appelle la méthode d'addition qui modifie l'objet 'copie'
    return copie;     //Et on renvoie le résultat. Ni a ni b n'ont changé.
}
```

### Code complet

`Duree.hpp`
```cpp
#ifndef DEF_DUREE
#define DEF_DUREE

class Duree
{
public:
    Duree(int heures = 0, int minutes = 0, int secondes = 0);
    Duree& operator+=(const Duree &duree);
    void afficher() const;

private:
    int m_heures;
    int m_minutes;
    int m_secondes;
};

Duree operator+(Duree const& a, Duree const& b);

#endif
```

`Duree.cpp`
```cpp
#include <iostream>
#include "Duree.hpp"

using namespace std;

Duree::Duree(int heures, int minutes, int secondes)
    : m_heures(heures), m_minutes(minutes), m_secondes(secondes)
{
}

Duree& Duree::operator+=(const Duree &duree2)
{
    m_secondes += duree2.m_secondes;
    m_minutes += m_secondes / 60;
    m_secondes %= 60;

    m_minutes += duree2.m_minutes;
    m_heures += m_minutes / 60;
    m_minutes %= 60;

    m_heures += duree2.m_heures;

    return *this;
}

void Duree::afficher() const
{
    cout << m_heures << "h" << m_minutes << "m" << m_secondes << "s" << endl;
}

Duree operator+(Duree const& a, Duree const& b)
{
    Duree copie(a);
    copie += b;
    return copie;
}
```

`main.cpp`
```cpp
#include <iostream>
#include "Duree.hpp"

using namespace std;

int main()
{
    Duree duree1(0, 10, 42), duree2(0, 53, 27);
    Duree resultat;

    duree1.afficher();
    cout << "+" << endl;
    duree2.afficher();

    resultat = duree1 + duree2;

    cout << "=" << endl;
    resultat.afficher();

    return 0;
}
```

### Autres opérateurs arithmétiques

Le concept est identique
- `operator-()` -> `operator-=()`
- `operator*()` -> `operator*=()`
- `operator/()` -> `operator/=()`
- `operator%()` -> `operator%=()`

### Opérateurs de flux (<< et >>)

```cpp
cout << "Coucou !";
cin >> variable;
```
Revient à écrire :
```cpp
operator<<(cout, "Coucou !");
operator>>(cin, variable);
```

#### Implémentation de <<
```cpp
ostream& operator<<( ostream &flux, Duree const& duree )
{
    //Affichage des attributs
    return flux;
}
```

Ici, `ostream &flux` correspondra à `cout`, mais cela permet de généraliser.

`Duree.cpp`
```cpp
// Méthode d'affichage pour les durées
void Duree::afficher(ostream &flux) const
{
    flux << m_heures << "h" << m_minutes << "m" << m_secondes << "s";
}

// ------------------//

// Fonction d'opération qui utilise la méthode précédente
ostream &operator<<( ostream &flux, Duree const& duree)
{
    duree.afficher(flux) ;
    return flux;
}
```

Maintenant, on peut s'en servir dans le main :

`main.cpp`
```cpp
int main()
{
    Duree duree1(2, 25, 28), duree2(0, 16, 33);
    
    cout << duree1 << " et " << duree2 << endl;

    return 0;
}
```

## Associer classe et pointeur

### Pointeur de classe vers une autre classe

```cpp
class Personnage
{
    public:

    //Quelques méthodes…

    private:

    Arme *m_arme;
    //L'Arme est un pointeur, l'objet n'est plus contenu dans le Personnage
    //…
};
```
Beaucoup d'avantages, mais pas obligatoire pour autant de passer par des pointeurs, c'est au feeling.  
Mais cela permet :
- de facilement changer d'arme en faisant simplement pointer le pointeur vers une autre arme
- de facilement permettre à un personnage de donner son arme à un autre
- de simplement mettre le pointeur à 0 pour dire que le personnage n'a plus d'arme

### Allocation dynamique

```cpp
Personnage::Personnage() : m_arme(0), m_vie(100), m_mana(100)
{
    m_arme = new Arme();
}

// et / ou :

Personnage::Personnage(string nomArme, int degatsArme) : m_arme(0), m_vie(100), m_mana(100)
{
    m_arme = new Arme(nomArme, degatsArme);
}
```

### Désallocation

```cpp
Personnage::~Personnage()
{
    delete m_arme;
}
```

Si on ne delete pas le pointeur lorque qu'un personnage est détruit, il y aura des fuites mémoires car l'arme ne sera jamais détruite toute seule.

### Modifications dûes au pointeur

Exemple :
```cpp
void Personnage::attaquer(Personnage &cible)
{
    cible.recevoirDegats(m_arme->getDegats());
}
```

Penser à remplacer le `.` par une `->` !

Pour les attributs dans `Personnage.hpp`, il faut modifier l'attribut d'arme :

```cpp
Arme m_arme;
```
devient
```cpp
Arme* m_arme
```

Et cela entrainera toutes les modifs de pointeur à régler (cf. étapes précédentes)

### Le pointeur `this`

Exemples :
```cpp
Personnage* Personnage::getAdresse() const
{
    return this; // Renvoie l'addresse de l'objet
}
```
```cpp
Duree& Duree::operator+=(const Duree &duree2)
{
    //Des calculs compliqués…

    return *this;   // Renvoie l'objet lui-même
}
```

### Constructeur de copie et pointeurs

Le constructeur de copie par défaut se contente simplement de copier tous les attributs, y compris les pointeurs !  
Cela pose donc un problème car deux personnages par exemple auront leur pointeur qui pointe vers la même arme

`Personnage.hpp`
```cpp
class Personnage
{
    public:

    Personnage();
    Personnage(Personnage const& personnageACopier);
    //Le prototype du constructeur de copie
    Personnage(std::string nomArme, int degatsArme);
    ~Personnage();
    
    /*
    … plein d'autres méthodes qui ne nous intéressent pas ici
    */

    private:

    int m_vie;
    int m_mana;
    Arme *m_arme;
};
```

`Personnage.cpp`
```cpp
Personnage::Personnage(Personnage const& personnageACopier) 
   : m_vie(personnageACopier.m_vie), m_mana(personnageACopier.m_mana), m_arme(0)
{
    m_arme = new Arme(*(personnageACopier.m_arme));
}
```
Ansi, les deux persos auront bien la même arme, mais représentée par deux objets indépendants, et donc le pointeur de chaque perso pointera bien vers une arme différente.

### Opérateur d'affectation

Il faut différencier l'opérateur et le constructeur de copie :  
Ils font bien la même chose, mais le constructeur de copie est appelé lors d'une initialisation, tandis que l'opérateur est appelé lors d'une affectation.

```cpp
Personnage david = goliath; //Constructeur de copie
david = goliath; //operator=
```

Implémentation de l'opérateur :
```cpp
Personnage& Personnage::operator=(Personnage const& personnageACopier) 
{
    if(this != &personnageACopier)
    // On vérifie que l'objet n'est pas le même que celui reçu en argument
    {
        m_vie = personnageACopier.m_vie; //On copie tous les champs
        m_mana = personnageACopier.m_mana;
	    delete m_arme;
        m_arme = new Arme(*(personnageACopier.m_arme));
    }
    return *this; //On renvoie l'objet lui-même
}
```

Cependant, le constructeur de copie et cet opérateur sont extremement liés : si on a besoin d'implémenter l'un, il faudra obligatoirement implémenter l'autre également.

## Héritage

Simplification de la classe Personnage pour l'exemple

`Personnage.hpp`
```cpp
#ifndef DEF_PERSONNAGE
#define DEF_PERSONNAGE
 
#include <iostream>
#include <string>
 
class Personnage
{
    public:
        Personnage();
        void recevoirDegats(int degats);
        void coupDePoing(Personnage &cible) const;
 
    private:
        int m_vie;
        std::string m_nom;
};
 
#endif
```

`Personnage.cpp`
```cpp
#include "Personnage.hpp"
 
using namespace std;
 
Personnage::Personnage() : m_vie(100), m_nom("Jack")
{
 
}
 
void Personnage::recevoirDegats(int degats)
{
    m_vie -= degats;
}
 
void Personnage::coupDePoing(Personnage &cible) const
{
    cible.recevoirDegats(10);
}
```

`Guerrier.hpp`
```cpp
#ifndef DEF_GUERRIER
#define DEF_GUERRIER
 
#include <iostream>
#include <string>
#include "Personnage.hpp"
 
class Guerrier : public Personnage
{
    public:
        void frapperAvecUnMarteau() const;
        //Méthode qui ne concerne que les guerriers
};
 
#endif
```

`Magicien.hpp`
```cpp
#ifndef DEF_MAGICIEN
#define DEF_MAGICIEN
 
#include <iostream>
#include <string>
#include "Personnage.hpp"
 
class Magicien : public Personnage
{
    public:
        void bouleDeFeu() const;
        void bouleDeGlace() const;
 
    private:
        int m_mana;
};
 
#endif
```

### Dérivation de type

```cpp
Personnage *monPersonnage(0);
Guerrier *monGuerrier = new Guerrier();
 
monPersonnage = monGuerrier; // Mais… mais… Ça marche !?
```
Possible grâce à l'héritage

### Relation entre héritage et constructeurs

```cpp
Personnage::Personnage(string nom) : m_vie(100), m_nom(nom)
{
 
}
```
```cpp
Magicien::Magicien(string nom) : Personnage(nom), m_mana(100)
{
 
}
```
Appelle le constructeur de Personnage dans Magicien, puis ensuite on s'occupe à l'attribut unique au Magicien

### La portée `protected`

Il existe déjà `public` et `private`.

`protected` rend les éléments d'une classe mère UNIQUEMENT accessibles par elle-même ou ses classes filles.

### Masquage

```cpp
class Personnage
{
    public:
        Personnage();
        Personnage(std::string nom);
        void recevoirDegats(int degats);
        void coupDePoing(Personnage& cible) const;
        
        void sePresenter() const;
 
    protected:
        int m_vie;
        std::string m_nom;
};
```

```cpp
void Personnage::sePresenter() const
{
    cout << "Bonjour, je m'appelle " << m_nom << "." << endl;
    cout << "J'ai encore " << m_vie << " points de vie." << endl;
}
```

Le Guerrier a une ligne de plus :
```cpp
void Guerrier::sePresenter() const
{
    cout << "Bonjour, je m'appelle " << m_nom << "." << endl;
    cout << "J'ai encore " << m_vie << " points de vie." << endl;
    cout << "Je suis un Guerrier redoutable." << endl;
}
```

la classe Guerrier modifie la fonction héritée de Personnage, c'est le masquage.

```cpp
void Guerrier::sePresenter() const
{
    Personnage::sePresenter();
    cout << "Je suis un Guerrier redoutable." << endl;
}
```

Ici, on a un cas de démasquage.

## Polymorphisme

### Résolution statique des liens

```cpp
class Vehicule
{
    public:
    void affiche() const;  //Affiche une description du Vehicule

    protected:
    int m_prix;  //Chaque véhicule a un prix
};

class Voiture : public Vehicule //Une Voiture EST UN Vehicule
{
    public:
    void affiche() const;

    private:
    int m_portes;  //Le nombre de portes de la voiture
};

class Moto : public Vehicule  //Une Moto EST UN Vehicule
{
    public:
    void affiche() const;
 
    private:
    double m_vitesse;  //La vitesse maximale de la moto
};

// --------------------------------------------------- //

void Vehicule::affiche() const
{
    cout << "Ceci est un vehicule." << endl;
}

void Voiture::affiche() const
{
    cout << "Ceci est une voiture." << endl;
}

void Moto::affiche() const
{
    cout << "Ceci est une moto." << endl;
}
```

```cpp
void presenter(Vehicule v)  //Présente le véhicule passé en argument
{
    v.affiche();
}

int main()
{
    Vehicule v;
    presenter(v);

    Moto m;
    presenter(m);

    return 0;
}
```

### Résolution dynamique des liens

```cpp
class Vehicule
{
    public:
    virtual void affiche() const;  //Affiche une description du Vehicule

    protected:
    int m_prix;  //Chaque véhicule a un prix
};

class Voiture: public Vehicule  //Une Voiture EST UN Vehicule
{
    public:
    virtual void affiche() const;

    private:
    int m_portes;  //Le nombre de portes de la voiture
};

class Moto : public Vehicule  //Une Moto EST UN Vehicule
{
    public:
    virtual void affiche() const;
 
    private:
    double m_vitesse;  //La vitesse maximale de la moto
};
```
```cpp
void presenter(Vehicule const& v)  //Présente le véhicule passé en argument
{
    v.affiche();
}

int main()  //Rien n'a changé dans le main()
{
    Vehicule v;
    presenter(v);

    Moto m;
    presenter(m);

    return 0;
}
```

Il ne faut pas traiter les constructeurs par de la résolution dynamique, mais par contre il est nécessaire de le faire pour le destructeur si on utilise le polymorphisme.

```cpp
class Vehicule
{
    public:
    Vehicule(int prix);           //Construit un véhicule d'un certain prix
    virtual void affiche() const;
    virtual ~Vehicule();          //Remarquez le 'virtual' ici

    protected:
    int m_prix;
};

class Voiture: public Vehicule
{
    public:
    Voiture(int prix, int portes);
    //Construit une voiture dont on fournit le prix et le nombre de portes
    virtual void affiche() const;
    virtual ~Voiture();

    private:
    int m_portes;
};

class Moto : public Vehicule 
{
    public:
    Moto(int prix, double vitesseMax);
    //Construit une moto d'un prix donné et ayant une certaine vitesse maximale
    virtual void affiche() const;
    virtual ~Moto();
 
    private:
    double m_vitesse;
};
```
```cpp
Vehicule::Vehicule(int prix)
    :m_prix(prix)
{}

void Vehicule::affiche() const
//J'en profite pour modifier un peu les fonctions d'affichage
{
    cout << "Ceci est un vehicule coutant " << m_prix << " euros." << endl;
}

Vehicule::~Vehicule() //Même si le destructeur ne fait rien, on doit le mettre !
{}

Voiture::Voiture(int prix, int portes)
    :Vehicule(prix), m_portes(portes)   
{}

void Voiture::affiche() const
{
    cout << "Ceci est une voiture avec " << m_portes << " portes et coutant " << m_prix << " euros." << endl;
}

Voiture::~Voiture()
{}

Moto::Moto(int prix, double vitesseMax)
    :Vehicule(prix), m_vitesse(vitesseMax)
{}

void Moto::affiche() const
{
    cout << "Ceci est une moto allant a " << m_vitesse << " km/h et coutant " << m_prix << " euros." << endl;
}

Moto::~Moto()
{}
```

## Mettre en oeuvre le polymorphisme

### Gérer des collections hétérogènes (= plusieurs types)

```cpp
int main()
{
    vector<Vehicule*> listeVehicules;

    listeVehicules.push_back(new Voiture(15000, 5));
    //J'ajoute à ma collection de véhicules une voiture
    //Valant 15000 euros et ayant 5 portes
    listeVehicules.push_back(new Voiture(12000, 3));  //…
    listeVehicules.push_back(new Moto(2000, 212.5));
    //Une moto à 2000 euros allant à 212.5 km/h

    listeVehicules[0]->affiche();
    //On affiche les informations de la première voiture
    
    listeVehicules[2]->affiche();
    //Et celles de la moto

    for(int i(0); i<listeVehicules.size(); ++i)
    {
        delete listeVehicules[i];  //On libère la i-ème case mémoire allouée
        listeVehicules[i] = 0;  //On met le pointeur à 0 pour éviter les soucis
    }
   
    return 0;
}
```

### Utiliser des fonctions virtuelles pures

```cpp
class Vehicule
{
    public:
    Vehicule(int prix);           
    virtual void affiche() const;
    virtual int nbrRoues() const = 0;  //Affiche le nombre de roues du véhicule
    // avec le = 0, nbRoues devient une fonction virtuelle pure
    // meme concept que les methodes abstraites en Java, donc pas besoin d'ecrire la fonction dans le .cpp
    virtual ~Vehicule();         

    protected:
    int m_prix;
};

class Voiture : public Vehicule
{
    public:
    Voiture(int prix, int portes);
    virtual void affiche() const;
    virtual int nbrRoues() const;  //Affiche le nombre de roues de la voiture
    virtual ~Voiture();

    private:
    int m_portes;
};
```

### Classes abstraites

Une classe qui possède au moins une méthode virtuelle pure est une classe abstraite.

```cpp
int main()
{
    Vehicule* ptr(0);  //Un pointeur sur un véhicule
    
    Voiture caisse(20000,5);
    //On crée une voiture
    //Ceci est autorisé puisque toutes les fonctions ont un corps
    
    ptr = &caisse;  //On fait pointer le pointeur sur la voiture

    cout << ptr->nbrRoues() << endl;
    //Dans la classe fille, nbrRoues() existe, ceci est donc autorisé

    return 0;
}
```

## Exercice

1. Créer la classe abstraite  `Figure`  contenant les méthodes virtuelles :
    - `afficher()`  qui affiche le type de la classe. Exemple :  `Je suis une figure`  ;
    - la méthode virtuelle pure  `perimetre()`  ;
    - la méthode virtuelle pure  `aire()` .

2. Créer les 4 classes filles   ( `Triangle` ,  `Carre` ,  `Rectangle` ,  `Cercle` ) qui hériteront de la classe mère  `Figure`  et qui définissent les trois méthodes virtuelles de la classe  `Figure`.

3. Créer les constructeurs des 4 classes filles avec les attributs :
    - `Triangle`  : base et hauteur ;
    - `Carre`  : longueur ;
    - `Rectangle`  : longueur et largeur ;
    - `Cercle`  : rayon.

4. Définir l’ensemble des méthodes virtuelles.

5. Créer un vecteur de  `Figure`  et ajouter une instance de chaque classe fille.

6. Enfin à l’aide d’une boucle  `for`  , appeler chacune des méthodes :  `affiche()`  ,  `perimetre()`  et  `aire()`.  

`Figure.hpp`
```cpp
#ifndef FIGURE_HPP
#define FIGURE_HPP

#include <iostream>
class Figure {
    public:
        virtual void afficher() const;
        virtual double perimetre() const = 0;
        virtual double aire() const = 0;
};

class Carre : public Figure {
    protected:
        double m_cote;

    public:
        Carre(double cote);
        virtual void afficher();
        virtual void perimetre();
        virtual void aire();
};

// .....

#endif
```

`Figure.cpp`
```cpp
#include "Figure.hpp"

using namespace std;

void Figure::afficher() {
    cout << "Je suis une figure" << endl;
}

Carre::Carre(double cote) : m_cote(cote) {}

void Carre::afficher() {
    cout << "Je suis un carré" << endl;
}

double Carre::perimetre() {
    return 4 * m_cote;
}

double Carre::aire() {
    return m_cote * m_cote;
}

// .......
```

`main.cpp`
```cpp
#include <iostream>
#include <vector>
#include "Figure.hpp"

vector<Figure*> vector;
vector.pushback(new Carre(2));
vector.pushback(new Cercle(4));

for (int i = 0; i < vector.size(); i++) {
    vector[i]->afficher();
    cout << vector[i]->perimetre() << endl;
    cout << vector[i]->aire() << endl;
}

return 0;
```

## Utiliser éléments statiques et l'amitié

### Méthode statique

`MaClasse.hpp`
```cpp
class MaClasse
{
    public:
    MaClasse();
    static void maMethode();
};
```

`MaClasse.cpp`
```cpp
void MaClasse::maMethode() //Ne pas remettre 'static' dans l'implémentation
{
    cout << "Bonjour !" << endl;
}
```

`main.cpp`
```cpp
int main()
{
    MaClasse::maMethode();
 
    return 0;
}
```

### Attributs statiques

`MaClasse.hpp`
```cpp
class MaClasse
{
    public:
    MaClasse();
 
    private:
    static int monAttribut;
 
};
```
```cpp
//Initialiser l'attribut en dehors de toute fonction ou classe (espace global)
int MaClasse::monAttribut = 5;
```

Autre exemple avec la classe `Personnage` :

Ici on veut pouvoir connaître à tout instant le nombre d'instances actuelles de la classe Personnage.
```cpp
class Personnage
{
    public:
    Personnage(string nom);
    //Plein de méthodes…
    ~Personnage();
    static int nombreInstances();   //Renvoie le nombre d'objets créés

    private:
    string m_nom;
    static int compteur;
}
```
```cpp
int Personnage::compteur = 0; //On initialise notre compteur à 0

Personnage::Personnage(string nom)
    :m_nom(nom)
{
    ++compteur;  //Quand on crée un personnage, on ajoute 1 au compteur
}

Personnage::~Personnage()
{
    --compteur;  //Et on enlève 1 au compteur lors de la destruction
}

int Personnage::nombreInstances()
{
    return compteur;   //On renvoie simplement la valeur du compteur
}
```
```cpp
int main()
{
    //On crée deux personnages
    Personnage goliath("Goliath le tenebreux");
    Personnage lancelot("Lancelot le preux");

    //Et on consulte notre compteur
    cout << "Il y a actuellement " << Personnage::nombreInstances() << " personnages en jeu." << endl;
    return 0;
}
```

### Principe d'amitié

C'est donner un accès complet aux éléments d'une classe.
Cela casse donc le concept d'encapsulation : il faut être vigilant en l'utilisant.

```cpp
class Duree
{
    public:
 
    Duree(int heures = 0, int minutes = 0, int secondes = 0);

    private:

    void affiche(ostream& out) const;  //Permet d'écrire la durée dans un flux
 
    int m_heures;
    int m_minutes;
    int m_secondes;

    friend std::ostream& operator<< (std::ostream& flux, Duree const& duree);
    // peut etre mise dans public, private, protected : ça n'a aucun impact
};
```
```cpp
ostream &operator<<( ostream &out, Duree const& duree )
{
    duree.afficher(out) ;
    return out;
}
```

## Conteneurs

### Conteneurs séquences

- `vector`
- `deque`
- `list`
- `stack`
- `queue`
- `priority_queue`

### Conteneurs associatifs

- `set`
- `multiset`
- `map`
- `multimap`

### Méthodes communes

- `empty()`
- `clear()`
- `swap()`

### Utiliser séquences et leurs adaptateurs

- `vector`
    - `push_back()`
    - `pop_back()`
    - `front()` -> accès premiere case
    - `back()` -> accès derniere case
    - `assign()` -> modif contenu d'un tableau
- `deque` -> "double ended queue"
    - `push_front()` -> ajoute un élement en tete de file
    - `push_back()` -> ajoute un element en fin de file
- `stack`
    - `push()`
    - `top()`
    - `pop()`
- `queue`
    - `push()`
    - `front()` -> equivalent du top()
    - `pop()`
- `prority_queue`
    - `push()`
    - `top()` -> affiche le plus grand nombre stocké
    - `pop()`

### Utiliser les tables associatives

```cpp
#include <map>
#include <string>
using namespace std;

map<string, int> a;

a["salut"] = 3; //La case "salut" de la map vaut maintenant 3
```
C'est donc un dictionnaire.
```cpp
#include <map>
#include <string>
#include <fstream>
#include <iostream>
using namespace std;

int main()
{
    ifstream fichier("texte.txt");
    string mot;
    map<string, int> occurrences;
    while(fichier >> mot)   //On lit le fichier mot par mot
    {
         ++occurrences[mot]; //On incrémente le compteur pour le mot lu
    }
    cout << "Le mot 'banane' existe " << occurrences["banane"] << " fois dans le fichier" << endl; 
    return 0;
}
```

Autres tables associatives :

Utilisent les itérateurs.

## Itérateurs et foncteurs

### Parcourir conteneurs avec itérateurs

Déclaration
```cpp
#include <vector>
using namespace std;

vector<int> tableau(5,4);     //Un tableau de 5 entiers valant 4
vector<int>::iterator it;     //Un itérateur sur un vector d'entiers

map<string, int>::iterator it1; //Un itérateur sur les tables associatives string-int

deque<char>::iterator it2; //Un itérateur sur une deque de caractères 

list<double>::iterator it3; //Un itérateur sur une liste de nombres à virgule
```

Itération
```cpp
#include<deque>
#include <iostream>
using namespace std;

int main()
{
    deque<int> d(5,6);        //Une deque de 5 éléments valant 6
    deque<int>::iterator it;  //Un itérateur sur une deque d'entiers

    //Et on itère sur la deque
    for(it = d.begin(); it!=d.end(); ++it)
    {
        cout << *it << endl;    //On accède à l'élément pointé via l'étoile
    }
    return 0;
}
```

Méthodes
```cpp
#include <vector>
#include <string>
#include <iostream>
using namespace std;

int main()
{
    vector<string> tab;    //Un tableau de mots

    tab.push_back("les"); //On ajoute deux mots dans le tableau
    tab.push_back("Developpeurs");

    tab.insert(tab.begin(), "Salut"); //On insère le mot "Salut" au début

    //Affiche les mots donc la chaîne "Salut les Developpeurs"
    for(vector<string>::iterator it=tab.begin(); it!=tab.end(); ++it)
    {
        cout << *it << " ";
    }

    tab.erase(tab.begin()); //On supprime le premier mot

    //Affiche les mots donc la chaîne "les Developpeurs"
    for(vector<string>::iterator it=tab.begin(); it!=tab.end(); ++it)
    {
        cout << *it << " ";
    }

    return 0;
}
```

### Différents itérateurs

- Bidirectionnal iterators
    - ne peuvent parcourir qu'un élément à la fois, en partant du début
    - les seuls opérateurs sont ++ et --
    - utilisés pour `list`, `set` et `map`
- Random access iterators
    - peuvent avancer de plusieurs éléments à la fois
    - commencer à partir de n'importe quel élément
    - opérateurs : ++, --, +, -
    - utilisés pour `vector` et `deque`

### Utilisr `list` et `map`

`list` = liste chainée
```cpp
#include <list>
#include <iostream>
using namespace std;

int main()
{
    list<int> liste;       //Une liste d'entiers
    liste.push_back(5);    //On ajoute un entier dans la liste
    liste.push_back(8);    //Et un deuxième
    liste.push_back(7);    //Et encore un !
    
    //On itère sur la liste
    for(list<int>::iterator it = liste.begin(); it!=liste.end(); ++it)
    {
        cout << *it << endl;
    }
    return 0;
}
```

Pour les maps, l'itérateur pointe sur des `pair`, un couple clé-valeur  
Exemple :
```cpp
#include <utility>
#include <iostream>
using namespace std;

int main()
{
    pair<int, double> p(2, 3.14);    //Une paire contenant un entier valant 2 et un nombre à virgule valant 3.14

    cout << "La paire vaut (" << p.first << ", " << p.second << ")" << endl;

    // ----------------------------------------------------------------//

    map<string, double> poids; //Une table qui associe le nom d'un animal à son poids
    
    //On ajoute les poids de quelques animaux
    poids["souris"] = 0.05;
    poids["tigre"] = 200;
    poids["chat"] = 3;
    poids["elephant"] = 10000;

    //Et on parcourt la table en affichant le nom et le poids
    for(map<string, double>::iterator it=poids.begin(); it!=poids.end(); ++it)
    {
        cout << it->first << " pese " << it->second << " kg." << endl;
    }

    return 0;
}
``` 

Chercher un élément dans une `map`
```cpp
int main()
{
    map<string, double> poids; //Une table qui associe le nom d'un animal à son poids
    
    //On ajoute les poids de quelques animaux
    poids["souris"] = 0.05;
    poids["tigre"] = 200;
    poids["chat"] = 3;
    poids["elephant"] = 10000;

    map<string, double>::iterator trouve = poids.find("chien");

    if(trouve == poids.end())
    {
        cout << "Le poids du chien n'est pas dans la table" << endl;
    }
    else
    {
        cout << "Le chien pese " << trouve->second << " kg." << endl;
    }
    return 0;
}
```

### Creer un foncteur
```cpp
class Addition{
public:
    
    int operator()(int a, int b)   //La surcharge de l'opérateur ()
    {
        return a+b;
    }
};
```
```cpp
#include <iostream>
using namespace std;

int main()
{
    Addition foncteur;
    int a(2), b(3);
    cout << a << " + " << b << " = " << foncteur(a,b) << endl; //On utilise le foncteur comme s'il s'agissait d'une fonction
    return 0;
}
```

### Foncteurs évolutifs
```cpp
class Remplir{
public:
    Remplir(int i)
        :m_valeur(i)
    {}

    int operator()()
    {
        ++m_valeur;
        return m_valeur;
    }

private:
    int m_valeur;
};
```
Ici, permet de faire incrémenter l'attribut de la classe à chaque appel du foncteur.

Exemple pour remplir un `vector` de 1 à 100 :
```cpp
int main()
{ 
    vector<int> tab(100,0); //Un tableau de 100 cases valant toutes 0

    Remplir f(0);       

    for(vector<int>::iterator it=tab.begin(); it!=tab.end(); ++it)
    {
        *it = f(); //On appelle simplement le foncteur sur chacun des éléments du tableau
    }
    
    return 0;
}
```

### Prédicats : des foncteurs particuliers

```cpp
class TestVoyelles
{
public:
    bool operator()(string const& chaine) const
    {
        for(int i(0); i<chaine.size(); ++i)
        {
            switch (chaine[i])   //On teste les lettres une à une
            {
                case 'a':        //Si c'est une voyelle
                case 'e':
                case 'i':
                case 'o':
                case 'u':
                case 'y':
                    return true;  //On renvoie 'true'
                default:
                    break;        //Sinon, on continue
            }
        }
        return false;   //Si on arrive là, c'est qu'il n'y avait pas de  voyelle du tout
    }
};
```

### Foncteurs prédéfinis

```cpp
#include <iostream>
#include <functional>    //Ne pas oublier !
using namespace std;

int main()
{
    plus<int> foncteur;    //On déclare le foncteur additionnant deux entiers
    int a(2), b(3);
    cout << a << " + " << b << " = " << foncteur(a,b) << endl; //On utilise le foncteur comme s'il s'agissait d'une fonction
    return 0;
}
```

### Fusionner les deux concepts

#### Modifier comportement d'une `map`

Le constructeur d'une `map` peut en fait prendre un argument, un foncteur de comparaison.

```cpp
#include <string>
using namespace std;

class CompareLongueur
{
public:
    bool operator()(const string& a, const string& b)
    {
        return a.length() < b.length();
    }
};
```
```cpp
int main()
{
  //Une table qui associe le nom d'un animal à son poids
  map<string, double,CompareLongueur> poids;  //On utilise le foncteur comme critère de comparaison
        

  //On ajoute les poids de quelques animaux       
  poids["souris"] = 0.05;
  poids["tigre"] = 200;
  poids["chat"] = 3;
  poids["elephant"] = 10000;

  //Et on parcourt la table en affichant le nom et le poids
  for(map<string, double>::iterator it=poids.begin(); it!=poids.end(); ++it)
  {
      cout << it->first << " pese " << it->second << " kg." << endl;
  }
  return 0;
}
```

## Puissance des algorithmes
```cpp
#include <algorithm>
#include <vector>
using namespace std;

//Définition de Remplir…

int main()
{ 
    vector<int> tab(100,0); //Un tableau de 100 cases valant toutes 0

    Remplir f(0);       

    generate(tab.begin(), tab.end(), f);
    //On applique f à tout ce qui se trouve entre begin() et end()
    
    return 0;
}
```
```cpp
int main()
{ 
    vector<int> tab(100,0); //Un tableau de 100 cases valant toutes 0

    Remplir f(0);       

    generate(tab.begin(), tab.begin()+10, f); //On applique f aux 10 premières cases
    generate(tab.end()-5, tab.end(), f);      //Et aux 5 dernières
    
    return 0;
}
```

Possible de faire pareil avec une `list` par exemple :
```cpp
int main()
{ 
    list<int> tab; //Une liste d'entiers

    //Quelques manipulations pour créer des éléments…

    Remplir f(0);       

    generate(tab.begin(), tab.end(), f); //On applique f aux éléments de la liste
    
    return 0;
}
```

### Compter avec les algos `count` et `count_if`

- `count` utilise une valeur en 3e argument
- `count_if` utlise un prédicat en 3 argument
```cpp
#include <iostream>
#include <cstdlib> //pour rand()                                                     
#include <ctime>   //pour time()                                                     
#include <vector>
#include <algorithm>
using namespace	std;

class Generer
{
public:
    int operator()() const
    {
        return rand() % 10;  //On renvoie un nombre entre 0 et 9
    }
};

int main()
{
    srand(time(0));

    vector<int> tab(100,-1); //Un tableau de 100 cases                                  

    generate(tab.begin(), tab.end(), Generer());  //On génère les nombres aléatoires                                                                

    int const compteur = count(tab.begin(), tab.end(), 5); //Et on compte les occurrences du 5 

    cout << "Il y a " << compteur << " elements valant 5." << endl;

    return 0;
}
```
```cpp
#include <algorithm>
#include <string>
#include <vector>
using namespace std;

class TestVoyelles
{
public:
    bool operator()(string const& chaine) const
    {
        for(int i(0); i<chaine.size(); ++i)
        {
            switch (chaine[i])   //On teste les lettres une à une
            {
                case 'a':        //Si c'est une voyelle
                case 'e':
                case 'i':
                case 'o':
                case 'u':
                case 'y':
                    return true;  //On renvoie 'true'
                default:
                    break;        //Sinon, on continue
            }
        }
        return false;   //Si on arrive là, c'est qu'il n'y avait pas de voyelle du tout
    }
};

int main()
{
    vector<string> tableau;

    //… On remplit le tableau en lisant un fichier, par exemple.

    int const compteur = count_if(tableau.begin(), tableau.end(), TestVoyelles());

    //… Et on fait quelque chose avec 'compteur'

    return 0;
}
```

### `find` et `find_if`

Même concept que pour count, `find` utilise une valeur, tandis que `find_if` utilise un prédicat
```cpp
#include <deque>
#include <algorithm>
#include <iostream>
using namespace std;

int main()
{
    deque<char> lettres;

    //On remplit la deque… avec generate() par exemple !

    deque<char>::iterator trouve = find(lettres.begin(), lettres.end(), 'a');

    if(trouve == lettres.end())
        cout << "La lettre 'a' n'a pas ete trouvee" << endl;
    else
        cout << "La lettre 'a' a ete trouvee" << endl;

    return 0;
}
```

### Trier avec `sort`

Applicable UNIQUEMENT sur des Random Access Iterators, donc :
- `vector`
- `deque`
```cpp
int main()
{
    srand(time(0));

    vector<int> tab(100,-1); //Un tableau de 100 cases                                 

    generate(tab.begin(), tab.end(), Generer()); //On génère les nombres aléatoires        

    sort(tab.begin(), tab.end());                //On trie le tableau

    for(vector<int>::iterator it=tab.begin(); it!=tab.end(); ++it)
        cout << *it << endl;                     //On affiche le tableau trié

    return 0;
}
```

```cpp
class ComparaisonLongueur
{
public:
    bool operator()(const string& a, const string& b)
    {
        return a.length() < b.length();
    }
};

int main()
{
    vector<string> tableau;

    //… On remplit le tableau en lisant un fichier par exemple.

    sort(tableau.begin(), tableau.end(), ComparaisonLongueur());

    //Le tableau est maintenant trié par longueur de chaîne

    return 0;
}
```

### Afficher contenu d'un `vector`

```cpp
class Afficher
{
public:
    void operator()(int a) const
    {
        cout << a << endl;
    }
};
```
```cpp
int main()
{
    srand(time(0));
    vector<int> tab(100, -1);
    generate(tab.begin(), tab.end(), Generer());  //On génère des nombres aléatoires
    sort(tab.begin(), tab.end());

    for_each(tab.begin(), tab.end(), Afficher());   //Et on affiche les éléments
    
    return 0;
}
```
Autre exemple :
```cpp
class Sommer
{
public:
    Sommer()
        :m_somme(0)
    {}

    void operator()(int n)
    { 
        m_somme += n; 
    }

    int resultat() const
    {
        return m_somme;
    }

private:
    int m_somme;

};
```
```cpp
int main()
{
    srand(time(0));
    vector<int> tab(100, -1);
    generate(tab.begin(), tab.end(), Generer());  //On génère des nombres aléatoires

    Sommer somme;

    //On somme les éléments et on récupère le foncteur utilisé
    somme = for_each(tab.begin(), tab.end(), somme);   
 
    cout << "La somme des elements generes est : " << somme.resultat() << endl;
   
    return 0;
}
```

### Traiter deux conteneurs en meme temps : `transform()`

Arguments de `transform()` :
- début du premier tableau
- fin du premier tableau
- début du deuxième tableau
- début du troisième tableau
- foncteur
```cpp
#include <vector>
#include <algorithm>
#include <functional>
using namespace std;

int main()
{
    vector<double> a(50, 0.);    //Trois tableaux de 50 nombres à virgule
    vector<double> b(50, 0.);
    vector<double> c(50, 0.);
   
    //Remplissage des vectors 'a' et 'b'….

    transform(a.begin(), a.end(), b.begin(), c.begin(), plus<double>());

    //À partir d'ici les cases de 'c' contiennent la somme des cases de 'a' et 'b'

    return 0;
}
```
ATTENTION, b et c doivent avoir une taille minimum pour que cela fonctionne (>=`a.size()`)

## Utiliser les itérateurs sur les flux

Il y a en fait deux autres types d'itérateurs :
- itérateurs sur flux entrants
- itérateurs sur flux sortants

Ils ne possèdent que l'opérateur `++`

### Itérateur sur flux sortant
```cpp
#include <iostream>
#include <iterator>
using namespace std;

int main()
{
    ostream_iterator<double> it(cout);
    *it = 3.14;
    *it = 2.71;

    return 0;
}

// Affiche 3.142.71
```
```cpp
#include <iostream>
#include <iterator>
using namespace std;

int main()
{
    ostream_iterator<double> it(cout, ", ");
    *it = 3.14;
    *it = 2.71;

    return 0;
}

// Affiche 3.14, 2.71
```

### Itérateur sur flux entrant
```cpp
#include <fstream>
#include <iterator>
using namespace std;

int main()
{
    ifstream fichier("C:/Nanoc/data.txt");
    istream_iterator<double> it(fichier); 

    double a,b;
    a = *it;    //On lit le premier nombre du fichier
    ++it;       //On passe au suivant
    b = *it;    //On lit le deuxième nombre

    return 0;
}
```
```cpp
#include <fstream>
#include <iterator>
#include <iostream>
using namespace std;

int main()
{
    ifstream fichier("data.txt");
    istream_iterator<double> it(fichier); //Un itérateur sur le fichier                           
    istream_iterator<double> end;         //Le signal de fin

    while(it != end)   //Tant qu'on n'a pas atteint la fin
    {
        cout << *it << endl;  //On lit
        ++it;                 //Et on avance
    }
    return 0;
}
```
Itérateur sans valeur pointe vers un end_of_stream_iterator, utilisé pour une fin de fichier par exemple

### Algorithmes
`copy`
```cpp
#include <algorithm>
#include <vector>
#include <iterator>
#include <fstream>
using namespace std;

int main()
{
  vector<int> tab(100,0);
  ifstream fichier("C:/Nanoc/data.txt");
  istream_iterator<int> it(fichier);
  istream_iterator<int> fin;
  copy(it, fin, tab.begin());     //On copie le contenu du fichier du début à la fin dans le vector

  return 0;
}
```

```cpp
int main()
{
    srand(time(0));
    vector<int> tab(100,-1); //Un tableau de 100 cases

    //On génère les nombres aléatoires
    generate(tab.begin(), tab.end(), Generer());      
    //On trie le tableau   
    sort(tab.begin(), tab.end());                     
    //Et on l'affiche
    copy(tab.begin(), tab.end(), ostream_iterator<int>(cout, "\n");
    return 0;
}
```

Pour régler le problème des tailles de tableaux, il existe les `back_insert_iterator`

```cpp
#include <algorithm>
#include <vector>
#include <iterator>
#include <fstream>
using namespace std;

int main()
{
  vector<int> tab;   //Un tableau vide
  ifstream fichier("C:/Nanoc/data.txt");
  
  istream_iterator<int> it(fichier);
  istream_iterator<int> fin;
  back_insert_iterator<vector<int> > it2(tab);
  
  //L'algorithme ajoute les cases nécessaires au tableau
  copy(it, fin, it2);  

  return 0;
}
```
On peut aussi utiliser `count`, `min_element` et `max_element` pour les fichiers :
```cpp
ifstream fichier("C:/Nanoc/data.txt");
cout << *min_element(istream_iterator<int>(fichier), istream_iterator<int>()) << endl;
```

### Inserer des nombres dans une `string`
```cpp
#include <string>
#include <sstream>
#include <iostream>
using namespace std;

int main()
{
  ostringstream flux;   //Un flux permettant d'écrire dans une chaîne            

  flux << "Salut les";  //On écrit dans le flux grâce à l'opérateur <<          
  flux << " developpeurs";
  flux << " !";

  string const chaine = flux.str(); //On récupère la chaîne                     

  cout << chaine << endl;  //Affiche 'Salut les developpeurs !'                        
  return 0;
}
```

```cpp
string chaine("Le nombre pi vaut: ");
double const pi(3.1415);

ostringstream flux;
flux << chaine;
flux << pi;

cout << flux.str() << endl;
```
Il existe aussi `istringstream` pour la lecture.

## Aller plus loin avec la SL (Standard Library)

### Itérateurs avec les `string`

```cpp
#include <iostream>
#include <string>
#include <algorithm>
#include <cctype>
using namespace std;

class Convertir
{
public:
    char operator()(char c) const
    {
        return toupper(c);
    }
};

int main()
{
    string chaine("Salut les developpeurs !");
    transform(chaine.begin(), chaine.end(), chaine.begin(), Convertir());
    cout << chaine << endl;
    return 0;
}
```

### Manipuler tableaux statiques
```cpp
#include <algorithm>
using namespace std;

int main()
{
    int const taille(1000); 
    double tableau[taille];     //On déclare un tableau 
    
    //Remplissage du tableau…

    // Itérateurs
    double* debut(tableau);         // équivalent de `begin()`
    double* fin(tableau+taille);    // équivalent de `end()`
    
    sort(debut, fin);           //Et on trie

    return 0;
}
```

### Calcul scientifique

#### Nombres complexes

```cpp
#include <complex>
#include <iostream>
using namespace std;

int main()
{
    complex<double> c(2,3);
    cout << c << endl;

    complex<double> a(1., 2.), b(-2, 4), c;
    c = sqrt(a+b);

    a = cos(c/b) + sin(b/c);

    complex<double> a(3,4);
    cout << norm(conj(a)) << endl; //Affiche '5' (norme et conjugué)

    return 0;
}
```

#### Opération dans tableaux avec `valarray`
```cpp
#include<valarray>
using namespace std;

int main()
{
    // ATTENTION : constructeur inversé avec les `vector` (valeur d'abord, puis nombre de cases)
    valarray<int> a(10, 5);  //5 éléments valant 10
    valarray<int> b(8, 5);   //5 éléments valant 8

    valarray<int> c = a + b;  //Chaque élément de c vaut 18
    return 0;
}
```
```cpp
#include<valarray>
#include<cmath>
using namespace std;

class Cosinus   //Un foncteur pour le calcul du cosinus
{
public:
    double operator()(double x) const
    {
        return cos(x);
    }
};

int main()
{
    valarray<double> a(10);  //10 éléments
    
    //Remplissage du tableau…

    a.apply(Cosinus);

    //Chaque case contient maintenant le cosinus de son ancienne valeur

    return 0;
}
```

## Gérez des erreurs avec les exceptions

### Gestion d'erreurs

```cpp
// Du code sans risque.
try
{
   // Du code qui pourrait créer une erreur.
}
```
```cpp
throw 123;   // On lance l'entier 123, par exemple si l'erreur 123 est survenue
 
throw string("Erreur fatale. Contactez un administrateur"); // On peut lancer un string.
 
throw Personnage; // On peut tout à fait lancer une instance d'une classe.

throw 3.14 * 5.12; // Ou même le résultat d'un calcul
```
Exemple concret :
```cpp
int division(int a,int b) // Calcule a divisé par b.
{
   if(b==0)
      throw string("ERREUR : Division par zéro !");
   else
      return a/b;
}
 
int main()
{
    int a,b;
    cout << "Valeur pour a : ";
    cin >> a;
    cout << "Valeur pour b : ";
    cin >> b;
 
    try
    {
        cout << a << " / " << b << " = " << division(a,b) << endl;
    }
    catch(string const& chaine)
    {
        cerr << chaine << endl;
    }
    return 0;
}
```

### Gestion d'exceptions standard

```cpp
class exception 
{
public:
    exception() throw(){ } //Constructeur.
    virtual  ~exception() throw(); //Destructeur.
 
    virtual const char* what() const throw(); //Renvoie une chaîne "à la C" contenant des infos sur l'erreur.
};
```
Exemple concret :
```cpp
#include <exception>
using namespace std;
 
class Erreur: public exception
{
public:
    Erreur(int numero=0, string const& phrase="", int niveau=0) throw()
         :m_numero(numero),m_phrase(phrase),m_niveau(niveau)
    {}
 
     virtual const char* what() const throw()
     {
         return m_phrase.c_str();
     }
     
     int getNiveau() const throw()
     {
          return m_niveau;
     }
    
    virtual ~Erreur() throw()
    {}
 
private:
    int m_numero;               //Numéro de l'erreur
    string m_phrase;            //Description de l'erreur
    int m_niveau;               //Niveau de l'erreur
};
```
```cpp
int division(int a,int b) // Calcule a divisé par b.
{
   if(b==0)
      throw Erreur(1,"Division par zéro",2);
   else
      return a/b;
}
 
int main()
{
   int a,b;
   cout << "Valeur pour a : ";
   cin >> a;
   cout << "Valeur pour b : ";
   cin >> b;
 
   try
   {
       cout << a << " / " << b << " = " << division(a,b) << endl;
   }
   catch(std::exception const& e)
   {
       cerr << "ERREUR : " << e.what() << endl; // ERREUR : division par zéro
   }
 
   return 0;
}
```

```cpp
#include <iostream>
#include <vector>
using namespace std; 

int main()
{
    try
    {
        vector<int> a(1000000000,1); //Un tableau bien trop grand
    }
    catch(exception const& e) //On rattrape les exceptions standard de tous types
    {
        cerr << "ERREUR : " << e.what() << endl; //On affiche la description de l'erreur
        // ERREUR : std::bad_alloc
        // C'est une exception de la bibliothèque standard
    }
    return 0;
}
```

### Utiliser le fichier `stdexcept` pour faciliter la tache

Il contient 2 catégories d'exceptions :
- Exceptions logiques
    - `domain_error` : Erreur de domaine mathématique.
    - `invalid_argument` : Argument invalide passé à une fonction.
    - `length_error` : Taille invalide.
    - `out_of_range` : Erreur d'indice de tableau.
    - `logic_error` : Autre problème de logique.
- Exceptions d'exécution
    - `range_error` : Erreur de domaine.
    - `overflow_error` : Erreur d'overflow.
    - `underflow_error` : Erreur d'underflow.
    - `runtime error` : Autre type d'erreur.    (Si on ne sait pas quoi choisir parmi les 3 autres, on prend ça)

Exemple :
```cpp
int division(int a,int b) // Calcule a divisé par b.
{
   if(b==0)
      throw domain_error("Division par zéro");
   else
      return a/b;
}
```

### Exceptions des `vector` (et `deque`)

```cpp
#include <vector>
#include <iostream>
using namespace std;

int main()
{
    vector<double> tab(5, 3.14);  //Un tableau de 5 nombres décimaux

    try
    {
        tab.at(8) = 4.;  //On essaye de modifier la 8ème case
    }
    catch(exception const& e)
    {
        cerr << "ERREUR : " << e.what() << endl;
        // ERREUR : vector::_M_range_check
    }
    return 0;
}
```

### Assertions
```cpp
#include <cassert>
using namespace std;

int main()
{
    int a(5);
    int b(5);

    assert(a == b) ; //On vérifie que a et b sont égaux
    
    //reste du programme
    return 0;
}
```
Ne fait rien si la condition renvoie `true`, mais dans le cas contraire :
- ```monProg: main.cpp:9: int main(): Assertion `a == b' failed.```

### Désactiver les assertions

Pourquoi ?
- Rendre le code plus rapide

Mais risqué car plus aucun test ne sera effectué.

Il faut rajouter `-DNDEBUG` à la ligne de compilation pour les désactiver.

## Créer des templates

### Fonctions `template`

#### Déclarer un type générique

```cpp
#include <iostream>
using namespace std;

template <typename T>
T maximum(const T& a,const T& b)
{
   if(a>b)
      return a;
   else
      return b;
}

int main()
{
     double pi(3.14);
     double e(2.71);

     cout << maximum<double>(pi,e) << endl; //Utilise la "version double"de la fonction

     int cave(-1);
     int dernierEtage(12);

     cout << maximum<int>(cave,dernierEtage) << endl; //Utilise la "version int" de la fonction

     unsigned int a(43);
     unsigned int b(87);

     cout << maximum<unsigned int>(a,b) << endl; //Utilise la "version unsigned int" de la fonction.

     return 0;
}
```
Mais on est pas obligé d'utiliser les `<>`, le compilateur traduit automatiquement:
```cpp
int main()
{
    double pi(3.14);
    double e(2.71);

    cout << maximum(pi,e) << endl; //Utilise la "version double" de la fonction
    return 0;
}
```

ATTENTION : une fonction `template` doit se situer forcément dans un fichier .hpp, le prototype comme la définition.

### Fonctions plus complexes
```cpp
#include<iostream>
using namespace std;

template<typename T, typename S>
S moyenne(T tableau[], int taille)
{
  S somme(0);                  //La somme des éléments du tableau
  for(int i(0); i<taille; ++i)
    somme += tableau[i];

  return somme/taille;
}

int main()
{
  int tab[5];
  //Remplissage du tableau

  cout << "Moyenne : " << moyenne<int,double>(tab,5) << endl; 
  // Ici, il faut expliciter les types car deux arguments

  return 0;
}
```

### Spécialiser une fonction `template`

```cpp
template <>
string maximum<string>(const string& a, const string& b)
{
  if(a.size()>b.size())
    return a;
  else
    return b;
}
```
```cpp
int main()
{
  cout << "Le plus grand est: " << maximum<std::string>("elephant","souris") << endl;
  // Le plus grand est: elephant

  return 0;
}
```

### Classes `template`

```cpp
template <typename T>
class Rectangle{
public:
    //…

   T hauteur() const
   {
      return m_haut-m_bas;
   }

private:
   
   //Les côtés du Rectangle
   T m_gauche;
   T m_droite;
   T m_haut;
   T m_bas;
};
```
Si on veut la fonction en dehors de la classe :
```cpp
template <typename T>
class Rectangle{
public:
    //…

   T hauteur() const; 
   
    //…
};

template<typename T>
T Rectangle<T>::hauteur() const
{
   return m_haut-m_bas;
}
```

En rajoutant quelques éléments :
```cpp
template <typename T>
class Rectangle{
public:
    //…

    Rectangle(T gauche, T droite, T haut, T bas)
        :m_gauche(gauche),
         m_droite(droite),
         m_haut(haut),
         m_bas(bas)
   {}

   T hauteur() const
   {
      return m_haut-m_bas;
   }

   bool estContenu(T x, T y) const
   {
      return (x >= m_gauche) && (x <= m_droite) && (y >= m_bas) && (y <= m_haut);
   }

private:
   
   //Les côtés du Rectangle
   T m_gauche;
   T m_droite;
   T m_haut;
   T m_bas;
};
```
Et maintenant pour l'instancier :
```cpp
int main()
{
   Rectangle<double> monRectangle(1.0, 4.5, 3.1, 5.2);

   cout << monRectangle.hauteur() << endl;
  
   return 0;
}
```

## Fin du cours

### Héritage multiple

```cpp
class FenCalculatrice : public QWidget, public Ui::FenCalculatrice
{

};
```

### Types énumérés

```cpp
enum Niveau{Facile, Moyen, Difficile};

int main()
{
    Niveau level;

    //…

    if(level == Moyen)
        cout << "Vous avez choisi le niveau moyen" << endl;
    //…
    
    return 0;
}
```

```cpp
enum Direction{Nord, Sud, Est, Ouest};

int main()
{
    Direction dir;
    Personnage p;

    //…

    switch(dir)
    {
        case Nord: p.avancerNord(); break;
        case Sud: p.avancerSud(); break;
        case Est: p.avancerEst(); break;
        case Ouest: p.avancerOuest(); break;
    }

    //…

    return 0;
}
```

### Les `typedef`

```cpp
std::map<std::string, std::vector<int> >::iterator it;
```
C'est très long d'écrire ce type, donc on peut utiliser un `typedef`

```cpp
typedef std::map<std::string, std::vector<int> >::iterator Iterateur;

// Maintenant, on peut déclarer un itérateur beaucoup plus facilement !
Iterateur it;
```

### Utiliser d'autres bibliothèques

- Jeux en 2D :
    - `Allegro`
    - `SFML`
- 3D :
    - `Irrlicht`
    - `Ogre3D`
- Créer des programmes en fenêtre :
    - `wxWidgets`
    - `.NET`
- Manipuler du son :
    - `FMOD EX`
- Compléter la bibliothèque standard :
    - `boost` (Visiblement très utile !)