# curso-kafka

## Iniciando o ambiente
```powershell
docker-compose up -d
```

## Criando um tópico
```powershell
docker exec broker `
kafka-topics --bootstrap-server broker:9092 `
             --create `
             --topic quickstart
```

Ao executar esse comando você deve obter o seguinte resultado.
![resultado da operação de criação do tópico: Created topic quickstart](/docs/img/docker-exec-borker-resultado.PNG)

## Produzindo mensagens
Abra um novo console e execute o seguinte comando.

```powershell
docker exec --interactive --tty broker `
kafka-console-producer --bootstrap-server broker:9092 `
                       --topic quickstart
```
Ele vai abrir a interface do kafka para que você comece a produzir mensagens, conforme a imagem a seguir.

Assim:
![resultado da operação de criação do producer: Interface de linha de comando do kafka producer aguardando entrada de mensagens. ](/docs/img/docker-exec-borker-kafka-console-producer.PNG)

A cada linha digitada a interface entende que é uma nova mensagem e a envia para o tópico.

![Inserindo as mensagens Mensagem 1, Mensagem 2 e Mensagem 3 na interface do produtor. A cada mensagem um enter para mudar de linha.](/docs/img/docker-exec-borker-kafka-console-producer-mensagens.PNG)


## Lendo as mensagens

Abra um novo console e execute o comando a seguir.

```powershell
docker exec --interactive --tty broker `
kafka-console-consumer --bootstrap-server broker:9092 `
                       --topic quickstart `
                       --from-beginning
```

![O Consumer foi criado e apresenta as mensagens: Mensagem 1, Mensagem 2 e Mensagem 3](/docs/img/docker-exec-borker-kafka-console-consumer.PNG)


## Liberando recursos

```powershell
#Pára o ambiente e remove os containers as redes e os volumes.
docker-compose down -v
```