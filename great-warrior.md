#include <stdio.h>
#include <stdlib.h>
#include<windows.h>
#include<string.h>

int N=0,i,CR[20],NR=0,NT=0, *P1, *P2;

float Taux[20];
int *p1;
 //variable globale

// Pour la gestion de l'affichage
COORD coord={0,0};
void gotoxy (int x,int y){
    coord.X=x;
    coord.Y=y;

SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE),coord);}



//structure pour gerer les informations des employers:
struct EMPLOYER{
    int matricule;
    char nom[20],prenom[20];
    int salaire_brut;
    float taux;
    int code_region;

};
typedef struct EMPLOYER employer;

//tableau des employers
employer a[50];

//creation d'un fichier :
            //FILE* fichier= NULL;
//
int main()
{
    int c;
    system("color 0A");

//    fichier= fopen("miniprojet.doc","a");



  // menu principal:
   dt: {menu(a);
    gotoxy(77,9);scanf("%d",&c);}
    switch(c){
    case 1:
           system("cls");
            Gestion_employes();

         break;
    case 2:
          system("cls");{
          Gestioncode_region();}
          break;
          system("cls");
    case 3:printf("ce fut un plaisir , à bientot !");
    goto end;

         break;

    default :printf("invalid");}
end:
return 0;}

//synthaxe du menu principale:
void menu(){


    gotoxy(35,2);printf("ÚÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄ¿");
    gotoxy(35,3);printf("³                                            ³");
    gotoxy(35,4);printf("³               MENU PRINCIPAL               ³");
    gotoxy(35,5);printf("ÃÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄ´");
    gotoxy(35,6);printf("³           1.Gestion des Employes           ³");
    gotoxy(35,7);printf("³           2.Gestion du code rWgion         ³");
    gotoxy(35,8);printf("³           3.Quitter                        ³");
    gotoxy(35,9);printf("³                                   Choix:   ³");
   gotoxy(35,10);printf("ÀÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÙ");







     }

void Gestion_employes(){
    int choix;

system("color 6");
     gotoxy(40,1);printf("ÚÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄ¿");
     gotoxy(40,2);printf("³        Menu de gestion des employes        ³");
     gotoxy(40,3);printf("ÃÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄ´");
     gotoxy(40,4);printf("³           1.Ajout d'un employes            ³");
     gotoxy(40,5);printf("³                                            ³");
     gotoxy(40,6);printf("³           2-modification                   ³");
     gotoxy(40,7);printf("³                                            ³");
     gotoxy(40,8);printf("³           3. Suppression                   ³");
     gotoxy(40,9);printf("³                                            ³");
    gotoxy(40,10);printf("³           4.Recherche                      ³");
    gotoxy(40,11);printf("³                                            ³");
    gotoxy(40,12);printf("³           5- Liste des employes            ³");
    gotoxy(40,13);printf("³                                            ³");
    gotoxy(40,14);printf("³           6. Etat des salaires             ³");
    gotoxy(40,15);printf("³                                            ³");
    gotoxy(40,16);printf("³           7.Menu principal                 ³");
    gotoxy(40,17);printf("³                                            ³");
    gotoxy(40,18);printf("³                                            ³");
    gotoxy(40,19);printf("³                                            ³");
    gotoxy(40,20);printf("³                                  Choix:    ³");
    gotoxy(40,21);printf("³                                            ³");
    gotoxy(40,22);printf("ÀÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÙ");
    gotoxy(82,20);scanf("%d",&choix);

switch(choix){
    case 1: //ajout d'un employer
          system("cls");

       Ajouter_employer();
        getch();
        system("cls");

       break;

      case 2:
        system("cls");
               employe_modification(&N);
     break;

      case 3://suppression
        system("cls");
          employe_suppression();
       break;

     case 4 ://recherche d'employes
        system("cls");
        employe_recherche();
        break;


      case 5 :
         for(i=0;i<=N-1;i++){
        printf("\n%d : %s  %s   salaire brut: %d   region %d",a[i].matricule,a[i].nom,a[i].prenom,a[i].salaire_brut,a[i].code_region);
        Gestion_employes();
    }
        break;

        break;
       case 6 :
        system("cls");
        Etat_salaires();
        break;

        case 7 :
       system("cls");
       main();
        break;


    default :printf ("invalid");



}

}

void Ajouter_employer(){
int i=0,n=0,code_temp,choix;
float taux_temp;
if(NR==0){
          do{ printf("\n\t => il faut d'abord mettre en place des codes regions ou on placera les employers"); //rediriger l'utillisateur en cas de manque de regions
              printf("\n pour rajouter une region aller au menu code region\n");
         printf("\n1)Menu gestion code region\n");
         printf("\n2)Revenir au menu des employers\n \n\t choix: ");
         scanf("\n %d",&i);}while(i!=1 && i!=2);
                        if(i==1){Gestioncode_region(); }
                        else Gestion_employes();}

else{
printf("voici les regions disponibles:\n");

 for(P1=CR,i=0;P1<CR+NR;P1++,i++){
printf("\nregion %d : %d  avec taux salariale = %f \n",i+1,*P1,Taux[i]);

}
printf("\n\t choix:");          // choix de la region ou placer le ou les employers
scanf("%d",&choix);

for(P1=CR,i=0;P1<CR+NR,i<=NT;P1++,i++){
if(choix==i+1){                               //on place le code region dans une variable temporaire
    code_temp=*P1;
    taux_temp=Taux[i];
} }

printf("\ncombien d'employer de cette region voulez vous rajouter ?");
scanf("%d",&n);
system("cls");
gotoxy(10,51);printf(" region %d || taux salarial %f %:\n \n",code_temp,taux_temp);
for(i=N;i<=N+n-1;i++){
 a[i].code_region=code_temp;
printf("\n employer numero %d: ",i+1);
printf("\n\t  matricule:");
scanf("%d",&a[i].matricule);
printf("Nom:");
scanf("%s",&a[i].nom);
printf("Prenom: ");
scanf("%s",&a[i].prenom);
getchar();
printf("Salaire brut: ");
scanf("%d",&a[i].salaire_brut);


}
N=N+n;

system("cls");

Gestion_employes();}
}


void employe_modification(){
    int choix,n,i=0,code_temp;
    float taux_temp;
    menu_modif:
    gotoxy(10,1);printf("ÚÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄ¿");
    gotoxy(10,2);printf("³           1.Nom                            ³");
    gotoxy(10,3);printf("³           2.Prenom                         ³");
    gotoxy(10,4);printf("³           3.Salaire brut                   ³");
    gotoxy(10,5);printf("³           4.code Region                    ³");
    gotoxy(10,6);printf("³           5.Retour                         ³");
    gotoxy(10,7);printf("³                                Choix:      ³");
    gotoxy(10,8);printf("ÀÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÙ");
    gotoxy(50,7);scanf("%d",&choix);

     system("cls");


    switch(choix){
    case 1:

          for(i=0;i<=N-1;i++){
          printf("\n%d_ %s : %d",i+1,a[i].nom,a[i].matricule);}


      do{ printf("\n veuillez selectioner la personne dont vous souhaitez changer le nom : ");
       scanf("%d",&n);
       printf("nouveau nom: ");
       scanf("%s",&a[n-1].nom);}while(n<0||n>N);



        printf("appuyer sur entrer pour revenir au menu secondaire");
        getch();
        system("cls");
        goto menu_modif;


         break;

    case 2:
        for(i=0;i<=N-1;i++){
          printf("\n%d_ %s ",i+1,a[i].prenom);}


     do{  printf("\n veuillez sasir le numero du prenom que vous souhaitez changer : ");
       scanf("%d",&n);
       printf("nouveau nom: ");
       scanf("%s",a[n-1].prenom);}while(n<0||n>N);



        printf("appuyer sur entrer pour revenir au menu secondaire");
        getch();
        system("cls");
        goto menu_modif;



        break;

    case 3:
        for(i=0;i<=N-1;i++){
          printf("\n%d_%s: %d dhs\n",i+1,a[i].nom,a[i].salaire_brut);}

       do{
       printf("\n\n veuillez sasir le numero de la personne dont vous souhaitez modifier le salaire : ");
       scanf("%d",&n);
       printf("nouveau salaire: ");
       scanf("%d",&a[n-1].salaire_brut);}while(n<0||n>N);



        printf("appuyer sur entrer pour revenir au menu secondaire");
        getch();
        system("cls");
        goto menu_modif;


        system("cls");


       break;

    case 4 ://code région modiff
        for(i=0;i<=N-1;i++){
          printf("\n%d_ %s : %d",i+1,a[i].nom,a[i].code_region);}

       do{
       printf("\n veuillez selectioner la personne dont vous souhaitez changer le code region : ");
       scanf("%d",&n);
      do{ printf("selectionner un code preexistant ou creer en un nouveau: ");
       printf("1) choisir un code prexistant");
       printf("/n2) creer un nouveau");
       scanf("%d",&i);}while(n!=1 && i!=2);
       if(i==1){
       for(P1=CR,i=0;P1<CR+NR;P1++,i++){
printf("\nregion %d : %d  avec taux salariale = %f \n",i+1,*P1,Taux[i]);

          for(P1=CR,i=0;P1<CR+NR,i<=NT;P1++,i++){
if(choix==i+1){                               //on place le code region et son taux dans une variable temporaire
    code_temp=*P1;
    taux_temp=Taux[i];
} }
      a[n-1].code_region=code_temp;
      a[n-1].taux=taux_temp;
 }

}
       scanf("%d",&a[n-1].code_region);}while(n<0||n>N);



        printf("appuyer sur entrer pour revenir au menu secondaire");
        getch();
        system("cls");
        goto menu_modif;



  case 5:
      system("cls");
   Gestion_employes();
   break;

  default :{system("cls");
    printf ("invalide, reessayer:");
    employe_modification();}




goto menu_modif;}

}

void employe_suppression(){

    int choix,n,j,min,max;
    menu_supr:
    gotoxy(10,1);printf("ÚÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄ¿");
    gotoxy(10,2);printf("³        1.Un par Un                         ³");
    gotoxy(10,3);printf("³        2.Par region                        ³");
    gotoxy(10,4);printf("³        3.Tout                              ³");
    gotoxy(10,5);printf("³        4.Retour                            ³");
    gotoxy(10,6);printf("³                                Choix:      ³");
    gotoxy(10,7);printf("ÀÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÙ");
    gotoxy(50,6);scanf("%d",&choix);


     switch(choix){
    case 1:

        for(i=0;i<=N-1;i++){
          printf("\n%d_%s_",i+1,a[i].nom,a[i]);}

            do{ printf("\n veuillez selectioner l'employer a supprimer : ");
       scanf("%d",&n);}while(n<0||n>N);
       for(i=0;i<=N-1;i++){
          if(i==n-1){
                      for(j=i;j<=N-1;j++){
                                    a[j]=a[j+1];}
                                    N--;

          }

          }

printf("appuyer sur entrer pour revenir au menu secondaire");
        getch();
        system("cls");
        Gestion_employes();



         break;

    case 2://par région
            system("cls");
            printf("veuillez saisir le coderegion des employers a supprimer:");
            scanf("%d",&n);

                               for(i=0;i<=N-1;i++){

                         if(a[i].code_region==n){
                                    for(j=i;j<=N-1;j++){
                                    a[j]=a[j+1];}
                                    N--;

          }

          }
          system("cls");
         employe_suppression();


        break;

    case 3://Tout supprimer:
        system("cls");
        N=0;
        printf("les employers ont ete suprimer avec succes");
        getch();
        system("cls");
        Gestion_employes();
       break;


  case 4 ://retour
      Gestion_employes();

        break;


    default :printf ("invalid");




goto menu_supr;}

}

void employe_recherche(){
int choix,j,employesTrouves = 0 , min ,max;

int i,matricule;
int  nombreEmployes= 0;
char Nom[10];
employer T;
char rech[20];
 menu_recherche:
    gotoxy(10,1);printf("ÚÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄ¿");
    gotoxy(10,2);printf("³           1.Par matricule                  ³");
    gotoxy(10,3);printf("³           2.Par nom                        ³");
    gotoxy(10,4);printf("³           3.Par intervalle de salaire brut ³");
    gotoxy(10,5);printf("³           4.Par code                       ³");
    gotoxy(10,6);printf("³           5.Retour                         ³");
    gotoxy(10,7);printf("³                                Choix:      ³");
    gotoxy(10,8);printf("ÀÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÙ");
    gotoxy(50,7);scanf("%d",&choix);

    switch(choix){
    case 1:
                 printf("Matricule de l'employé à rechercher : ");
                scanf("%d", &matricule);

     for (i = 0; i < N; i++) {
        if (a[i].matricule == matricule) {
            afficherEmploye(a[i]);
            employesTrouves= 1;

        }
    }
   if (!employesTrouves) {
        printf("Aucun employé trouvé avec le nom %s.\n", matricule);
    }
            break;


    case 2:
           employesTrouves = 0;
                    system("cls");
                   printf("\nNom de l'employé à rechercher : ");
               scanf("%s",&Nom);
               getchar();

    for (i = 0; i <= N; i++) {
        if (strcmp(a[i].nom, Nom) == 0) {
            afficherEmploye(a[i]);
            employesTrouves = 1;
        }
    }

    if (!employesTrouves) {
        printf("Aucun employé trouvé avec le nom %s.\n", Nom);
    }

          break;
          system("cls");
    case 3:printf("donner l'intervalle de salaire :");
          scanf(" %d",&max);
          scanf("%d",&min);

           for (i = 0; i <= N; i++) {
        if (a[i].salaire_brut>=min && a[i].salaire_brut<=max) {
            afficherEmploye(a[i]);
            employesTrouves = 1;
        }

        break;



        case 4:printf("donner le code de region :");
          scanf(" %d",&max);

           for (i = 0; i <= N; i++) {
        if (a[i].code_region==max) {
            afficherEmploye(a[i]);
            employesTrouves = 1;
        }
    }
  ;

         break;

    default :printf("invalid");}



    }}


void Etat_salaires(){

int i,c;
float salaire_net,S=0 ;
printf("voici les regions disponibles , choisissez une pour afficher l'etat de ses salaires:\n");
for(P1=CR,i=0;P1<CR+NR;P1++,i++){
        printf("\: %d  avec taux salariale = %f \n",i+1,*P1,Taux[i]);}


system ("cls");

 gotoxy(10,1);printf("ÚÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄ¿");
 gotoxy(10,2);printf("³                                           ETAT DES SALAIRES                          ³");
 gotoxy(10,3);printf("ÃÄÄÄÄÄÄÄÄÄÄÄÄÂÄÄÄÂÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄ´");
 gotoxy(10,4);printf("³Code Region ³   ³                                                                     ³");
 gotoxy(10,5);printf("ÃÄÄÄÄÄÄÄÄÄÄÄÄÁÄÄÄÅÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÂÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÂÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄ´");
 gotoxy(10,6);printf("³  Matricule     ³  Nom & Prenom         ³  Salaire de base  ³    Salaire net          ³");
 gotoxy(10,7);printf("ÃÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÅÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÅÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÅÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄ´");
 gotoxy(10,8);printf("³-               ³                       ³                   ³                         ³");

for(P1=CR,i=0;P1<CR+N;P1++,i++){

gotoxy(10,9+i);printf("³-               ³                       ³                   ³                         ³");
}
gotoxy(10,i+9);printf("³                ³                       ³                   ³                         ³");
gotoxy(10,i+10);printf("ÃÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÁÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÁÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÅÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄ´");
gotoxy(10,i+11);printf("³                                     Somme des salaires Net:³                         ³");
gotoxy(10,i+12);printf("ÃÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÁÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄ´");
gotoxy(10,i+13);printf("ÀÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÙ");

gotoxy(24,4);scanf("%d",&c);
for(P1=CR,i=0;P1<CR+N;P1++,i++){
gotoxy(14,9+i);printf("%d",a[i].matricule);
gotoxy(28,9+i);printf("%s",a[i].nom);
gotoxy(36,9+i);printf("%s",a[i].prenom);
gotoxy(52,9+i);printf("%d",a[i].salaire_brut);
salaire_net=(float)a[i].salaire_brut+a[i].salaire_brut*(a[0].taux)/100;
S+=salaire_net;
gotoxy(72,9+i);printf("%f",salaire_net);}
gotoxy(72,i+11);printf("%f",S);
getch();
system("cls");
Gestion_employes();

}

void Gestioncode_region(){
system("color 0B");
   system("cls");
    int A,b, n=0, c,cr=0,i=0,j;


    P2=CR;
menusec:

    gotoxy(15,1);printf("ÚÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄ¿");
    gotoxy(15,2);printf("³                                            ³");
    gotoxy(15,3);printf("³          Menu gestion code region          ³");
    gotoxy(15,4);printf("ÃÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄ´");
    gotoxy(15,5);printf("³           1.Ajout d'un code                ³");
    gotoxy(15,6);printf("³           2.Modifier le taux               ³");
    gotoxy(15,7);printf("³           3.Supprimer Code                 ³");
    gotoxy(15,8);printf("³           4.Rechercher Code                ³");
    gotoxy(15,9);printf("³           5.Liste des codes                ³");
   gotoxy(15,10);printf("³           6.Menu principal  *choix:        ³");
   gotoxy(15,11);printf("ÀÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÄÙ");
   gotoxy(52,10);scanf("%d",&A);

    //Deuxieme menu :

 switch(A){
    case 1: //ajout d'un code
          system("cls");
          P2=CR+cr;

         printf("combien de regions voulez vous ajoutez?:");
        scanf("%d",&n);
      for(P2=P1=CR+cr;P1<(CR+cr+n);P1++){
            printf("\n%d-",i+1);
        scanf("%d",P1);
        printf("\n le taux salariale de cette region:");
        scanf("%f",&Taux[i]);
        NR++;
        NT++;
        i++;

      }
      cr=NR;// cr prends
        printf("appuyer sur entrer pour revenir au menu secondaire");
        getch();
        system("cls");
        goto menusec;



         break;

    case 2:
       printf("quelle est l'employer dont vous souhaitez modifier le taux ?");

                 for(i=0;i<=N-1;i++){
          printf("\n%f",a[i].taux);}

 if(N>0){ scanf("%d",&b);
  printf("nouveau taux: ");
  scanf("%d",&c);

      a[i].taux= c;}


          Gestioncode_region();



        break;

    case 3://suppression
        system("cls");
      printf("donner le code region à supprimer");


            scanf("%d",&c);


        for(i=0;i<=NR-1;i++){
                if(c==CR[i]){
                              for(j=i;j<=NR-1;j++){
                                    CR[j]=CR[j+1];
                                    NR--;
                }}}
if(N>0){

            for(i=0;i<=N-1;i++){
            if(a[i].code_region==c){
                    for(j=i;j<=N-1;j++){
                                    a[j]=a[j+1];}
                                    N--;
                                    }}
        }
       system("cls");
       Gestioncode_region();
         break;


    case 4 :

       printf("Matricule de l'employer a rechercher : ");
                scanf("%d", &c);

     for (i = 0; i < N-1; i++) {
        if (a[i].matricule == c) {
            printf("\nle code que vous cherchez est : %d", a[i].code_region);}


        break;
    case 5:
        printf("\nliste des codes:\n");

        for(P1=CR,i=0;P1<=CR+NR;P1++,i++){
printf("\n %d) region %d : avec taux salariale = %f \n",i+1,*P1,Taux[i]);}
                getch();
             Gestioncode_region();


        break;
    case 6:
         system("cls");
        main();
        break;

    default :printf ("invalid");





}}}













void afficherEmploye(const employer employe) {
    printf("Matricule : %d\n", employe.matricule);
    printf("Nom : %s\n", employe.nom);
    printf("Prénom : %s\n", employe.prenom);
    printf("Salaire brut : %.d\n", employe.salaire_brut);
    printf("Code de région : %s\n", employe.code_region);
    printf("\n");}
