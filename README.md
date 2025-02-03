# Projeto de Cancela Automática com Arduino
![Montagem do Projeto](imagem_2025-02-02_205054272.png)

Este projeto utiliza um **Arduino Uno**, um **sensor ultrassônico** e um **microservo** para criar uma cancela automática. O sensor ultrassônico mede a distância e, se um objeto for detectado a menos de 10 cm, o servo motor move a cancela para abrir (de 100° para 0°) e depois fecha (de 0° para 100°).

## Componentes Usados:
- 1 Arduino Uno
- 1 Sensor Ultrassônico HC-SR04
- 1 Microservo (SG90)
- 1 Protoboard
- 4 Fios macho-macho
- 4 Fios macho-fêmea
## Como Funciona:
1. O sensor ultrassônico mede a distância em relação a objetos à sua frente.
2. Quando a distância for inferior a 10 cm, o microservo será acionado para abrir a cancela.
3. O servo fica aberto por 1,5 segundos e depois fecha.

## Como Usar:
1. Conecte os componentes conforme as [Instruções de Montagem](#Montagem).
2. Faça o upload do código no Arduino.
3. Teste o sensor ultrassônico para ver a cancela abrir e fechar automaticamente.

O código pode ser acessado na página [Código do programa](#Código-do-programa).

## Licença:
Este projeto é de código aberto e pode ser utilizado de acordo com a licença MIT.

# Montagem
![Montagem do Projeto](‎imagem_2025-02-02_202941771.png)

## Dicas de montagem:
- Use cabos pretos ou azuis para GND e cabos vermelhos para VCC.
- Mantenha seu projeto organizado.

## Instruções de Montagem:
- Pegue seu Arduino Uno e ligue o 5V na parte positiva do protoboard (geralmente indicada na cor vermelha e com o símbolo +).
- Ligue o pino de tensão do motor e do sensor no protoboard.
- Aterre o sensor e o protoboard nos pinos de entrada "GND" do Arduino.
- No sensor, conecte os pinos "Echo" e "Trig" nos pinos de entrada digitais 7 e 6 do Arduino, respectivamente.
- Agora, conecte o pino de saída do motor ao pino digital 9 do Arduino.
- Insira o código do programa e, se tudo correr bem, sua cancela estará pronta.

# Código do Programa


```cpp
#include <Servo.h>

Servo myservo;   

int pos = 10;
int cm = 10;

long readUltrasonicDistance(int triggerPin, int echoPin) {
  pinMode(triggerPin, OUTPUT); 
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);
  pinMode(echoPin, INPUT);
  return pulseIn(echoPin, HIGH);
}

void setup() {
  myservo.attach(9); 
  myservo.write(100); // Define posição inicial
  Serial.begin(9600);
}

void loop() {
  cm = 0.01723 * readUltrasonicDistance(6, 7);

  if (cm < 10) {
    Serial.print(cm);
    Serial.println("cm");

    // Movendo o servo de 100° para 0° mais rápido
    for (pos = 70; pos >= 0; pos -= 1) { 
      myservo.write(pos);             
      delay(10); // Movimento mais rápido                       
    }

    delay(1500); // Mantém 1,5 segundos em 0°

    // Movendo de volta de 0° para 100°
    for (pos = 0; pos <= 70; pos += 1) { 
      myservo.write(pos);
      delay(10);                                      
    }

    delay(2500); // Ajuste para completar 6 segundos totais
  }                          
}
