# Controle de Servo Motor e LED com ESP32
Este projeto é um exemplo simples de como utilizar um ESP32 para controlar um servo motor e um LED. A ideia é fazer o servo se mover entre posições específicas enquanto o LED acende e apaga em sincronia com esses movimentos.
É um bom ponto de partida para quem está aprendendo a trabalhar com servo motores, sinais PWM e controle digital com microcontroladores.

Objetivos

Controlar um servo motor usando a biblioteca ESP32Servo.
Acender e apagar um LED de forma sincronizada com os movimentos do servo.
Aplicar conceitos básicos de eletrônica e programação embarcada.

Materiais necessários
ESP32
Servo motor (como SG90)
LED comum
Resistor de 220 ohms (para o LED)
Jumpers
Protoboard
Esquema de ligação

Conexões sugeridas:
Componente	ESP32 GPIO
Servo	GPIO 2
LED	GPIO 5
O resistor de 220 ohms deve ser colocado em série com o LED.
Conecte todos os GNDs (servo, LED, ESP32) ao mesmo terra.
Para melhor desempenho, especialmente com servos maiores, recomenda-se uma fonte externa de 5V para alimentar o servo.

Instalação da biblioteca
Antes de rodar o código, é necessário instalar a biblioteca ESP32Servo.

Passos no Arduino IDE:
Vá em Sketch > Incluir Biblioteca > Gerenciar Bibliotecas.
Procure por ESP32Servo.
Instale a biblioteca.
     Código basico de funcionamento;
     
        #include <ESP32Servo.h>  // Biblioteca para controlar servo motor com ESP32
        Servo motor;  // Objeto para controle do servo
        #define LED_PIN 5  // Define o pino onde o LED está conectado
        
        void setup() {
          motor.setPeriodHertz(50);        // Define a frequência do servo (50Hz padrão)
          motor.attach(2, 500, 2400);      // Conecta o servo no pino 2, com limites de pulso
          motor.write(90);                 // Posição inicial no centro (90 graus)
          
          pinMode(LED_PIN, OUTPUT);        // Configura o pino do LED como saída
        }
        
        void loop() {
          motor.write(180);               // Move o servo para 180 graus
          digitalWrite(LED_PIN, HIGH);   // Acende o LED
          delay(1000);                    // Aguarda 1 segundo
        
          motor.write(90);               // Volta para 90 graus
          digitalWrite(LED_PIN, LOW);   // Apaga o LED
          delay(1000);
        
          motor.write(0);                // Move para 0 grau
          delay(1000);
        
          motor.write(90);               // Volta para o centro
          digitalWrite(LED_PIN, HIGH);  // Acende o LED
          delay(1000);
        }

O que esse código faz!?

O servo começa na posição central (90°).
Em seguida, gira para 180°, enquanto o LED acende.
Depois, retorna para 90° e o LED apaga.
O servo vai então para 0°, espera, e retorna ao centro com o LED aceso novamente.
O ciclo se repete indefinidamente.

Observações
O ESP32 pode não fornecer corrente suficiente para alguns servos. Se o movimento estiver fraco ou errático, use uma fonte de alimentação externa para o servo.
Sempre conecte o GND da fonte externa ao GND do ESP32 para garantir o funcionamento correto do sinal PWM.

conclusão
 Com apenas alguns materiais e linhas de código você consegue "automatizar" algo!

 ![1000058528](https://github.com/user-attachments/assets/1a24e145-01a2-405d-9719-7abe1969dc6d)

