# Conexão do Node-RED com o HiveMQ

Este documento descreve o processo de configuração do Node-RED para se conectar ao HiveMQ, incluindo a utilização de um Arduino para leitura de dados de umidade e temperatura.

## Fluxo no Node-RED

### 1. Serial In

- **Nome:** Arduino Serial
- **Serial Port:** COM4:9600-8N1
- **Configuração:** 
 ## Configuração do Nó Serial In

### Nome
- **Nome:** Nome

### Serial Port
- **Serial Port:** COM4

### Settings

| Configuração | Valor |
|--------------|-------|
| Baud Rate    | 9600  |
| Data Bits    | 8     |
| Parity       | None  |
| Stop Bits    | 1     |

### DTR/RTS/CTS/DSR

| Pino | Estado |
|------|--------|
| DTR  |        |
| RTS  |        |
| CTS  |        |
| DSR  |        |

### Input

- **Optionally wait for a start character of:** (deixe em branco se não for necessário)
- **Split input on the character:** \n
- **Deliver:** ASCII strings

### Output

- **Add character to output messages:** (deixe em branco se não for necessário)

### Request

- **Default response timeout:** 10000 ms


### 2. Function
- **Nome:** Parse Sensor Data
- Código:

```javascript
// Verifique se msg.payload está definido
if (msg.payload) {
    // Remova caracteres de nova linha e espaços extras
    var payload = msg.payload.trim();
    
    // Verifique se a string contém "Umidade" ou "T="
    if (payload.includes("Umidade")) {
        // Extraia o valor de umidade
        var umidade = payload.split(":")[1].trim();
        msg.umidade = parseFloat(umidade);
    } else if (payload.includes("T=")) {
        // Extraia o valor de temperatura
        var temperatura = payload.split("T=")[1].split(" ")[0].trim();
        msg.temperatura = parseFloat(temperatura);
    }
    
    // Retorne a mensagem com os novos campos
    return msg;
} else {
    // Se msg.payload não estiver definido, retorne null para não continuar o fluxo
    return null;
}
```
### 3. MQTT Out

- **Nome:** HiveMQ Broker
- **Servidor:** mqtt-dashboard.com
- **Porta:** 1883
- **Tópico:** topic_test
- **QoS:** 0
- **Reter:** 
- **Conectar automaticamente:** Sim
- **Usar TLS:** Não
- **Protocolo:** MQTT V3.1.1
- **ID do cliente:** Deixe em branco para geração automática
- **Mantenha-se vivo:** 60
- **Sessão:** Usar sessão limpa

### 4. Debug Nodes

#### Debug Arduino Data

- **Nome:** Debug Arduino Data
- **Saída:** msg.payload
- **Para:** Janela de depuração, Console do sistema, Estado do nó (32 caracteres)

#### Debug Processed Data

- **Nome:** Debug Processed Data
- **Saída:** msg.payload
- **Para:** Janela de depuração, Console do sistema, Estado do nó (32 caracteres)

### 5. Inject Nodes

#### Inject Temperature

- **Nome:** Inject Temperature
- **msg.payload:** 26
- **msg.topic:** sensor/temperature

#### Inject Humidity

- **Nome:** Inject Humidity
- **msg.payload:** 60
- **msg.topic:** sensor/humidity

## Configuração do HiveMQ

### Aba Connection

- **Host:** mqtt-dashboard.com
- **Port:** 8884
- **ClientID:** clientId-7qyjclq0wY
- **Connect:** 
- **Username:** Deixe em branco para não usar autenticação
- **Password:** Deixe em branco para não usar autenticação
- **Keep Alive:** 60
- **SSL:** Sim
- **Clean Session:** Sim
- **Last-Will Topic:** Deixe em branco para não usar
- **Last-Will QoS:** 0
