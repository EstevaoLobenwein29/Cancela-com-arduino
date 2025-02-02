Projeto de Cancela Automática com Arduino

Este projeto utiliza um **Arduino Uno**, um **sensor ultrassônico** e um **microservo** para criar uma cancela automática. O sensor ultrassônico mede a distância e, se um objeto for detectado a menos de 30 cm, o servo motor move a cancela para abrir (de 100° para 0°) e depois fecha (de 0° para 100°).

## Componentes Usados:
- Arduino Uno
- Sensor Ultrassônico HC-SR04
- Microservo (SG90)
- Protoboard
- Fios macho-macho e macho-fêmea

## Como Funciona:
1. O sensor ultrassônico mede a distância em relação a objetos à sua frente.
2. Quando a distância for inferior a 30 cm, o microservo será acionado para abrir a cancela.
3. O servo fica aberto por 1,5 segundos e depois fecha.

## Como Usar:
1. Conecte os componentes conforme as instruções de montagem.
2. Faça o upload do código no Arduino.
3. Teste o sensor ultrassônico para ver a cancela abrir e fechar automaticamente.

## Licença:
Este projeto é de código aberto e pode ser utilizado de acordo com a licença MIT.
