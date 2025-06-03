# Création d'un jeu d'escape game du type storyteller



## PCB : 
Le PCB a été créé sur KiCad à partir d'une carte microcontrôleur STM32 à laquelle on a branché tous les éléments nécessaires, c'est-à-dire : un régulateur de tension, un servomoteur, un écran, un capteur RFID, des boutons, des LEDs et des connecteurs.
L'écran va permettre d'afficher les consignes sur le jeu. Les leds et les boutons serviront à valider et savoir si la réponse est correcte.


## Partie informatique :   

### CODE du moteur :
Le code est écrit pour un servomoteur de type 6800 MGA protronic dont l'angle de rotation maximal est 120° (déterminé experimentalement en l'absence de documentation). Le code définit la pulsation du signal PWM en sortie à partir d'un angle de rotation donné en entrée.

void setServo(int angle){   
  int pulsemax = 1900   
  int pulsemin = 1500     
  int anglemax = 120 
  int pulse = pulsemin + (pulsemax-pulsemin)*angle/anglemax    
  TIM2->CCR4 = pulse;   
}   
Ici pour le cas où PWM du moteur est sur channel 4 du timer 2.

### CODE du capteur RFID : 
//Card_READ : Lis les informations de la carte ou d'un tag et modifie les listes contenant les personnages  
void Card_READ(void)  
{   
	//Les trois porchaines lignes suffisent pour   
	status1=MFRC522_Request(PICC_REQIDL,str);   
	status2=MFRC522_Anticoll(str);    
	memcpy(sNum,str,5);    
	if (status1==0 && status2==0 && Read_MFRC522(0x37)==146  && (str[0]!=old_str[0] ||  str[1]!=old_str[1] || str[2]!=old_str[2] || str[3]!=old_str[3] || str[4]!=old_str[4]))   //Vérifie que le capteur fonctionne correctement et que la carte est différente de la précédente pour éviter des répétitions    
	{	old_str[0]=str[0];    
		old_str[1]=str[1];   
		old_str[2]=str[2];   
		old_str[3]=str[3];   
		old_str[4]=str[4];   
		Card_Passed=1;   // on note qu'une carte a été captée et que l'écran doit être modifié   
if (str[0]==218 && str[1]==232 && str[2]==60 && str[3]==77 && str[4]==67){   // exemple pour un personnage    
add_character("Clemence ");  // sert à garder la liste des personnages dans chaque pièce   
			perso="Clemence ";  // garde le personnage le plus récent    
			nb_personages[i]+=1;  // sert à modifier la position où le nom des personnages est affiché}    

### CODE de l’écran LED:   
//screen_update : Met à jour l'écran   
void screen_update()   
{	if (button_pressed==1){   
		char buffer[16]={0};   
		ssd1315_Clear(SSD1315_COLOR_BLACK);   
		snprintf(buffer,16,"%s ",(pieces[i]));   
		ssd1315_Draw_String(0,0,buffer,&Font_11x18);   
		int len=strlen(personages[i]);   
		for (int n=0;n<len;n++){   // l'affichage n'est pas idéal(échec d'écriture similaire au cas Card_passed)    
			snprintf(buffer,16,"%c ",(personages[i][n]));     
			ssd1315_Draw_String(7*n,pos,buffer,&Font_7x10);    
			ssd1315_Refresh();    
			printf("%c \n\r",personages[i][n]);   
			}    
		pos=20;    
		ssd1315_Refresh();    
	}    
	if (Card_Passed==1){     
		Card_Passed=0;    
		char buffer[16]={0};    
		snprintf(buffer,16,"%s ",(pieces[i]));  // la pièce est affichée en haut et en gros    
		ssd1315_Draw_String(0,0,buffer,&Font_11x18);    
		snprintf(buffer,16,"%s ",perso);    
		ssd1315_Draw_String(0,10+(10*nb_personages[i]),buffer,&Font_7x10);  // les personnages sont ajoutés de plus en plus bas selon le nombre dans la pièce     
		ssd1315_Refresh();}    


bémol du code:  utilisation d’un loop au lieu de réaliser des tasks (simplement par manque de temps, nous avons privilégié la création d’un code fonctionnel plus simple à réaliser pour pouvoir présenter un projet fini informatiquement, c'est un défaut qui serait facilement résolu avec plus de temps)   
  
le reste du code ainsi que l’ioc est accessible dans Projet1A5.0.zip  






## Avis de chacun sur le projet 

Mélina : J'ai beaucoup appris durant ce projet notamment sur la création du PCB.     
Tom : J’ai découvert les complexités liées à la réalisation d’un projet ainsi que l’importance d’une bonne organisation dans un groupe.
Bradley : Que ce soit en code, modélisation 3D et management j'ai beaucoup appris, ce qui me permettra de mieux entreprendre mes futurs projets.
Lucie : 

