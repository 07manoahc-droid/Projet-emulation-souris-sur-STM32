Controleur de souris via carte STM32F407 (accéléromètre) :



Ce projet transforme la carte de développement "STM32F407G-DISC1" en une souris d'ordinateur, contrôlée par l'inclinaison de la carte selon ses axes. 



J'ai développé ce petit projet académique dans le cadre de mon master 2. Il fait suite à un ancien projet dont le but est d'envoyer des raccourcis clavier via cette même carte. Ce projet à été réalisé en C et m'a permis de mieux comprendre l'architecture et lees protocoles de communication de microcontroleurs tout en améliorant mes compétences en programmation. 



* Fonctionnalités clés



Émulation USB HID (Human Interface Device) : La carte est reconnue nativement par n'importe quel système d'exploitation (Windows, macOS, Linux) comme une souris standard, sans installation de pilote côté PC.



Communication SPI (Serial Peripheral Interface) : Interfaçage bas niveau avec accéléromètre embarqué (LIS302DL / LIS3DSH) pour lire les données d'inclinaison brutes.



Traitement du signal brute en temps réel : Implémentation d'une "zone morte" pour annuler le bruit du capteur lorsque la carte est à plat, et conversion des données d'accélération en vecteurs de vitesse de déplacement.



* Stack Technique et Outils



Microcontrôleur : STM32F407G-DISC1 (ARM Cortex-M4)

Langage : C 

Framework : STM32 HAL

IDE et outils : STM32CubeIDE, STM32CubeMX

Protocoles : SPI, USB 2.0 FS



* Architecture du Code



L'essentiel de la logique se trouve dans le fichier 'Core/Src/main.c'.



1\. Initialisation : Configuration de l'horloge système, du bus SPI à 10 MHz et du périphérique USB OTG en mode Device.

2\. Setup du Capteur : Écriture dans le registre de contrôle ('0x20') via SPI pour activer l'accéléromètre à une fréquence de 100Hz.

3\. Boucle principale ('while(1)') :

&#x20;  - Lecture continue des registres X ('0x29') et Y ('0x2B').

&#x20;  - Filtrage et calcul des vecteurs de déplacement.

&#x20;  - Envoi du rapport formaté '\[Boutons, X, Y, Molette]' via la fonction 'USBD\_HID\_SendReport()'.



* Si vous voulez tester ce projet ?



1\. Clonez ce dépôt : 'git clone https://github.com/\[VOTRE\_NOM]/\[NOM\_DU\_DEPOT].git'

2\. Ouvrez le projet avec STM32CubeIDE.

3\. Connectez le port Mini-USB (ST-LINK) pour l'alimentation et le débogage.

4\. Connectez le port Micro-USB (USB USER) à votre ordinateur (c'est par ce port que passent les signaux HID).

5\. Compilez et flashez le programme.

6\. Inclinez la carte et le curseur se déplace selon les différents axes


