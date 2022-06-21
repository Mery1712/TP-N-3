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
