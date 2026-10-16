<div align="center">
  
## Simulador de Roteamento UDP

## 🎯 Sobre o Projeto
O projeto consiste em uma aplicação que simula a troca de tabelas de roteamento e o envio de mensagens de texto entre roteadores. O simulador lê os IPs vizinhos a partir de um arquivo de configuração e cadastra-os em uma tabela de roteamento local com métrica 1. A aplicação utiliza socket UDP para enviar as mensagens para a porta 9000 do roteador vizinho. As tabelas são atualizadas com base nos anúncios periódicos dos vizinhos, incrementando a métrica em 1 e ajustando as saídas conforme as rotas mais curtas recebidas. Além das tabelas, a aplicação permite o envio de mensagens de texto, aceitando as que são direcionadas a ela própria ou roteando as mensagens para o próximo roteador do caminho estipulado na tabela.

## ⚙️ Pré-requisitos e Dependências
- Ter o Node.js instalado no computador.


## 📁 Estrutura de Diretórios
-  `script.js`: Arquivo principal contendo toda a lógica do simulador em JavaScript executado via Node.js.
-  `roteadores.txt`: Arquivo de texto de configuração onde os endereços IP dos roteadores vizinhos devem ser informados, com um endereço IP por linha. Como exemplo, um endereço IP configurado é `10.1.1.117`.
-  `Readme.md `: Arquivo de documentação para referências sobre o funcionamento e comandos.


## 🚀 Como Executar
O comando para rodar a aplicação no terminal é:
`node [fileName].js <ip_computador> [arquivo_de_visinhos].txt`.
Para a estrutura atual do código, o comando a ser utilizado será similar a: `node script.js <SEU_IP> roteadores.txt`.



## 🛠️ Pipeline de Execução
O funcionamento baseia-se em partições assíncronas do socket UDP, sem possuir uma função main direta:
- `socket.on`: Fica escutando caso receba uma mensagem e verifica o seu primeiro caractere:
   - `!`: Chama a função handleTextMessage, que separa a mensagem conforme o padrão exigido ou a encaminha caso não seja para o seu IP.
   - `*`: Chama a função handleRouterAnnouncement, que verifica se o IP já existe na tabela, o adiciona se não existir e compartilha a tabela com todos caso haja alteração.
   - `#`: Chama a função handleRouteAnnouncement, que verifica a tabela recebida, adiciona IPs desconhecidos como destino e estipula como rota o IP do roteador que enviou a tabela.
- `socket.bind`: Inicia o servidor e chama funções para a manutenção periódica da operação: 
   - `sendRoutingTable`: Função de envio da tabela que é disparada a cada 15s.
   - `printRoutingTable`: Função para imprimir a tabela ao usuário a cada 20s.
   - `checkTimeouts`: Função para verificar o tempo de comunicação dos vizinhos a cada 35s.
- `setupCli`: Interface de linha de comando para permitir a interação do usuário durante a execução:
   - Para envio de mensagem, utiliza-se a instrução `msg` (ex: "digite msg").
   - Para verificação imediata da tabela, digite `table`.
   - Para enviar anúncio de roteador online, digite `on`.
# Autores:
| [<img loading="lazy" src="https://avatars.githubusercontent.com/u/142232479?v=4" width=115><br><sub>Luiza Hackenhaar Naziazeno</sub>](https://github.com/luizahackenhaarnaziazeno) | [<img loading="lazy" src="https://github.com/ncjhsn7.png" width=115><br><sub>ncjhsn7</sub>](https://github.com/ncjhsn7) | [<img loading="lazy" src="https://github.com/SophiaSilveira.png" width=115><br><sub>Sophia Silveira</sub>](https://github.com/SophiaSilveira) |
| :---: | :---: | :---: |
