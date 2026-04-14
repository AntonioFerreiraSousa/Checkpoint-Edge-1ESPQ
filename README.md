# 🍇 Vinheria Agnello — Monitor de Luminosidade

![Arduino](https://img.shields.io/badge/Arduino-Uno%20R3-blue) ![Sensor](https://img.shields.io/badge/Sensor-LDR-green) ![Simulação](https://img.shields.io/badge/Simulação-Tinkercad-orange) ![Linguagem](https://img.shields.io/badge/Linguagem-C%2B%2B%20%2F%20Arduino-lightgrey)

Sistema embarcado de monitoramento ambiental desenvolvido para a **Vinheria Agnello**. Utiliza um sensor de luminosidade (LDR) para medir a intensidade de luz no ambiente e aciona alertas visuais (LEDs) e sonoros (buzzer) conforme o nível detectado, garantindo as condições ideais de armazenamento dos vinhos.

---

## Integrantes

- Antonio do Nascimento Ferreira de Sousa
- Kaio Nincao Maia Dias
- Kaue Fernando Jaques Lopes
- Matheus Martins Santos
- Leonardo Gonçalves Cardoso da Fonseca

---

## Como funciona

```
LDR capta luz → Arduino lê A5 → Converte analógico → digital → Avalia valor → Aciona LED + buzzer
```

O LDR entrega uma resistência variável de acordo com a incidência de luz. O Arduino lê essa variação pela porta analógica `A5` e converte em um valor entre `0` e `1023`. Na simulação do Tinkercad, o valor é ajustado via slider ao clicar no componente.

> **Nota sobre a simulação:** No Tinkercad, os valores oscilam entre **~49** (máxima luz) e **~969** (mínima luz). Os limiares foram calibrados com base nesses limites.

---

## Estados do sistema

| Estado | LED | Buzzer | Faixa de valor |
|--------|-----|--------|----------------|
| ✅ Adequado | 🟢 Verde | Desligado | `valorLuz > 500` |
| ⚠️ Alerta | 🟡 Amarelo | Desligado | `100 ≤ valorLuz < 500` |
| 🚨 Crítico | 🔴 Vermelho | 3 segundos | `valorLuz < 100` |

---

## Componentes

| Componente | Qtd. | Conexão | Observação |
|------------|------|---------|------------|
| Arduino Uno R3 | 1x | — | Microcontrolador principal |
| LDR (Photoresistor) | 1x | `A5` | Sensor de luminosidade ambiente |
| LED Verde | 1x | `D5` | Estado adequado |
| LED Amarelo | 1x | `D6` | Estado de alerta |
| LED Vermelho | 1x | `D7` | Estado crítico |
| Buzzer | 1x | `D8` | Alarme sonoro (3s no estado crítico) |
| Resistor 220Ω | 3x | — | Proteção dos LEDs (um por LED) |
| Resistor 10kΩ | 1x | — | Divisor de tensão com o LDR |
| Protoboard | 1x | — | Montagem dos componentes |


---

## Como monitorar via Serial

Com o Arduino conectado ao computador, abra o **Serial Monitor** na Arduino IDE (`Ctrl+Shift+M`) e configure a taxa de comunicação para `9600 baud`. O valor lido pelo LDR será exibido continuamente, permitindo calibrar os limiares se necessário.

---

## Estrutura do circuito

- O LDR forma um **divisor de tensão** com o resistor de 10kΩ — um terminal ligado ao 5V, o outro ao GND, e o ponto médio ao pino A5.
- Cada LED tem seu próprio resistor de 220Ω em série para limitar a corrente e proteger o componente.
- O buzzer é ligado diretamente ao pino digital D8 com o GND.

---

## Simulação no Tinkercad

1. Acesse [tinkercad.com](https://www.tinkercad.com) e monte o circuito conforme https://www.tinkercad.com/things/5frMtULh1z7-projetoldrvinheriaagnello?sharecode=W5kL3OvtbJI3VmnoSFzhZr475TspkrkprUvPfMrzz9Y
2. Inicie a simulação e clique no LDR para exibir o slider de controle de luminosidade.
3. Observe os LEDs e o Serial Monitor para validar o comportamento do sistema.

---

*Projeto desenvolvido como atividade acadêmica — Vinheria Agnello · Monitor de Luminosidade com Arduino*
