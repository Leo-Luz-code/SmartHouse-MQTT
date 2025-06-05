# **SmartHouse - MQTT com Raspberry Pi Pico W**  

🚀 **Um projeto IoT para monitorar sensores e controlar dispositivos via MQTT.**  

---

## **Objetivo**  
Este projeto demonstra como usar a **Raspberry Pi Pico W** como um cliente MQTT para:  
✔ **Publicar dados** de sensores (temperatura, umidade e qualidade do ar simulados).  
✔ **Receber comandos** para controlar LEDs e buzzer remotamente.  
✔ **Conectar-se a um broker MQTT** (como Mosquitto, HiveMQ ou EMQX) com autenticação segura.  

---

## **Funcionalidades**  

### **📡 Conexão MQTT**  
- Conecta-se ao broker MQTT via Wi-Fi.  
- Suporta autenticação por usuário e senha (configurável em `env.h`).  
- Mantém conexão ativa com **Keep Alive (60s)**.  

### **📤 Publicação de Dados**  
| Tópico            | Descrição                          | Exemplo de Mensagem |  
|-------------------|-----------------------------------|---------------------|  
| `/temperature`    | Temperatura interna da Pico (°C)  | `"27.50"`           |  
| `/humidity`       | Umidade simulada (0-100%)         | `"65"`              |  
| `/air_quality`    | Qualidade do ar simulada (ppm)    | `"850"`             |  

### **📥 Controle por MQTT**  
| Tópico          | Ação                              | Comandos Válidos    |  
|----------------|----------------------------------|--------------------|  
| `/led`         | Liga/desliga LED onboard        | `"On"`, `"Off"`    |  
| `/green_led`   | Controla LED verde (GPIO11)      | `"On"`, `"Off"`    |  
| `/blue_led`    | Controla LED azul (GPIO12)       | `"On"`, `"Off"`    |  
| `/red_led`     | Controla LED vermelho (GPIO13)   | `"On"`, `"Off"`    |  

### **⚠️ Alertas Sonoros**  
- O **buzzer (GPIO21)** é ativado quando:  
  - Umidade > **65%** (bips lentos).  
  - Qualidade do ar > **1000 ppm** (bips rápidos).  

---

## **📦 Hardware Utilizado**  
| Componente          | Função                          | Conexão na Pico W  |  
|---------------------|--------------------------------|-------------------|  
| **Joystick**        | Simula umidade (VRY) e qualidade do ar (VRX) | `GPIO26` (VRX), `GPIO27` (VRY) |  
| **LED RGB**         | Feedback visual                | `GPIO11` (Verde), `GPIO12` (Azul), `GPIO13` (Vermelho) |  
| **Buzzer**          | Alerta sonoro                  | `GPIO21` (PWM)    |  
| **Sensor de Temp.** | Temperatura interna do RP2040  | ADC interno       |  

---

## **⚙️ Configuração**  
1. **Configure o `env.h`** (renomeie `env_example.h`):  
   ```c
   #define WIFI_SSID "SUA_REDE"  
   #define WIFI_PASSWORD "SENHA_WIFI"  
   #define MQTT_SERVER "broker.mqtt.com"  
   #define MQTT_USERNAME "usuario"  // Opcional  
   #define MQTT_PASSWORD "senha"    // Opcional  
   ```

2. **Compile e envie** para a Pico W (usando VS Code + PlatformIO ou Arduino IDE).  

---

## **🌐 Exemplo de Fluxo MQTT**  
1. A Pico publica em `/temperature`:  
   ```json
   "27.50"
   ```  
2. Um app envia `"On"` para `/red_led` → LED vermelho acende.  
3. Se umidade > 65%, a Pico ativa o **buzzer** e publica em `/humidity`:  
   ```json
   "67"
   ```  

---

## **📌 Próximos Passos**  
- [ ] Adicionar sensores reais (DHT22, MQ-135).  
- [ ] Integrar com Node-RED para dashboard.  
- [ ] Implementar TLS para conexão segura.  

---

## **📚 Recursos**  
- [Biblioteca lwIP para MQTT](https://www.nongnu.org/lwip/)  
- [Tutorial Mosquitto MQTT](https://mosquitto.org/)  

---

✨ **Contribuições são bem-vindas!** Sinta-se à vontade para abrir **issues** ou **pull requests**.  

**Licença:** MIT  
**Autor:** Leonardo Rodrigues Luz  

--- 

🔗 **Clone o repositório:**  
```bash
git clone https://github.com/seu-usuario/smarthouse-mqtt-pico.git
```
