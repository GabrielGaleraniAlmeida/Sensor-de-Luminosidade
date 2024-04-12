# Sensor-de-Luminosidade

Sistema de Monitoramento de Luminosidade com Alarme
Este projeto utiliza um Arduino para capturar informações de luminosidade do ambiente utilizando um LDR (Light Dependent Resistor) e implementa um sistema de alarme com LEDs e um buzzer para sinalizar condições normais e anormais de luminosidade.

Componentes Necessários
Arduino Uno (ou similar)
LDR (Light Dependent Resistor)
3 LEDs (verde, amarelo, vermelho)
Buzzer
Resistores (para limitar a corrente nos LEDs e no LDR)
Protoboard
Jumpers
Montagem do Circuito
1. Conecte o LDR a uma porta analógica do Arduino.
2. Conecte os LEDs (verde, amarelo, vermelho) a pinos digitais do Arduino, utilizando resistores para limitar a corrente.
3. Conecte o buzzer a um pino digital do Arduino.

Funcionamento
O LDR fornece uma resistência variável dependendo da intensidade da luz incidente sobre ele. O Arduino lê essa resistência utilizando um conversor analógico para digital (ADC). Com base nessa leitura, o Arduino determina se a luminosidade está dentro dos limites estipulados.

Se a luminosidade estiver dentro dos limites, o LED verde é ligado.
Se a luminosidade estiver em níveis de alerta, o LED amarelo é ligado e o buzzer soa por 3 segundos.
Se a luminosidade estiver fora dos limites, o LED vermelho é ligado.
O buzzer só para de soar quando a luminosidade retorna ao nível normal.

Como Reproduzir o Projeto
1. Monte o circuito conforme descrito acima.
2. Carregue o código abaixo no Arduino:

#define LED_VERDE    8
#define LED_AMARELO  9
#define LED_VERMELHO 10
#define BUZZER       7

int limiteInferior = 700;
int limiteSuperior = 900;
int valorLDR = 0;

void setup() 
{
  pinMode(BUZZER, OUTPUT);
  pinMode(LED_VERDE, OUTPUT);
  pinMode(LED_AMARELO, OUTPUT);
  pinMode(LED_VERMELHO, OUTPUT);
  Serial.begin(9600);
}

void loop() 
{
  valorLDR = analogRead(A0);
  
  if (valorLDR < limiteInferior) 
  {
    acaoOK(valorLDR);
  } 
  else if (valorLDR > limiteSuperior) 
  {
    acaoProblema(valorLDR);
  } 
  else 
  {
    acaoAlerta(valorLDR);
  }

  delay(100);
}

void acaoOK(int valorLDR) 
{
  digitalWrite(LED_VERDE, HIGH);
  digitalWrite(LED_AMARELO, LOW);
  digitalWrite(LED_VERMELHO, LOW);
  tone(BUZZER, 0, 0);
  Serial.println("OK - LDR: " + String(valorLDR));
}

void acaoAlerta(int valorLDR) 
{
  digitalWrite(LED_VERDE, LOW);
  digitalWrite(LED_AMARELO, HIGH);
  digitalWrite(LED_VERMELHO, LOW);
  tone(BUZZER, 500, 3000);
  Serial.println("Alerta - LDR: " + String(valorLDR));
}

void acaoProblema(int valorLDR) 
{
  digitalWrite(LED_VERDE, LOW);
  digitalWrite(LED_AMARELO, LOW);
  digitalWrite(LED_VERMELHO, HIGH);
  tone(BUZZER, 1000, 3000);
  Serial.println("Problema - LDR: " + String(valorLDR));
}

3. Conecte o Arduino ao seu computador e abra a IDE do Arduino.
4. Compile e faça o upload do código para o Arduino.
5. Agora, o sistema estará monitorando a luminosidade do ambiente e ativando o alarme conforme necessário.

Considerações Finais

Este é um projeto básico para demonstrar como monitorar a luminosidade do ambiente e implementar um sistema de alarme utilizando Arduino. Você pode expandir este projeto adicionando mais sensores e funcionalidades, como enviar notificações por Wi-Fi ou SMS quando ocorrerem eventos de alerta. Divirta-se explorando as possibilidades!

Se precisar de mais ajuda ou tiver alguma dúvida, não hesite em perguntar!!!;)


Integrantes do grupo:

Gabriel Galerani Almeida
Gabriel Frageri Dias
Gustavo Alves dos Santos Teixeira
Pedro Paulo Garcia Silva





