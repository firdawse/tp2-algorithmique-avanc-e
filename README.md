
# Algorithmique et programmation avancée 
## Série de TP 2 : Pr.AMAMOU Ahmed
### Objectif : Manipulation des structures 

Un semestre est composé de 6 modules, chaque module est enseigné par un professeur et suivis par des étudiants. Chaque module à 3 notes: TP + Contrôle + Examen. La direction à décider de stocker les notes par un tableau de structures et de les gérer par un programme C. on suppose qu'un étudiant et enseignant sont caractérisés par un Code, un Nom, filière. Un module est caractérisé par un code, un nom, un enseignant, les étudiants, les notes.
## 1. Définir les structures étudiant, enseignant, notes et modules.
```c
typedef struct {
    float tp;
    float controle;
    float exam;
}NOTE;

typedef struct {
    int code;
    char nom[40];
    char filiere[40];
}ETUDIANT;

typedef struct {
    int code;
    char nom[40];
    char filiere[40];
}ENSEIGNANT;

typedef struct {
    int code;
    char nom[40];
    ETUDIANT etudiants;
    ENSEIGNANT enseignant ;
    NOTE notes;
}MODULE;
```

 ## 2. Ecrire une fonction qui saisit un étudiant. 
 ```c
 //saisir un étudiant 
void saisirEtudiant(ETUDIANT *X){
	
    printf("entrer le code : \n");
    scanf("%d",&X->code);
     printf("entrer le nom : \n");
    scanf("%s",&X->nom);
     printf("entrer la filiere : \n");
    scanf("%s",&X->filiere);
}
```
 ## 3. Ecrire une fonction qui affiche un étudiant.
 ```c
 //afficher un etudiant 
void AfficherEtudiant(ETUDIANT X){
	printf("code : %d \n nom: %s \n filiere : %s \n",X.code,X.nom,X.filiere);	
}
```
 ##  4. Ecrire une fonction qui saisit un enseignant. 
 ```c
 //saisir un enseignnat 
void saisirEnseignant(ENSEIGNANT *X){
   printf("entrer le code : \n");
    scanf("%d",&X->code);
     printf("entrer le nom : \n");
    scanf("%s",&X->nom);
     printf("entrer la filiere : \n");
    scanf("%s",&X->filiere);
}
 ```
 ## 5. Ecrire une fonction qui affiche un enseignant. 
 ```c
 //afficher un enseignant
void AfficherEnseignant(ENSEIGNANT X){
		printf("code : %d \n nom: %s \n filiere : %s",X.code,X.nom,X.filiere);	
}

 ```
 ## 6. Ecrire une fonction qui saisit les notes. 
  ```c
 void saisirNote(NOTE *X){
	printf("entrer la note de tp : \n");
    scanf("%f",&X->tp);
     printf("entrer la note du controle : \n");
    scanf("%f",&X->controle);
     printf("entrer la note d'exam : \n");
    scanf("%f",&X->exam);	
}

 ```
 ## 7. Ecrire une fonction qui affiche les notes. 
  ```c
 //Afficher les notes
void afficherNote(NOTE X){
	printf("tp : %d \n controle: %f \n examen : %f \n",X.tp,X.controle,X.exam);		
}

 ```
 ## 8. Ecrire une fonction qui saisit un module. 
  ```c
 // saisir un module 
void saisirModule(MODULE * M){
	
printf("entrer le code \n");
scanf("%d",&M->code);
printf("entrer le nom \n");
scanf("%s",&M->nom);
printf("entrer l'enseignant \n");
scanf("%s",&M->enseignant);	
saisirEtudiant(&M->etudiants);
saisirNote(&M->notes);
}

 ```
 ## 9. Ecrire une fonction qui affiche un module. 
  ```c
 //afficher un module

void afficherModule(MODULE M){
	
	printf("le code du module est : %d \n la nom du module est : %s \n l'enseignant du module est : %s \n",M.code,M.nom,M.enseignant);
    AfficherEtudiant(M.etudiants);
	afficherNote(M.notes);
	
}
 ```
 ##  10. Ecrire une fonction qui saisit un tableau de modules.
  ```c
//saisir un tableau de module
void tableauModule(MODULE *c, int taille ){
    int i;
    for(i=0;i<taille;i++){
        saisirModule(&c[i]);
    }
}
 ```
 ## 11. Ecrire une fonction qui affiche un tableau de modules. 
  ```c
 //afficher un tableau de module 
void afficherTableauModule(MODULE *c, int taille ){
    int i;
    for(i=0;i<taille;i++){
        afficherModule(c[i]);
    }
}
 ```
 ## 12. Ecrire le programme principal qui réalise le scénario suivant : 
 - Déclaration d'un tableau dynamique de modules. 
 - Saisie d'un tableau de modules. 
 -  Affichage d'un tableau de modules. 
  ```c
 int main(int argc, char *argv[]) {
	
	int taille =6;
	MODULE * modules =malloc(taille*sizeof(MODULE));
	tableauModule(&modules, taille );
	afficherTableauModule(&modules, taille );
	
	return 0;	
}
 ```
  ## 13. Ecrire une fonction qui calcule le nombre des étudiants qui suivent un module donné. 
   ```c
 //nbr d'étudiants suivant un module donné

int nbrEtudiant(MODULE *M,int taille,int codeModule){
int i;
int n=0;
for(i=0;i<taille;i++){
	if(codeModule==M[i]->code){
		n++;
	}
}
return n;
}
 ```
  ## 14. Ecrire une fonction qui affiche les modules suivis par un étudiant donné. 
   ```c
 //nbr de modules suivi par un étudiant donné

int nbrModule(MODULE *M,int taille,char Etudiant[]){
int i;
int n=0;
for(i=0;i<taille;i++){
	if(Etudiant==M[i]->etudiants.nom){
		n++;
	}
}
return n;
}
 ```
  ## 15. Ecrire une fonction qui calcule la moyenne du module d'un étudiant donnée. 
   ```c
 //moyenne d'un module
float moyenneNote(NOTE n){
	float moyenne = n.tp*1/4 +n.controle*1/4 +n.exam*1/2;
	printf("la moyenne du module est %f",moyenne);
}

 //moyenne du module d'un etudiant 
float moyenneEtudiant(MODULE *M,int taille,char etudiant[],int codeModule){
int i;
for(i=0;i<taille;i++){
	if(etudiant==M[i]->etudiants.nom&& codeModule=M[i]->code){
		return moyenneNote(M[i]->notes)
	}
}
return 0;
}
 ```
  ## 16. Ecrire une fonction qui calcule la moyenne du semestre d'un étudiant donné ( 1 semestre = 6 modules)
   ```c
 //moyenne du semestre d'un etudiant donné
float moyenneSemestre(MODULE *M,int taille,char etudiant[]){
int i;
float somme=0;
for(i=0;i<taille;i++){
	if(etudiant==M[i]->etudiants.nom){
		somme+= moyenneNote(M[i]->notes)
	}
}

return somme/6;
}

 ```
