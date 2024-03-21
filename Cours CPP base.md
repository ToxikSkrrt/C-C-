# COURS

## cout / cin (= printf / scanf en C)
```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    cout << "Combien vaut pi ?" << endl;
    double piUtilisateur(-1.); //On crée une case mémoire pour stocker unnombre réel
    cin >> piUtilisateur; //Et on remplit cette case avec ce qu'écritl'utilisateur

    cin.ignore();   // IMPORTANT ! nécessaire lors d'une lecture par mot avant lecture par ligne 
                    // (cin >> ... avant getlin(cin, ...))

    cout << "Quel est votre nom ?" << endl;
    string nomUtilisateur("Sans nom"); //On crée une case mémoire pour contenir une chaine de caractères
    getline(cin, nomUtilisateur); //On remplit cette case avec toute la ligne que l'utilisateur a écrit

    cout << "Vous vous appelez " << nomUtilisateur << " et vous pensez que pi vaut " << piUtilisateur << "." << endl;

    return 0;
}

```

## Exemple sur les constantes
```cpp
string const motDePasse("wAsTZsaswQ"); //Le mot de passe secret
double const pi(3.14);
unsigned int const pointsDeVieMaximum(100); //Le nombre maximal de points de vie
```

## Exercice 1

```cpp
#include <iostream>
using namespace std;

int main()
{
    int n1, n2;

    cout << "n1 : " << endl;
    cin >> n1;
    cin.ignore();

    cout << "n2 : " << endl;
    cin >> n2;
    cin.ignore();


    cout << "resultat : " << n1 + n2 << endl;

    return 0;
}
```

## test 2 corrigé

```cpp
//
//  main.cpp
//  convertisseur
//
//  Created by Ranga Gonnage on 14/12/2021.
//

#include <iostream>

using namespace std;

int main() {
    double euroUtilisateur(0);
    double const ratioDollar(1.20);
    
    cout << "Convertisseur euro -> dollar" << endl;
    
    cout << "Entrez un montant à convertir en dollar : ";
    cin >> euroUtilisateur;
    
    double resultat = euroUtilisateur * ratioDollar;
    
    if (euroUtilisateur < 0)
    {
        cout << "La saisie est incorrecte ! " << endl;
    }
    else
    {
        cout << euroUtilisateur << "€ équivaut à " << resultat << "$" << endl;
    }

    return 0;
}

// Solution avec la boucle pour la question 8

/*
int main() {
    double euroUtilisateur(0);
    double const ratioDollar(1.20);
    
    cout << "Convertisseur euro -> dollar" << endl;
    
    do
    {
        cout << "Entrez un montant à convertir en dollar : ";
        cin >> euroUtilisateur;
        
        double resultat = euroUtilisateur * ratioDollar;
        
        if (euroUtilisateur < 0)
        {
            cout << "La saisie est incorrecte ! " << endl;
        }
        else
        {
            cout << euroUtilisateur << "€ équivaut à " << resultat << "$" << endl;
        }
    } while (euroUtilisateur < 0);
    
    return 0;
}
*/
```

## Exercice sur le for
```cpp
#include <iostream>
using namespace std;

int dessineRectangle(int l, int h)
{
    if (l < 0 || h < 0)
    {
        cerr << "Erreur" << endl;
        exit(1);
    }

    for(int ligne(0); ligne < h; ligne++)
    {
        for(int colonne(0); colonne < l; colonne++)
        {
            cout << "*";
        }
        cout << endl;
    }

    return l * h;
}

int main()
{
    int largeur, hauteur;
    cout << "Largeur du rectangle : ";
    cin >> largeur;
    cout << "Hauteur du rectangle : ";
    cin >> hauteur;

    int surf = dessineRectangle(largeur, hauteur);

    cout << "Surface du rectangle = " << surf << endl;
    return 0;
}
```


## Tableau statique
```cpp
#include <iostream>
using namespace std;

int main()
{
   int const nombreNotes(6);
   double notes[nombreNotes];

   notes[0] = 12.5;
   notes[1] = 19.5;  //Bieeeen !
   notes[2] = 6.;    //Pas bien !
   notes[3] = 12;
   notes[4] = 14.5;
   notes[5] = 15;
   
   double moyenne(0);
   for(int i(0); i<nombreNotes; ++i)
   {
      moyenne += notes[i];   //On additionne toutes les notes
   }
   //En arrivant ici, la variable moyenne contient la somme des notes (79.5)
   //Il ne reste donc qu'à diviser par le nombre de notes
   moyenne /= nombreNotes;
   
   cout << "Votre moyenne est : " << moyenne << endl;

   return 0;
}
```

## Exemple utilisation des références
```cpp
#include <iostream>
using namespace std;

void swap(int& a, int& b) {
    int tmp = a;
    a = b;
    b = tmp;
}

int main() {
    int a(10), b(20);
    cout << "a = " << a << ", b = " << b << endl;
    swap(a, b);
    cout << "a = " << a << ", b = " << b << endl;
    return 0;
}
```

## Tableau dynamique
```cpp
#include <iostream>
#include <vector> //Ne pas oublier !
using namespace std;

int main()
{
    vector<int> tab(5, 3);  //Crée un tableau de 5 entiers valant tous 3
    vector<string> listeNoms(12, "Sans nom"); //Crée un tableau de 12 strings valant toutes « Sans nom »

    int const nombreMeilleursScores(5);  //La taille du tableau

    vector<int> meilleursScores(nombreMeilleursScores);  //Déclaration du tableau

    meilleursScores[0] = 118218;  //Remplissage de la première case
    meilleursScores[1] = 100432;  //Remplissage de la deuxième case
    meilleursScores[2] = 87347;   //Remplissage de la troisième case
    meilleursScores[3] = 64523;   //Remplissage de la quatrième case
    meilleursScores[4] = 31415;   //Remplissage de la cinquième case


    vector<int> tableau(3,2); //Un tableau de 3 entiers valant tous 2
    tableau.push_back(8);  //On ajoute une 4ème case qui contient la valeur 8
    tableau.push_back(7);  //On ajoute une 5ème case qui contient la valeur 7
    tableau.push_back(14); //Et encore une avec le nombre 14 cette fois

    //Le tableau contient maintenant les nombres : 2 2 2 8 7 14

    vector<int> tableau(3,2); //Un tableau de 3 entiers valant tous 2
    tableau.pop_back(); //Et hop ! Plus que 2 cases
    tableau.pop_back(); //Et hop ! Plus que 1 case

    vector<int> tableau(5,4); //Un tableau de 5 entiers valant tous 4
    int const taille(tableau.size());
    //Une variable qui contient la taille du tableau
    //La taille peut varier mais la valeur de cette variable ne changera pas
    //On utilise donc une constante
    //À partir d'ici, la constante 'taille' vaut donc 5

    return 0;
}
```

## Exemple avec tableau dynamique
```cpp
#include <iostream>
#include <vector> //Ne pas oublier !
using namespace std;

int main()
{
   vector<double> notes; //Un tableau vide

   notes.push_back(12.5);  //On ajoute des cases avec les notes
   notes.push_back(19.5);
   notes.push_back(6);
   notes.push_back(12);
   notes.push_back(14.5);
   notes.push_back(15);
   
   double moyenne(0);
   for(int i(0); i<notes.size(); ++i)
   //On utilise notes.size() pour la limite de notre boucle
   {
      moyenne += notes[i];   //On additionne toutes les notes
   }

   moyenne /= notes.size();
   //On utilise à nouveau notes.size() pour obtenir le nombre de notes
   
   cout << "Votre moyenne est : " << moyenne << endl;

   return 0;
}
```

## Passage d'un vector en argument de fonction
```cpp
//Une fonction recevant un tableau d'entiers en argument (PAR VALEUR)
void fonction(vector<int> a)
{
    //…
}

//Une fonction recevant un tableau d'entiers en argument (PAR REFERENCE)
void fonction(vector<int> const& a)
{
    //…
}

vector<int> tableau(3,2);   //On crée un tableau de 3 entiers valant 2
fonction(tableau);          //On passe le tableau à la fonction déclarée au-dessus
```

## Vector dans un autre fichier hpp
```cpp
#ifndef TABLEAU_H_INCLUDED
#define TABLEAU_H_INCLUDED

#include <vector>

void fonctionAvecTableau(std::vector<int>& tableau);

#endif // TABLEAU_H_INCLUDED
```

## Fonction qui renvoie un vector
```cpp
vector<double> encoreUneFonction(int a)
{
    //...
}
```

## Tableau 2D dynamique (pas recommandé)
```cpp
vector<vector<int>> grille;

grille.push_back(vector<int>(5));   //On ajoute une ligne de 5 cases à notre grille
grille.push_back(vector<int>(3,4)); //On ajoute une ligne de 3 cases contenant chacune le nombre 4 à notre grille
```

## Tableau 2D statique (recommandé)
```cpp
int const tailleX(5);
int const tailleY(4);
int tableau[tailleX][tailleY];
```

## String = tableau de type Vector
```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
   string nomUtilisateur("Julien");
   cout << "Vous etes " << nomUtilisateur << "." <<endl;

   nomUtilisateur[0] = 'L';  //On modifie la première lettre
   nomUtilisateur[2] = 'c';  //On modifie la troisième lettre
   nomUtilisateur.push_back('u');

   cout << "Ah non, vous etes " << nomUtilisateur << "!" << endl;


   string texte("Portez ce whisky au vieux juge blond qui fume.");  //46 caractères
   cout << "Cette phrase contient " << texte.size() << " lettres." << endl;


   string prenom("Albert"); 
   string nom("Einstein");
   
   string total;    //Une chaîne vide
   total += prenom; //On ajoute le prénom à la chaîne vide
   total += " ";    //Puis un espace
   total += nom;    //Et finalement le nom de famille

   cout << "Vous vous appelez " << total << "." << endl; 

   return 0;
}
```

## Manipulation de fichiers

### Ouverture
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main()
{
   ofstream monFlux("C:/Nanoc/scores.txt");
   //Déclaration d'un flux permettant d'écrire dans le fichier
   // C:/Nanoc/scores.txt
   return 0;


   string const nomFichier("C:/Nanoc/scores.txt");

    ofstream monFlux(nomFichier.c_str());
    //Déclaration d'un flux permettant d'écrire dans un fichier.


    ofstream monFlux("C:/Nanoc/scores.txt");  //On essaye d'ouvrir le fichier

    if(monFlux)  //On teste si tout est OK
    {
        //Tout est OK, on peut utiliser le fichier
    }
    else
    {
        cout << "ERREUR: Impossible d'ouvrir le fichier." << endl;
    }
}
```

### Ecriture (ofstream)
```cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main()
{
    string const nomFichier("C:/Nanoc/scores.txt");
    ofstream monFlux(nomFichier.c_str()); // ecriture classique
    ofstream monFlux(nomFichier.c_str(), ios::app); // ecriture sans ecrasement (append)

    if(monFlux)    
    {
        monFlux << "Bonjour, je suis une phrase écrite dans un fichier." << endl;
        monFlux << 42.1337 << endl;
        int age(36);
        monFlux << "J'ai " << age << " ans." << endl;
    }
    else
    {
        cout << "ERREUR: Impossible d'ouvrir le fichier." << endl;
    }
    return 0;
}
```

### Lecture (ifstream)
```cpp
ifstream monFlux("C:/Nanoc/C++/data.txt");  //Ouverture d'un fichier en lecture

if(monFlux)
{
    // Lecture par ligne
    string ligne;
    getline(monFlux, ligne); //On lit une ligne complète

    // Lecture par mot
    double nombre;
    monFlux >> nombre; //Lit un nombre à virgule depuis le fichier
    string mot;
    monFlux >> mot;    //Lit un mot depuis le fichier

    // Lecture par caractère
    char a;
    monFlux.get(a);

    // ATTENTION même problème que `cin` si on passe d'une lecture par mot à une lecture par ligne !
    ifstream monFlux("C:/Nanoc/C++/data.txt");

    string mot;
    monFlux >> mot;          //On lit un mot depuis le fichier

    monFlux.ignore();        //On change de mode

    string ligne;
    getline(monFlux, ligne); //On lit une ligne complète
}
else
{
    cout << "ERREUR: Impossible d'ouvrir le fichier en lecture." << endl;
}
```

#### Exemple de lecture complète d'un fichier
```cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std; 

int main()
{
   ifstream fichier("C:/Nanoc/fichier.txt");

   if(fichier)
   {
      //L'ouverture s'est bien passée, on peut donc lire

      string ligne; //Une variable pour stocker les lignes lues

      while(getline(fichier, ligne)) //Tant qu'on n'est pas à la fin, on lit
      {
         cout << ligne << endl;
         //Et on l'affiche dans la console
         //Ou alors on fait quelque chose avec cette ligne
         //À vous de voir
      }
   }
   else
   {
      cout << "ERREUR: Impossible d'ouvrir le fichier en lecture." << endl;
   }

   return 0;
}
```

### Fermeture d'un fichier
```cpp
void f()
{
    ofstream flux;  //Un flux sans fichier associé

    flux.open("C:/Nanoc/data.txt");  //On ouvre le fichier C:/Nanoc/data.txt

    //Utilisation du fichier

    flux.close();  //On referme le fichier
                   //On ne peut plus écrire dans le fichier à partir d'ici

    // -------------------------------------------------------------------------- //

    // fonctionne également si l'on veut ouvrir directement à la déclaration,
    // c'est une question de préférence
    ofstream flux("C:/Nanoc/data.txt");

    flux.close();
}
```

### Utilisation du curseur
```cpp
ofstream fichier("C:/Nanoc/data.txt");

int position = fichier.tellp(); //On récupère la position
// int position = fichier.tellg()   pour `ifstream`

cout << "Nous nous situons au " << position << "eme caractere du fichier." << endl;

// pour deplacer curseur (seekp pour ofstream / seekg pour ifstream)
flux.seekp(nombreCaracteres, position);
// 3 positions possibles :
// ios::beg
// ios::end
// ios::cur
```

### Trouver taille d'un fichier avec curseur
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main()
{
    ifstream fichier("C:/Nanoc/meilleursScores.txt");  //On ouvre le fichier
    fichier.seekg(0, ios::end);  //On se déplace à la fin du fichier

    int taille;
    taille = fichier.tellg();
    //On récupère la position qui correspond donc à la taille du fichier !

    cout << "Taille du fichier : " << taille << " octets." << endl;

    return 0;
}
```

## Pointeurs

### Exemples de pointeurs
```cpp
double *pointeurA(0);
//Un pointeur qui peut contenir l'adresse d'un nombre à virgule

unsigned int *pointeurB(0);
//Un pointeur qui peut contenir l'adresse d'un nombre entier positif

string *pointeurC(0);
//Un pointeur qui peut contenir l'adresse d'une chaîne de caractères

vector<int> *pointeurD(0);
//Un pointeur qui peut contenir l'adresse d'un tableau dynamique de nombres entiers

int const *pointeurE(0);
//Un pointeur qui peut contenir l'adresse d'un nombre entier constant


// IMPORTANT : ne pas oublier d'initialiser à 0 les pointeurs !! (= NULL en C en terme d'équivalence)
```

### Stocker une adresse
```cpp
int main()
#include <iostream>
using namespace std;

int main()
{
    int ageUtilisateur(16);
    int *ptr(0);  

    ptr = &ageUtilisateur;

    cout << "L'adresse de 'ageUtilisateur' est : " << &ageUtilisateur << endl; // affiche adresse
    cout << "La valeur de pointeur est : " << ptr << endl;  // affiche meme adresse
     cout << "La valeur est :  " << *ptr << endl;   // affiche valeur

    return 0;
}
```

### Recap rapide des pointeurs
Pour une variable `int nombre`  :
- `nombre` permet d'accéder à la valeur de la variable ;
- `&nombre` permet d'accéder à l'adresse de la variable.

Sur un pointeur `int *pointeur`  :
- `pointeur` permet d'accéder à la valeur du pointeur, c'est-à-dire à l'adresse de la variable pointée ;
- `*pointeur` permet d'accéder à la valeur de la variable pointée.

### Allocation dynamique
```cpp
int *pointeur(0);
pointeur = new int; // demnde une case memoire pouvant stocker un int, qui est ensuite pointée par `pointeur`

*pointeur = 2;  //On accède à la case mémoire pour en modifier la valeur

delete pointeur;    //On libère la case mémoire
pointeur = 0;       //On indique que le pointeur ne pointe plus vers rien
```

### Exemple d'allocation dynamique
```cpp
#include <iostream>
using namespace std;

int main()
{
   int* pointeur(0); // ou int* pointeur(null_ptr)
   pointeur = new int;

   cout << "Quel est votre age ? ";
   cin >> *pointeur;
   //On écrit dans la case mémoire pointée par le pointeur 'pointeur'

   cout << "Vous avez " << *pointeur << " ans." << endl;
   //On utilise à nouveau *pointeur
    delete pointeur;   //Ne pas oublier de libérer la mémoire
   pointeur = 0;       //Et de faire pointer le pointeur vers rien

   return 0;
}
```