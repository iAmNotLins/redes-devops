# redes-devops

## TCP/IP 
### Explicação breve.

[![](https://mermaid.ink/img/pako:eNpVT0FugzAQ_AraM0EYYwI-VEpDb-mlzamQwwo7gAo2MkZtinhND31IPlZClFTd087Mzu7OCIUWEjgcG_1RVGiss09z5cy1yTZdUxd4_jl_a2e3PjjOavVw1R6zvUHVd9pY6ezCw5-yzV6kkP1_Ms2eVIPFMrow4EJpagHcmkG60ErT4gXCeJFzsJVsZQ58bgWa9xxyNc2eDtWb1u3NZvRQVsCP2PQzGjqBVqY1lgbbO4uD1a8nVdw8UtRWm-dr6CX7vEcqIc1WD8oCpxFdDgEf4RM4i6hHAxqHLIoZS5gLJ-ABIx6LKSN-ECfUXxM6ufC1fOZ7jJDQT6LQpyQgSRhPvwVsa6c?type=png)](https://mermaid.live/edit#pako:eNpVT0FugzAQ_AraM0EYYwI-VEpDb-mlzamQwwo7gAo2MkZtinhND31IPlZClFTd087Mzu7OCIUWEjgcG_1RVGiss09z5cy1yTZdUxd4_jl_a2e3PjjOavVw1R6zvUHVd9pY6ezCw5-yzV6kkP1_Ms2eVIPFMrow4EJpagHcmkG60ErT4gXCeJFzsJVsZQ58bgWa9xxyNc2eDtWb1u3NZvRQVsCP2PQzGjqBVqY1lgbbO4uD1a8nVdw8UtRWm-dr6CX7vEcqIc1WD8oCpxFdDgEf4RM4i6hHAxqHLIoZS5gLJ-ABIx6LKSN-ECfUXxM6ufC1fOZ7jJDQT6LQpyQgSRhPvwVsa6c)



### Abordagem top down(começa da mais alta para mais baixa) 

### Aplicação (Layer 7)
#### é onde roda o protocolo http de comunicação entre sites, entre apis, smpt, tudo isso roda na camada de aplicação. Ela usa os recursos das camadas de baixa o para enviar as informações de um lado para o outro.

### Transporte (L4)
#### Vai tratar com portas e sockets, vai conectar dois processos. E aonde roda o tcp, udp.

### Rede (L3)
#### Camada de roteamento(hosts) vai conectar um computador ao outro. Permitir que os pacotes trafeguem na nossa rede.

### Enlace (L2)
#### Camada de link, precisa de cabo conectado.

## A vida de um pacote. 

| Camada (Envio) | Unidade de Dados | Fluxo | Unidade de Dados | Camada (Recepção) |
| :--- | :--- | :---: | :--- | :--- |
| **Aplicação** | HTTP Post | ⬇️ | Recebe o Post | **Aplicação** |
| **Transporte** | Segmento TCP | ⬇️ | Segmento TCP | **Transporte** |
| **Rede** | Datagrama IP | ⬇️ | Datagrama IP | **Rede** |
| **Link** | Frame | ⬇️ | Frame | **Link** |
| **Física** | Frame | ➡️ | Frame | **Física** |
| | **Conexão Física** | | **Conexão Física** | |



#### payload é os dados(informações http) 

#### http é um protocolo que por baixo dos panos ele vai usar o tcp
#### Transporte - quebra isso em vários segmentos para poder fazer esse transporte. Ele também é responsável pela porta que vai ser enviado, exemplo porta :80
#### Rede - é responsável por saber o IP a quem ela precisa enviar, ela basicamente pega as informações acima e adiciona o ip nela. 
#### Link - datagrama deixa de ser um datagrama e vira um frame, será transportado através desse link.
#### Física - Cabos fibra ótica aonde vai passar isso 

### O processo acima é a parte de envio, no recebimento é somente inverter o processo.
#### Cada camada injeta os heders importantes para cada camada. Transporte coloca a porta, rede coloca o IP e por ai vai. Isso faz com que saibam exatamente aonde esse pacote precisa ser entregue.


A Escadinha do TCP/IP (Encapsulamento)

| Camada | L2 Header | L3 Header | L4 Header | L5+ Header | Payload (Dados) |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **L5** | | | | **App Header** | blog |
| **L4** | | | **TCP Header** | App Header | blog |
| **L3** | | **IP Header** | TCP Header | App Header | blog |
| **L2** | **Ethernet** | IP Header | TCP Header | App Header | blog |
| **L1** | `0101...` | `1010...` | `0111...` | `1100...` | `0101` |
