# REDES-DEVOPS

## TCP/IP 
### Explicação breve.

[![](https://mermaid.ink/img/pako:eNpVT8tugzAQ_BW0Z4Iwxjx8qJSG3tJLm1OBg4UdQAUbGaM2RXxND_2Q_FgdoqTqnnZmdnZ3ZqgUF0Dh2KmPqmHaOIeskI6tbb4durZi55_zt3L2cek4m83DVXvMD5rJcVDaCGcfln_KLn8RXIz_ySx_kh2r7GhQrgy4UOuWAzV6Ei70QvfsAmG-yAWYRvSiAGpbzvR7AYVcrGdg8k2p_mbTaqoboEfWjRZNA2dGZC2rNevvLJuMej3J6uYRvDVKP19Dr9ntHiG50Ds1SQMUx2g9BHSGT6Akwh4OcBKSKCEkJS6cgAYEeSTBBPlBkmI_Rnhx4Wv9zPcIQqGfRqGPUYDSMFl-AQM1a6Q?type=png)](https://mermaid.live/edit#pako:eNpVT8tugzAQ_BW0Z4Iwxjx8qJSG3tJLm1OBg4UdQAUbGaM2RXxND_2Q_FgdoqTqnnZmdnZ3ZqgUF0Dh2KmPqmHaOIeskI6tbb4durZi55_zt3L2cek4m83DVXvMD5rJcVDaCGcfln_KLn8RXIz_ySx_kh2r7GhQrgy4UOuWAzV6Ei70QvfsAmG-yAWYRvSiAGpbzvR7AYVcrGdg8k2p_mbTaqoboEfWjRZNA2dGZC2rNevvLJuMej3J6uYRvDVKP19Dr9ntHiG50Ds1SQMUx2g9BHSGT6Akwh4OcBKSKCEkJS6cgAYEeSTBBPlBkmI_Rnhx4Wv9zPcIQqGfRqGPUYDSMFl-AQM1a6Q)



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

#### L4, vai ter o source port, e o destination port. 
#### L3, vai ter o source IP, e destination IP
#### L2, qual mac address ele tem que entregar (parte mais física)
#### L1, camada mais binaria, quebrar ele em partes e transferir pela fibra ótica. 

#### As mais relevantes são L5, L4 e L3. Pois contem o dados, a porta e o IP de origem e destino.
