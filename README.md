# **Algorithmique et programmation avancée**

##  Objectif : Listes chainées

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





