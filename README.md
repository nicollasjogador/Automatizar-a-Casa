# SISTEMAS EMBARCADOS 
 1° Semestre - FATEC Jundiaí
 
 Integrantes:
 - Cristiano Francisco Correa;
 - João Felipe Gustavo;
 - Luis Gustavo do Santos Rosa;
 - Nicollas de Oliveira Juliano;
 - Rafael Massayoshi Hamazaki;
----

# Automatizar-a-Casa

----

# Sumário:

1 - Introdução;

2 - Materiais;

3 - Código-Fonte;

4 - Conclusão do Projeto;

5 - Link do vídeo;

----


# 1 - Introdução:

Projeto desenvolvido para a disciplina Sistemas Embarcados da FATEC - Jundiaí, visando implementar e disponibilizar à comunidade um sistema de baixo custo  em comparação ao que encontra-se comercialmente (como CLP's) que tem como finalidade apresentar a possibilidade de **automação residencial** com o Arduino Mega, com interação simultanea tanto **fisica** (**_Interruptores Touch_**), quanto **virtualmente** (acesso pela rede com o **_Módulo Ethernet_**). 


No **_Módulo Ethernet_**, o usuário utiliza um IP de Hospedagem próprio em seu dispositivo, permitindo conexão por computador ou celular, (ou qualquer outra opção para WEB) para realizar a manobra das "cargas", respectivamente ao sistema de iluminação da residência no nosso caso.

# 2 - Materiais utilizados:

+ Arduino Mega 2560;

![Imagem](./imagens/ARDUINO_MEGA2.jpg)


+ Relés;

![Imagem](./imagens/RELE1.jpg)

+ Módulo de Rede Ethernet W5500 ;

![Imagem](./imagens/ETHERNET.jpg)

+ Placas Touch (Interruptores);

![Imagem](./imagens/TOUCH1.jpg)

+ Módulo Opto-acoplador;

#####  - Proteção das entradas digitais entre os componentes;

![Imagem](./imagens/PROTECAO_ALIMENTACAO13.jpg)

+ Fonte de Alimentação 12V;

![Imagem](./imagens/FONTE.jpg)

+ Lâmpadas


# 3 - Código-Fonte: 



```
// PROJETO DOMOTICA - RESIDÊNCIA KIKO & ADRI
//PINOS COMUNICAÇÃO ENC28J60
//CS  > 53
//MOSI ou SI ou ST >  51
//MISO ou SO  >  100
//SCK  >  52
//RESET > RESET
//INT ou LNT >  2
//GND >  GND
//VCC > 3,3V




// SET DOS PINOS DE ENTRADAS DIGITAIS
const int CORREDOR_IN = 14;
const int SALAESTAR_IN =15;
const int SALAJANTAR_IN = 16;
const int GARAGEM_IN = 17;
const int COZINHA_IN = 18;
const int LAVANDERIA_IN = 19;
const int LAVABO_IN =20;
const int VARANDA_IN = 21;
const int QUINTAL_IN = 22;
const int BANHOSOCIAL_IN = 23;
const int BANHOSUITE_IN = 24;
const int SUITE_IN = 25;
const int CLOSET_IN = 26;
const int QUARTO1_IN = 27;
const int QUARTO2_IN = 28;
const int RESERVA3_IN = 29;
const int RESERVA4_IN = 30;
const int RESERVA5_IN = 31;
const int RESERVA6_IN = 32;
const int RESERVA7_IN = 33;

//SET DOS PINOS DE ENTRADAS ANALÓGICAS
int ANALOG_IN1 = 0;
int ANALOG_IN2 = 1;
int ANALOG_IN3 = 2;
int ANALOG_IN4 = 3;
int ANALOG_IN5 = 4;
int ANALOG_IN6 = 5;
int ANALOG_IN7 = 6;
int ANALOG_IN8 = 7;
int ANALOG_IN9 = 8;
int ANALOG_IN10 = 9;
int ANALOG_IN11 = 10;
int ANALOG_IN12 = 11;
int ANALOG_IN13 = 12;
int ANALOG_IN14 = 13;
int ANALOG_IN15 = 14;
int ANALOG_IN16 = 15;

// SET DOS PINOS DE SAÍDAS DIGITAIS  
const int CORREDOR_OUT = 34;
const int SALAESTAR_OUT = 35;
const int SALAJANTAR_OUT = 36;
const int GARAGEM_OUT = 37;
const int COZINHA_OUT = 38;
const int LAVANDERIA_OUT = 39;
const int LAVABO_OUT = 40;
const int VARANDA_OUT = 41;
const int QUINTAL_OUT = 42;
const int BANHOSOCIAL_OUT = 43;
const int BANHOSUITE_OUT = 44;
const int SUITE_OUT = 45;
const int CLOSET_OUT = 46;
const int QUARTO1_OUT = 47;
const int QUARTO2_OUT = 48;
const int RESERVA3_OUT = 49;
const int RESERVA4_OUT = 3;
const int RESERVA5_OUT = 4;
const int RESERVA6_OUT = 5;
const int RESERVA7_OUT = 6;

// SET DOS PINOS DE SAIDAS ANALÓGICAS

int ANALOG_OUT5 = 7;
int ANALOG_OUT6 = 8;
int ANALOG_OUT7 = 9;
int ANALOG_OUT8 = 10;
int ANALOG_OUT9 = 11;
int ANALOG_OUT10 = 12;
int ANALOG_OUT11 = 13;
 
// set varição estado saidas digitais
int CORREDOR_I = 0;
int CORREDOR_S = LOW;
int SALAESTAR_I = 0;
int SALAESTAR_S = LOW;
int SALAJANTAR_I = 0;
int SALAJANTAR_S = LOW;
int GARAGEM_I = 0;
int GARAGEM_S = LOW;
int COZINHA_I = 0;
int COZINHA_S = LOW;
int LAVANDERIA_I = 0;
int LAVANDERIA_S = LOW;
int LAVABO_I = 0;
int LAVABO_S = LOW;
int VARANDA_I = 0;
int VARANDA_S = LOW;
int QUINTAL_I = 0;
int QUINTAL_S = LOW;
int BANHOSOCIAL_I = 0;
int BANHOSOCIAL_S = LOW;
int BANHOSUITE_I = 0;
int BANHOSUITE_S = LOW;
int SUITE_I = 0;
int SUITE_S = LOW;
int CLOSET_I = 0;
int CLOSET_S = LOW;
int QUARTO1_I = 0;
int QUARTO1_S = LOW;
int QUARTO2_I = 0;
int QUARTO2_S = LOW;
int RESERVA3_I = 0;
int RESERVA3_S = LOW;
int RESERVA4_I = 0;
int RESERVA4_S = LOW;
int RESERVA5_I = 0;
int RESERVA5_S = LOW;
int RESERVA6_I = 0;
int RESERVA6_S = LOW;
int RESERVA7_I = 0;
int RESERVA7_S = LOW;

int anterior1=0;
int anterior2=0;
int anterior3=0;
int anterior4=0;
int anterior5=0;
int anterior6=0;
int anterior7=0;
int anterior8=0;
int anterior9=0;
int anterior10=0;
int anterior11=0;
int anterior12=0;
int anterior13=0;
int anterior14=0;
int anterior15=0;
int anterior16=0;
int anterior17=0;
int anterior18=0;
int anterior19=0;
int anterior20=0;

int estado1 = LOW;
int estado2 = LOW;
int estado3 = LOW;
int estado4 = LOW;
int estado5 = LOW;
int estado6 = LOW;
int estado7 = LOW;
int estado8 = LOW;
int estado9 = LOW;
int estado10 = LOW;
int estado11 = LOW;
int estado12 = LOW;
int estado13 = LOW;
int estado14 = LOW;
int estado15 = LOW;
int estado16 = LOW;
int estado17 = LOW;
int estado18 = LOW;
int estado19 = LOW;
int estado20 = LOW;



void setup() {

 
 
// define os pinos de entradas
pinMode (CORREDOR_IN, INPUT);
pinMode (SALAESTAR_IN, INPUT);
pinMode (SALAJANTAR_IN, INPUT);
pinMode (GARAGEM_IN, INPUT);
pinMode (COZINHA_IN, INPUT);
pinMode (LAVANDERIA_IN, INPUT);
pinMode (LAVABO_IN, INPUT);
pinMode (VARANDA_IN, INPUT);
pinMode (QUINTAL_IN, INPUT);
pinMode (BANHOSOCIAL_IN, INPUT);
pinMode (BANHOSUITE_IN, INPUT);
pinMode (SUITE_IN, INPUT);
pinMode (CLOSET_IN, INPUT);
pinMode (QUARTO1_IN, INPUT);
pinMode (QUARTO2_IN, INPUT);
pinMode (RESERVA3_IN, INPUT);
pinMode (RESERVA4_IN, INPUT);
pinMode (RESERVA5_IN, INPUT);
pinMode (RESERVA6_IN, INPUT);
pinMode (RESERVA7_IN, INPUT);

// define os pinos de saídas:
pinMode (CORREDOR_OUT, OUTPUT);
pinMode (SALAESTAR_OUT, OUTPUT);
pinMode (SALAJANTAR_OUT, OUTPUT);
pinMode (GARAGEM_OUT, OUTPUT);
pinMode (COZINHA_OUT, OUTPUT);
pinMode (LAVANDERIA_OUT, OUTPUT);
pinMode (LAVABO_OUT, OUTPUT);
pinMode (VARANDA_OUT, OUTPUT);
pinMode (QUINTAL_OUT, OUTPUT);
pinMode (BANHOSOCIAL_OUT, OUTPUT);
pinMode (BANHOSUITE_OUT, OUTPUT);
pinMode (SUITE_OUT, OUTPUT);
pinMode (CLOSET_OUT, OUTPUT);
pinMode (QUARTO1_OUT, OUTPUT);
pinMode (QUARTO2_OUT, OUTPUT);
pinMode (RESERVA3_OUT, OUTPUT);
pinMode (RESERVA4_OUT, OUTPUT);
pinMode (RESERVA5_OUT, OUTPUT);
}
 
void loop(){
// le os estados dos interruptores:
CORREDOR_I = digitalRead(CORREDOR_IN);
SALAESTAR_I = digitalRead(SALAESTAR_IN);
SALAJANTAR_I = digitalRead(SALAJANTAR_IN);
GARAGEM_I = digitalRead(GARAGEM_IN);
COZINHA_I = digitalRead(COZINHA_IN);
LAVANDERIA_I = digitalRead(LAVANDERIA_IN);
LAVABO_I = digitalRead(LAVABO_IN);
VARANDA_I = digitalRead(VARANDA_IN);
QUINTAL_I = digitalRead(QUINTAL_IN);
BANHOSOCIAL_I = digitalRead(BANHOSOCIAL_IN);
BANHOSUITE_I = digitalRead(BANHOSUITE_IN);
SUITE_I = digitalRead(SUITE_IN);
CLOSET_I = digitalRead(CLOSET_IN);
QUARTO1_I = digitalRead(QUARTO1_IN);
QUARTO2_I = digitalRead(QUARTO2_IN);
RESERVA3_I = digitalRead(RESERVA3_IN);
RESERVA4_I = digitalRead(RESERVA4_IN);
RESERVA5_I = digitalRead(RESERVA5_IN);
RESERVA6_I = digitalRead(RESERVA6_IN);
RESERVA7_I = digitalRead(RESERVA7_IN);
  
//controle lampada CORREDOR 
if (CORREDOR_I == HIGH && anterior1 == LOW) {
estado1 = !estado1;
}
digitalWrite(CORREDOR_OUT,estado1);
anterior1=CORREDOR_I;
delay(50);

//controle lampada sala de estar 
if (SALAESTAR_I == HIGH && anterior2 == LOW) {
estado2 = !estado2;
}
digitalWrite(SALAESTAR_OUT,estado2);
anterior2=SALAESTAR_I;
delay(50);  
}
  //controle lampada SALA DE JANTAR 
if (SALAJANTAR_I == HIGH && anterior3 == LOW) {
estado3 = !estado3;
}
digitalWrite(SALAJANTAR_OUT,estado3);
anterior3=SALAJANTAR_I;
delay(50);
  //controle lampada GARAGEM
if (GARAGEM_I == HIGH && anterior4 == LOW) {
estado4 = !estado4;
}
digitalWrite(GARAGEM_OUT,estado4);
anterior4=GARAGEM_I;
delay(50);
    //controle lampada COZINHA 
if (COZINHA_I == HIGH && anterior5 == LOW) {
estado5 = !estado5;
}
digitalWrite(COZINHA_OUT,estado5);
anterior5=COZINHA_I;
delay(50);
    //controle lampada LAVANDERIA 
if (LAVANDERIA_I == HIGH && anterior6 == LOW) {
estado6 = !estado6;
}
digitalWrite(LAVANDERIA_OUT,estado6);
anterior6=LAVANDERIA_I;
delay(50);
    //controle lampada LAVABO 
if (LAVABO_I == HIGH && anterior7 == LOW) {
estado7 = !estado7;
}
digitalWrite(LAVABO_OUT,estado7);
anterior7=LAVABO_I;
delay(50);
    //controle lampada VARANDA  
if (VARANDA_I == HIGH && anterior8 == LOW) {
estado8 = !estado8;
}
digitalWrite(VARANDA_OUT,estado8);
anterior8=VARANDA_I;
delay(50);
    //controle lampada QUINTAL  
if (QUINTAL_I == HIGH && anterior9 == LOW) {
estado9 = !estado9;
}
digitalWrite(QUINTAL_OUT,estado9);
anterior9=QUINTAL_I;
delay(50);
    //controle lampada BANHEIRO SOCIAL   
if (BANHOSOCIAL_I == HIGH && anterior10 == LOW) {
estado10 = !estado10;
}
digitalWrite(BANHOSOCIAL_OUT,estado10);
anterior10=BANHOSOCIAL_I;
delay(50);
    //controle lampada BANHEIRO SUITE 
if (BANHOSUITE_I == HIGH && anterior11 == LOW) {
estado11 = !estado11;
}
digitalWrite(BANHOSUITE_OUT,estado11);
anterior11=BANHOSUITE_I;
delay(50);
    //controle lampada SUITE  
if (SUITE_I == HIGH && anterior12 == LOW) {
estado12 = !estado12;
}
digitalWrite(SUITE_OUT,estado12);
anterior12=SUITE_I;
delay(50);
    //controle lampada CLOSET
if (CLOSET_I == HIGH && anterior13 == LOW) {
estado13 = !estado13;
}
digitalWrite(CLOSET_OUT,estado13);
anterior13=CLOSET_I;
delay(50);
    //controle lampada QUARTO 1
if (QUARTO1_I == HIGH && anterior14 == LOW) {
estado14 = !estado14;
}
digitalWrite(QUARTO1_OUT,estado14);
anterior14=QUARTO1_I;
delay(50);
    //controle lampada QUARTO 2 
if (QUARTO2_I == HIGH && anterior15 == LOW) {
estado15 = !estado15;
}
digitalWrite(QUARTO2_OUT,estado15);
anterior15=QUARTO2_I;
delay(50);
   //controle lampada RESERVA3 
if (RESERVA3_I == HIGH && anterior16 == LOW) {
estado16 = !estado16;
}
digitalWrite(RESERVA3_OUT,estado16);
anterior16=RESERVA3_I;
delay(50);
 
   //controle lampada RESERVA4 
if (RESERVA4_I == HIGH && anterior17 == LOW) {
estado17 = !estado17;
}
digitalWrite(RESERVA4_OUT,estado17);
anterior17=RESERVA4_I;
delay(50);
   //controle lampada RESERVA5  
if (RESERVA5_I == HIGH && anterior18 == LOW) {
estado18 = !estado18;
}
digitalWrite(RESERVA5_OUT,estado18);
anterior18=RESERVA5_I;
delay(50);

// SIMULAÇÃO DE PRESENÇA NA RESIDÊNCIA
/*if (CORREDOR_I == HIGH){
    digitalWrite(SALAESTAR_OUT, HIGH);
    delay (1500);
    digitalWrite(COZINHA_OUT, HIGH);
    delay (200);
    digitalWrite(SALAESTAR_OUT, LOW);

    delay (1300);
    digitalWrite(LAVANDERIA_OUT, HIGH);
    delay (200);
    digitalWrite (COZINHA_OUT,LOW) ;
    
   delay (1300);
    digitalWrite(BANHOSOCIAL_OUT, HIGH);
    delay (200);
    digitalWrite (LAVANDERIA_OUT,LOW);

    delay (1300);
    digitalWrite(BANHOSUITE, HIGH);
    delay (200);
    digitalWrite (BANHOSOCIAL_OUT,LOW);

    delay (1300);
    digitalWrite(SUITE_OUT, HIGH);
    delay (200);
    digitalWrite (BANHOSUITE_OUT, LOW) ;

    delay (1300);
    digitalWrite(QUARTO1_OUT, HIGH);
    delay (200);
    digitalWrite (SUITE_OUT,LOW);

    delay (1300);
    digitalWrite(QUARTO2_OUT, HIGH);
    delay (200);
    digitalWrite (QUARTO1_OUT,LOW);*/

    
}

```
----
### - Observações:

_O código-fonte atual encontra-se **inacabado** com relação a função de comunicação de rede, entre servidor e placa Arduino, pois durante a execução do mesmo não houve tempo hábil para implementar a solução antes da entrega e apresentação do projeto. 
    Assim que encontrada a melhor versão do cógico para funcionamento ideal e completo do propósito do projeto, o atualizaremos à fim de compartilhar com a comunidade._


----
# 4 - Conclusão do Projeto:

Projeto com a montagem final em placa MDF para suporte/fixação dos componentes principais e interruptores touch, juntamente a uma maquete da planta baixa conectada aos saídas/relés do circuito para simulação do protótipo e interligado ao computador para controle por meio da conexão Ethernet.

![Imagem](./imagens/projetomontado.jpg)

![Imagem](./imagens/pagina.jpg)

![Imagem](./imagens/interruptor.jpg)

![Imagem](./imagens/circuito.jpg)

![Imagem](./imagens/casa.jpg)

# 5 - Link do Vídeo

[Projeto Funcionando](https://www.youtube.com/watch?v=zsscLPNTAK8)
