# **Algorithmique et programmation avancée**

##  Objectif : Listes chainées
Exercice 1 
On se propose de réaliser un programme C qui permet de gérer, à l'aide d'une liste chainée, les étudiants ayant
passé le contrôle unifié. La structure représentant l'étudiant est définie par :
typedef struct etudiant {
 char Nom[30];
 float Note;
 int CNE;
} Etudiant ;
<br>
<br>

> **Définir les structures Maillon et Liste**

```java script
/* 1. Definir les structures Maillon et Liste. */
typedef struct etudiant {
    char nom[20];
    int note;
    int cne;
    struct etudiant * suivant;
} Etudiant;



typedef struct maillon {
    Etudiant etud;
    struct maillon * suivant;
} Maillon;

```

<br>

> ** Écrire une fonction InsererFin qui permet d'insérer un étudiant E à la fin de la liste**

```java script


/* 2. Ecrire une fonction InsererFin qui permet d'insÃ©rer un Ã©tudiant E Ã  la fin de la liste. */
int InsererFin (Maillon * L, Etudiant E) {
    Maillon *m, *ptr;
    m = (Maillon*)malloc(sizeof (Maillon) );
    if ( m != NULL ){
        m->etud = E;
        m->suivant = NULL;
        if( L  !=  NULL ){
            ptr = L;
            while ( ptr->suivant != NULL )
                ptr = ptr->suivant;
            ptr->suivant=m;
        } else
            L = m;
        return 1;
    }
    return 0;
}

```
<br>



> **Écrire une fonction RechercheMajorant qui permet de retourner l'étudiant ayant obtenu la meilleure note. Nous
supposons que la liste n'est pas vide**
<br>


```java script


/* 3. Ecrire une fonction RechercheMajorant qui permet de retourner l'Ã©tudiant ayant obtenu la meilleure note. Nous supposons que la liste n'est pas vide. */

Etudiant RechercheMajorant (Maillon L) {
    Etudiant E;
    float max ;
    Maillon *m;
    E = L.etud;
    max = E.note;
    m = L.suivant ;

    while ( m != NULL ) {
        if( max < m->etud.note ) {
            max = m->etud.note;
            E = m->etud;
        }
        m=m->suivant;
    }
    return E ;
}

```
<br>



> **Écrire une fonction MoyennePromotion qui permet d'afficher la moyenne de la promotion**
<br>


```java script
/* 4. Ecrire une fonction MoyennePromotion qui permet d'afficher la moyenne de la promotion. */
void MoyennePromotion (Maillon *L) {
    float S=0, moyenne;
    int N=0 ;
    Maillon *m ;
    if( L != NULL ) {
        m = L;
        while( m != NULL) {
            S += m->etud.note;
            N++;
            m = m->suivant;
        }
        moyenne = S/N;
        printf("La moyenne de la promotion est : %f ", moyenne) ;
    }
    else
    printf("\n Erreur la liste est vide ") ;
}

```
<br>



> **Écrire une fonction Construireliste qui permet de construire une nouvelle liste où les étudiants qui n'ont pas
validé le semestre sont au début de la liste et les étudiants ayant validé le semestre sont à la fin (utiliser les
fonctions qui gèrent une liste chainée)**
<br>


```java script

/* 5. Ecrire une fonction ConstruireListe qui permet de construire une nouvelle liste oÃ¹ les Ã©tudiants qui n'ont pas validÃ© le semestre sont au dÃ©but de la liste et les Ã©tudiants ayant validÃ© le semestre sont Ã  la fin (utiliser les fonctions qui gÃ¨rent une liste chainÃ©e).*/

void ConstruireListe (Maillon *L, Maillon * R) {
    Maillon * m;
    m = L;
    while ( m != NULL) {
        if( m->etud.note < 10 )
            InsererDebut( R, m->etud);
        else
            InsererFin( R, m->etud);
        m = m->suivant;
    }
}
```
<br>



> **Écrire une fonction SupprimerNonValide qui permet de supprimer les étudiants qui n'ont pas validé le semestre**
<br>


```java script
/* 6. Ecrire une fonction SupprimeronValide qui permet de supprimer les etudiants qui n'ont pas valide le semestre. */

void SupprimerNonValide (Maillon * L) {
    Maillon *m, *ptr, *pred ;

    while( L  != NULL  && L->etud.note < 10 ){

// suppression de tous les non validÃ©s successifs Au debut
        Ptr = L;
        L = L->suivant;
        free(ptr);
    }
    if (L  != NULL) {

// suppression des autres non validÃ©s aprÃ¨s avoir rencontrer au moins un validÃ©
        pred = L;
        ptr = L->suivant;
        while(ptr != NULL){
                if( ptr->etud.note<10 ) {
                        m = ptr;
                        pred->suivant = ptr->suivant;
                        ptr = ptr->suivant;
                         free(m);
                         }

                   else {
                            pred = ptr;
                            ptr = ptr->suivant;
                       }
               }
          }
}


int main() {

    Maillon * Liste;
    printf("Hello, World!\n");
    return 0;
}
```

---


<br>


# **Exercice 2**
On propose d'implémenter une liste circulaire d'entiers. Une liste circulaire est une liste chainée avec la particularité
que le dernier élément pointe sur le premier élément (tête de la liste).
Exemple : une liste chainée circulaire L

<br>
<br>

> **Définir les structures Maillon et Liste**

```java script
/* 1. Definir les structures Maillon et Liste. */

typedef struct maillon {
    int valeur;
    struct maillon * suivant;
} Maillon;
```
<br>



> **Écrire une fonction CreerMaillon qui permet de réserver l'espace mémoire pour un maillon, la fonction
retourne l'adresse du maillon créé**

```java script

/* 2. Ecrire une fonction CreerMaillon qui permet reserver l'espace memoire pour un maillon, la fonction retourne l'adresse du maillon cree. */
Maillon * CreerMaillon (int V) {
    Maillon *m ;
    m = (Maillon*) malloc(sizeof(Maillon));
    if( m != NULL ) {
        m->valeur = V ;
        m->suivant=NULL;
    }
    return m;
}
```
<br>



> **Écrire une fonction DernierElement qui permet de retourner l'adresse du dernier maillon de la liste**
<br>


```java script*
/* 3. Ecrire une fonction DernierElement qui permet de retourner l'adresse du dernier maillon de la liste. */
Maillon* DernierElement (Maillon *L) {

    Maillon *m;

    if( L == NULL )
        return NULL;

    else {
        m = L;

        while ( m->suivant != L )
            m = m->suivant;
        return m;
    }
}

```
<br>



> **Écrire une fonction InsererFin qui permet d'insérer un élément V à la fin de la liste**
<br>


```java script*

/* 4. Ecrire une fonction InsererFin qui permet d'insÃ©rer un Ã©lÃ©ment V Ã  la fin de la liste. */
void InsererFin (Maillon * L, int V ) {

    Maillon *m, *ptr ;
    m = CreerMaillon (V) ;

    if ( m != NULL ) {
        if ( L == NULL ) {
            L = m;
            m->suivant = L;
        }

        else {
            ptr = DernierElement (L);
            ptr->suivant = m;
            m->suivant = L;
        }
    }
}




int main() {

    Maillon * Liste;
    printf("Hello, World!\n");
    return 0;
}
```

---


<br>

Exercice 3
On souhaite gérer les tâches d'un projet à l'aide d'une liste chainée simple. Une tâche est caractérisée par les
informations suivantes :
• Nom : Le nom de la tache (chaine de caractères)
• Durée : La durée d'une tache (nombre de jours : type entier)
• Priorité : La priorité d'une tache (entier) (la valeur la plus grande représente la priorité la plus élevée).
On suppose que la liste chainée est ordonnée selon la durée.

<br>
<br>

> **Définir les structures : Tache, Maillon et Liste**

```java script

/* 1. DÃ©finir les structures Maillon et Liste. */

typedef struct {
    char nom[20];
    int duree;
    int priorite;
} Tache ;

typedef struct maillon {
    Tache tach;
    struct maillon * suivant;
} Maillon;

Maillon* CreerMaillon (Tache T) {
    Maillon *m;
    m = (Maillon*)malloc(sizeof(Maillon));

    if ( m != NULL ) {
        m->tach = T;
        m->suivant = NULL;
    }
    return m;
}
```
<br>



> **Écrire une fonction CreerMaillon qui permet de créer un Maillon à partir d'une tâche T, la fonction doit
retourner l'adresse du maillon cree**
<br>


```java script*
/* 2. Ecrire une fonction CreerMaillon qui permet de crÃ©er un Maillon Ã  partir d'une tÃ¢che T, la fonction doit retourner l'adresse du maillon crÃ©Ã©. */

void InsererDebut (Maillon * L,Tache T) {
    Maillon *m ;
    m = CreerMaillon(T);

    if ( m != NULL ) {
        m->suivant = L;
        L = m;
    }
}
```
<br>



> **Écrire une fonction InsererDebut qui permet d'ajouter une tâche T au début de la liste**
<br>


```java script*
/* 3. Ecrire une fonction InsererDebut qui permet d'ajouter une tÃ¢che T au dÃ©but de la liste. */

void InsererOrdonnee (Maillon * L, Tache T ) {
    Maillon *m, *pred, *par ;

    if( L == NULL || L->tach.duree  >  T.duree )
        InsererDebut( L, T);

    else {
        m = creerMaillon (T);
        if( m != NULL) {
            par = L->suivant;
            pred = L;
            while ( par != NULL  && par-> tach.duree <  T.duree) {
                pred = par ;
                par = par->suivant;
            }
            m->suivant = par ;
            pred->suivant = m;
        }
    }
}
```
<br>



> **Écrire une fonction InsererOrdonnee qui permet d'ajouter une tâche T à la liste. La liste doit être ordonnée
après l'insertion de T**
<br>


```java script*/* 4. Ecrire une fonction InsererOrdonnee qui permet d'ajouter une tÃ¢che T Ã  la liste. La liste doit Ãªtre ordonnÃ©e aprÃ¨s l'insertion de T. */

void AfficherTachePrioritaire (Maillon *L) {
    Tache tmax;
    Maillon * ptr;

    if ( L == NULL)
        printf("Erreur : la liste est vide") ;
    else {
        tmax = L->tach ;
        ptr = L;
        while ( ptr != NULL) {
            if( ptr->tach.priorite > tmax.priorite )
                tmax = ptr->tach;
            ptr = ptr->suivant ;
        }
        printf("La tÃ¢che la plus prioritaire est : \n la tÃ¢che intitulÃ©e %s n de durÃ©e %d \n et de prioritÃ© %d\n", tmax.nom, tmax.duree, tmax.priorite );
    }
}



int main() {

    Maillon * Liste;
    printf("Hello, World!\n");
    return 0;
}
```

---


<br>


## **Réalisé par :Meryem JOUIHRI (RC)**
## **Encadré par : Mr.AMAMOU Ahmed**

<br>

---

# ** Merci**

