# Projeto Node-RED e HiveMQ

Este projeto demonstra como conectar o Node-RED ao HiveMQ para publicar e subscrever mensagens MQTT.

## Índice

- [Pré-requisitos](#pré-requisitos)
- [Instalação](#instalação)
- [Configuração do HiveMQ](#configuração-do-hivemq)
- [Configuração do Node-RED](#configuração-do-node-red)
- [Testes](#testes)
- [Contribuição](#contribuição)
- [Licença](#licença)

## Pré-requisitos

Antes de começar, você precisará ter os seguintes softwares instalados:

- [Node.js](https://nodejs.org/)
- [Node-RED](https://nodered.org/)
- Uma instância do [HiveMQ](https://www.hivemq.com/)

## Instalação

### Node-RED

1. Instale o Node-RED globalmente via npm:
    ```sh
    npm install -g node-red
    ```

2. Inicie o Node-RED:
    ```sh
    node-red
    ```

3. Acesse a interface web do Node-RED em `http://localhost:1880`.

### HiveMQ

1. Crie uma conta no [HiveMQ Cloud](https://www.hivemq.com/mqtt-cloud-broker/) ou configure seu próprio broker HiveMQ.

## Configuração do HiveMQ

1. Acesse seu painel do HiveMQ Cloud ou seu broker local.
2. Anote as seguintes informações:
    - URL do broker
    - Porta
    - Username (se necessário)
    - Password (se necessário)

## Configuração do Node-RED

1. Na interface do Node-RED, adicione um nó MQTT In e um nó MQTT Out.
2. Configure o nó MQTT In:
    - Server: `Adicionar novo servidor MQTT`
    - Server: `URL do broker`
    - Port: `Porta do broker`
    - Username: `Seu username` (se necessário)
    - Password: `Sua senha` (se necessário)
    - Topic: `Tópico que você deseja subscrever`

3. Configure o nó MQTT Out:
    - Server: `Adicionar novo servidor MQTT` (ou usar o mesmo do nó MQTT In)
    - Topic: `Tópico para publicar`

4. Conecte os nós MQTT In e MQTT Out a outros nós conforme necessário para processar as mensagens.

## Testes

1. Publique uma mensagem no tópico configurado usando o HiveMQ ou outro cliente MQTT.
2. Verifique se o Node-RED está recebendo a mensagem e processando conforme esperado.
3. Envie uma mensagem do Node-RED usando o nó MQTT Out e verifique se o HiveMQ recebe a mensagem.

## Contribuição

Contribuições são bem-vindas! Sinta-se à vontade para abrir issues ou pull requests.

## Licença

Este projeto está licenciado sob a [MIT License](LICENSE).

