# Monitoramento de Qualidade da Água para Criadouros de Peixes
## Colaboradores

- Eric Darakjian- RM: 557082
- Luciano Meriato - RM: 554546
- Pietro Vitor Pezzente - RM: 557283

## Descrição do problema e solução
Observamos que um dos maiores problemas que vem ocorrendo no oceano é a extinção de várias espécies de peixes devido a poluição, pesca predatória, mudanças climáticas e etc. Foram criados diversos projetos de criadouros sustentáveis para salvar essas espécies ameaçadas com a reprodução em cativeiro, porém os cativeiros precisam estar em plenas condições para que os peixes sobrevivam e possam se reproduzir. Nosso projeto visa monitorar a qualidade da água em criadouros de peixes, auxiliando na manutenção de um ambiente saudável para a reprodução de espécies. Utilizamos o arduíno para fazer a leitura do ph da água e da concentração de gases poluentes. Isso contribui para a sustentabilidade e ajuda a evitar a extinção de peixes.

## Componentes Utilizados

- 15 jumper cables
- 2 resistores de 220 ohms
- 1 resistor de 1K ohm
- 1 LED vermelho
- 1 LED verde
- 1 buzzer
- 1 potenciômetro
- 1 sensor de gás (MQ2)
- 1 Arduino Uno

## Objetivo

O objetivo deste projeto é ajudar na manutenção de criadouros de peixes que trabalham com a reprodução de espécies, monitorando continuamente a concentração de gases e o nível de pH da água. Com isso, é possível garantir que a água esteja em condições ideais para a sobrevivência e reprodução dos peixes.

## Código Utilizado

```cpp
int Vermelho = 10;
int Verde = 8;
int MQ2pin = A0;
int buzzer = 13;
int potPin = A1; // Pino do potenciômetro de pH

void setup() {
  pinMode(Vermelho, OUTPUT);
  pinMode(Verde, OUTPUT);
  pinMode(buzzer, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  float gasValue = analogRead(MQ2pin); // Leitura do sensor de gás
  float pHValue = analogRead(potPin); // Leitura do sensor de pH

  // Printa a concentração de gases constantemente
  Serial.print("Concentracao de gases: ");
  Serial.println(gasValue);

  // Verifica se a concentração de gases está alta
  if (gasValue >= 250) {
    digitalWrite(Vermelho, HIGH);
    digitalWrite(Verde, LOW);
    digitalWrite(buzzer, HIGH);
    tone(buzzer, 1000, 3000);
    Serial.println("Alta concentracao de poluentes detectada");
    Serial.println("/////////////////////////");
  } else {
    digitalWrite(Vermelho, LOW);
    digitalWrite(Verde, HIGH);
    digitalWrite(buzzer, LOW);
    noTone(buzzer);

    // Printa o valor de pH constantemente
    float voltage = pHValue * (5.0 / 1023.0); // Conversão do valor lido para tensão
    float pH = voltage * 14.0; // Mapeamento da tensão para o intervalo de pH (0-14)
    Serial.print("Valor de pH: ");
    Serial.println(pH);

    // Verifica se o pH é ácido, neutro ou alcalino
    if (pH < 6.0) {
      digitalWrite(Vermelho, HIGH);
      digitalWrite(Verde, LOW);
      digitalWrite(buzzer, HIGH);
      tone(buzzer, 1000, 3000);
      Serial.println("PH acido detectado");
      Serial.println("/////////////////////////");
    } else if (pH > 8.0) {
      digitalWrite(Vermelho, HIGH);
      digitalWrite(Verde, LOW);
      digitalWrite(buzzer, HIGH);
      tone(buzzer, 1000, 3000);
      Serial.println("PH alcalino detectado");
      Serial.println("/////////////////////////");
    } else {
      Serial.println("PH neutro");
      Serial.println("/////////////////////////");
    }
  }

  delay(1000); // Aguarda 1 segundo antes de fazer a próxima leitura
}
```

## Funcionamento do código

- Configura os pinos do LED vermelho, LED verde, buzzer e inicia a comunicação serial a 9600 bps.
- Leitura dos valores analógicos do sensor de gás (MQ2) e do potenciômetro (simulando o sensor de pH).
- Imprime a concentração de gases no monitor serial.
- Se a concentração de gases for maior ou igual a 250, aciona o LED vermelho e o buzzer, e imprime uma mensagem de alerta.
- Caso contrário, desativa o LED vermelho e o buzzer, e ativa o LED verde.
- Converte o valor analógico do potenciômetro para tensão e mapeia para o intervalo de pH (0-14).
- Imprime o valor de pH no monitor serial.
- Verifica se o pH é ácido (menor que 6.0), neutro (entre 6.0 e 8.0) ou alcalino (maior que 8.0) e aciona os LEDs e o buzzer de acordo.
- O LED verde só fica ativo quando ambos os valores de concentração de gás e pH estão dentro dos níveis aceitáveis.
- O LED vermelho e o buzzer são ativados se qualquer um dos valores estiver fora dos níveis aceitáveis.
- Se ambos os valores estiverem fora dos níveis aceitáveis, o LED vermelho e o buzzer permanecem ativados.

## Imagem de exemplo

![image](https://github.com/Pic0777/GS---EDGE---1ESPK/assets/162361580/0921271c-c700-4a72-80dd-a10ebefef510)

## Link tinkercad
Você pode acessar o nosso projeto aqui: https://www.tinkercad.com/things/6j6LIJ1YGRG-gs-edge/editel?returnTo=%2Fthings%2F6j6LIJ1YGRG-gs-edge&sharecode=FSd1fcVYWLBnm3HndtFGXM0WNYHO57VkLeJzekYU4vA
## Conclusão
Este projeto demonstra como utilizar sensores com Arduino para monitorar a qualidade da água, fornecendo alertas visuais e sonoros quando os parâmetros estão fora dos níveis seguros. Esta solução pode ser aplicada em criadouros de peixes para garantir um ambiente saudável e sustentável para a reprodução das espécies.
