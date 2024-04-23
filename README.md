/*
NB: les lignes de code ci-dessous contient généralement beaucoup de répétition, pour optimiser on a penser à utiliser des fonctions pour optimiser mais malheureusement le code ne marchais pas ce qui fait on a maintenue comme ça
pour les commentaires : le case 12 est un exemple parfait qui résume le fonctionnement de tous les autres case, merci pour la compréhension
ET  AUSSI : la signification des chiffres dans le case 
12 = 1
24 = 2
94 = 3
8 = 4
28 = 5
90 = 6
66 = 7
82 = 8
74 = 9
22 = 0
*/

#include <IRremote.h>
#include <Servo.h>
#include <Wire.h>
#include <Adafruit_PWMServoDriver.h>

Adafruit_PWMServoDriver myServo = Adafruit_PWMServoDriver();

#define SERVOMIN 150
#define SERVOMAX 380
#define SERVOMIN_1 150
#define SERVOMAX_1 380
int PIN_IR = 8;
int iValue;
uint8_t servonum = 0;
uint8_t numberOfServos = 6;

void setup()
{
 myServo.begin();
 myServo.setPWMFreq(60);
 delay(10);
 Serial.begin(9600);
 IrReceiver.begin(PIN_IR); //Déclaration/Initialisation de mon objet IR
 pinMode(7,OUTPUT);
}

void loop() {
 /*cette condition permet verifie la valeur capter par le capteur */ 
    if ( IrReceiver.decode() ) {
       iValue = IrReceiver.decodedIRData.command; // Valeur en décimal
       Serial.println(iValue);
       IrReceiver.resume();// permet d'attendre une nouvelle valeur de la commande 
       }

int valeur = iValue;
// le switch permet d'exécuter un exemple de code : dans ce cas c'est d'afficher un chiffre   
 switch (iValue) {
 case 12:
   {
delay(3000);
// le code ci-dessous : répresente la partie qui réinitialise les segments mobiles
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(0, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(1, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(2, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(3, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(4, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(5, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(6, 0, pulselen);
}
// fin du code qui réinitialise les segments

// le code ci-dessous : fait varier les angles des servomoteurs pour :
// Affiche le chiffre 1
delay(1000);
 // Segment 2
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(1, 0, pulselen);
}
 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(4, 0, pulselen);
}

// le code ci-dessous : est une boucle do-while qui permet de préserver une valeur afficher par les segments mobiles en attendant une nouvelle valeur de la télécommande
do {
   if ( IrReceiver.decode() ) {
   iValue = IrReceiver.decodedIRData.command; // Valeur en décimal
   Serial.println(iValue);
   IrReceiver.resume();// permet d'attendre une nouvelle valeur de la commande 
 }
 delay(100);
 }while(valeur == iValue);
 delay(1000);
}
   break;
   case 24:
   {
delay(1000);
// remettre à zero
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(0, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(1, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(2, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(3, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(4, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(5, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(6, 0, pulselen);
}
// Affiche le chiffre 2
 // Segment 2
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(0, 0, pulselen);
}
 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(1, 0, pulselen);
}
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(3, 0, pulselen);
}
 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(5, 0, pulselen);
}
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(6, 0, pulselen);
}
 delay(100);
do {
   if ( IrReceiver.decode() ) {
   iValue = IrReceiver.decodedIRData.command; // Valeur en décimal
   Serial.println(iValue);
   IrReceiver.resume(); //Important
   delay(100);
 }
 }while(valeur == iValue);
 delay(1000);
}
   break;
      case 94:
   {
delay(3000);
// remettre à zero
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(0, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(1, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(2, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(3, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(4, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(5, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(6, 0, pulselen);
}
// Affiche le chiffre 3
 // Segment 2
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(0, 0, pulselen);
}
 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(1, 0, pulselen);
}
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(3, 0, pulselen);
}
 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(4, 0, pulselen);
}
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(6, 0, pulselen);
}
 delay(100);
do {
   if ( IrReceiver.decode() ) {
   iValue = IrReceiver.decodedIRData.command; // Valeur en décimal
   Serial.println(iValue);
   IrReceiver.resume(); //Important
   delay(100);
 }
 }while(valeur == iValue);
 delay(1000);
}
   break;
         case 8:
   {
delay(1000);
// remettre à zero
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(0, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(1, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(2, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(3, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(4, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(5, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(6, 0, pulselen);
}
// Affiche le chiffre 4
  // Segment 2
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(1, 0, pulselen);
}
 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(2, 0, pulselen);
}
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(3, 0, pulselen);
}
 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(4, 0, pulselen);
}
 delay(100);
do {
   if ( IrReceiver.decode() ) {
   iValue = IrReceiver.decodedIRData.command; // Valeur en décimal
   Serial.println(iValue);
   IrReceiver.resume(); //Important
   delay(100);
 }
 }while(valeur == iValue);
 delay(1000);
}
   break;
            case 28:
   {
delay(1000);
// remettre à zero
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(0, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(1, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(2, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(3, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(4, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(5, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(6, 0, pulselen);
}
// Affiche le chiffre 5
// Segment 2
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(0, 0, pulselen);
}
 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(2, 0, pulselen);
}
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(3, 0, pulselen);
}
 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(4, 0, pulselen);
}
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(6, 0, pulselen);
}
 delay(100);
do {
   if ( IrReceiver.decode() ) {
   iValue = IrReceiver.decodedIRData.command; // Valeur en décimal
   Serial.println(iValue);
   IrReceiver.resume(); //Important
   delay(100);
 }
 }while(valeur == iValue);
 delay(1000);
}
   break;
           case 90:
   {
delay(1000);
// remettre à zero
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(0, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(1, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(2, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(3, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(4, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(5, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(6, 0, pulselen);
}
// Affiche le chiffre 6
 // Segment 2
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(0, 0, pulselen);
}
 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(2, 0, pulselen);
}
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(3, 0, pulselen);
}
 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(4, 0, pulselen);
}
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(5, 0, pulselen);
}
 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(6, 0, pulselen);
}
 delay(100);
do {
   if ( IrReceiver.decode() ) {
   iValue = IrReceiver.decodedIRData.command; // Valeur en décimal
   Serial.println(iValue);
   IrReceiver.resume(); //Important
   delay(100);
 }
 }while(valeur == iValue);
 delay(1000);
}
   break;
     case 66:
   {
delay(1000);
// remettre à zero
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(0, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(1, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(2, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(3, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(4, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(5, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(6, 0, pulselen);
}
// Affiche le chiffre 7
 // Segment 2
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(0, 0, pulselen);
}
// Segment 2
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(0, 0, pulselen);
}
 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(1, 0, pulselen);
}
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(4, 0, pulselen);
}
 delay(100);
do {
   if ( IrReceiver.decode() ) {
   iValue = IrReceiver.decodedIRData.command; // Valeur en décimal
   Serial.println(iValue);
   IrReceiver.resume(); //Important
   delay(100);
 }
 }while(valeur == iValue);
 delay(1000);
}
   break;
    case 82:
   {
delay(1000);
// remettre à zero
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(0, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(1, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(2, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(3, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(4, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(5, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(6, 0, pulselen);
}
// Affiche le chiffre 8
  // Segment 2
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(0, 0, pulselen);
}
 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(2, 0, pulselen);
}
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(3, 0, pulselen);
}
 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(4, 0, pulselen);
}
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(5, 0, pulselen);
}
 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(6, 0, pulselen);
}
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(1, 0, pulselen);
}
 delay(100);
do {
   if ( IrReceiver.decode() ) {
   iValue = IrReceiver.decodedIRData.command; // Valeur en décimal
   Serial.println(iValue);
   IrReceiver.resume(); //Important
   delay(100);
 }
 }while(valeur == iValue);
 delay(1000);
}
   break;
       case 74:
   {
delay(1000);
// remettre à zero
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(0, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(1, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(2, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(3, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(4, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(5, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(6, 0, pulselen);
}
// Affiche le chiffre 9
 // Segment 2
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(0, 0, pulselen);
}
 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(2, 0, pulselen);
}
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(3, 0, pulselen);
}
 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(4, 0, pulselen);
}
 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(6, 0, pulselen);
}
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(1, 0, pulselen);
}
 delay(100);
do {
   if ( IrReceiver.decode() ) {
   iValue = IrReceiver.decodedIRData.command; // Valeur en décimal
   Serial.println(iValue);
   IrReceiver.resume(); //Important
   delay(100);
 }
 }while(valeur == iValue);
 delay(1000);
}
   break;
      case 22:
   {
delay(1000);
// remettre à zero
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(0, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(1, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(2, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(3, 0, pulselen);
}

for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(4, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(5, 0, pulselen);
}
for (uint16_t pulselen = SERVOMAX; pulselen > SERVOMIN; pulselen--){
 myServo.setPWM(6, 0, pulselen);
}
// Affiche le chiffre 0
  // Segment 2
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(0, 0, pulselen);
}
 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(2, 0, pulselen);
}

 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(4, 0, pulselen);
}
 for (uint16_t pulselen = SERVOMIN; pulselen < SERVOMAX; pulselen++){
 myServo.setPWM(5, 0, pulselen);
}
 // Segment 5
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(6, 0, pulselen);
}
 for (uint16_t pulselen = SERVOMIN_1; pulselen < SERVOMAX_1; pulselen++){
 myServo.setPWM(1, 0, pulselen);
}
 delay(100);
do {
   if ( IrReceiver.decode() ) {
   iValue = IrReceiver.decodedIRData.command; // Valeur en décimal
   Serial.println(iValue);
   IrReceiver.resume(); //Important
   delay(100);
 }
 }while(valeur == iValue);
 delay(1000);
}
   break;
   default:
   Serial.println(iValue);
   break;
  }
   }
