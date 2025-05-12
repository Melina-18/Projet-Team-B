# Création d'un jeu d'escape game du type storyteller

sur markdown 

## PCB : 
Le PCB a été créé sur KiCad à partir d'une carte microcontrôleur STM32 à laquelle on a branché tous les éléments nécessaires, c'est-à-dire : un régulateur, un moteur, un écran, un capteur RFID, des boutons, des LEDs et des connecteurs.
L'écran va permettre d'afficher les consignes sur le jeu. Les leds et les boutons serviront à valider et savoir si la réponse est correcte.


## CODE du moteur :

void setServo(int angle){
  int pulsemax = 1900
  int pulsemin = 1500
  int pulse = pulsemin + (pulsemax-pulsemin)*angle/180
  TIM2->CCR4 = pulse;
}

## CODE du capteur RFID : 





## Avis de chacun sur le projet 

Mélina : J'ai beaucoup appris durant ce projet notamment sur la création du PCB. 
