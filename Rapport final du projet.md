# Création d'un jeu d'escape game du type storyteller


## PCB : 
Le PCB a été créé sur KiCad à partir d'une carte microcontrôleur STM32 à laquelle on a branché tous les éléments nécessaires, c'est-à-dire : un régulateur, un moteur, un écran, un capteur RFID, des boutons, des LEDs et des connecteurs.
L'écran va permettre d'afficher les consignes sur le jeu. Les leds et les boutons serviront à valider et savoir si la réponse est correcte.


## CODE du moteur :
Le code est écrit pour un servomoteur de type 6800 MGA protronic. Dont, l'angle de rotation maximal est 120° (déterminé experimentalement en l'absence de documentation). Il définit la pulsation du signal PWM en sortie à partir d'un angle de rotation donné en entrée.

void setServo(int angle){   
  int pulsemax = 1900   
  int pulsemin = 1500     
  int anglemax = 120 
  int pulse = pulsemin + (pulsemax-pulsemin)*angle/anglemax    
  TIM2->CCR4 = pulse;   
}   
Ici pour le cas où PWM du moteur est sur channel 4 du timer 2.
## CODE du capteur RFID : 





## Avis de chacun sur le projet 

Mélina : J'ai beaucoup appris durant ce projet notamment sur la création du PCB. 
