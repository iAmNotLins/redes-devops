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

### HTTP Message

#### Atua diretamente com a aplicação, é a camada que mais utilizamos. 

### Fundamentos 

#### 1- Usado para comunicação web
#### 2- Usado também no backend, para construção de API, aonde os dados podem ser consumidos através de uma requisição HTTP. 
### Como é feito uma requisição HHTP?
#### Requisição GET: É um método http para busca de dados
#### Requisição POST:Enviar dados
#### Requisição PUT: Usado em upload de algo (imagem, video)
#### Requisição PATCH: Aplica modificações parciais a um recurso.
#### Requisição DELETE: Remove um recurso.
#### Requisição HEAD: Solicita apenas os cabeçalhos de uma resposta.
#### Requisição OPTIONS: Descreve as opções de comunicação para o recurso de destino

### URI: Exemplo - closedcircle.com.br/seal-project, a URI é o que vem depois do /
#### Baseado nos seu Headers é o que vão saber o que fazer com a requisição.

| Campo HTTP | Valor |
| :--- | :--- |
| **Host** | `mateusmuller.me` |
| **Connection** | `close` |
| **User-agent** | `Mozilla` |
| **Accept-language** | `br` |


### HTTP Response

| Campo | Valor |
| :--- | :--- |
| **Status** | `HTTP/1.1 200 OK` |
| **Connection** | `close` |
| **Date** | `Tue, 2 Nov 2020 20:36 GMT` |
| **Server** | `Apache/2.2.3 (CentOS)` |
| **Last-Modified** | `Tue, 2 Nov 2020 19:47 GMT` |
| **Content-Length** | `6821` |
| **Content-Type** | `Text/html` |
| **Body** | `(data data data ...)` |


| Código | Status (Nome) | Categoria | Significado Rápido |
| :---: | :--- | :---: | :--- |
| **200** | `OK` | ✅ Sucesso | A requisição funcionou perfeitamente. |
| **201** | `Created` | ✅ Sucesso | Sucesso e algo foi criado (comum em POST). |
| **204** | `No Content` | ✅ Sucesso | Sucesso, mas não há nada para retornar. |
| **301** | `Moved Permanently` | 🔄 Redirecionamento | A página mudou de endereço para sempre. |
| **302** | `Found` | 🔄 Redirecionamento | A página mudou de endereço temporariamente. |
| **304** | `Not Modified` | 🔄 Cache | Conteúdo não mudou, usa-se o cache. |
| **400** | `Bad Request` | ⚠️ Erro Cliente | Requisição inválida ou mal formatada. |
| **401** | `Unauthorized` | ⚠️ Erro Cliente | Falta autenticação (Login). |
| **403** | `Forbidden` | ⚠️ Erro Cliente | Sem permissão de acesso. |
| **404** | `Not Found` | ⚠️ Erro Cliente | Recurso não encontrado. |
| **429** | `Too Many Requests` | ⚠️ Erro Cliente | Muitas requisições (Rate Limit). |
| **500** | `Internal Server Error`| 🚨 Erro Servidor | Erro genérico no servidor. |
| **502** | `Bad Gateway` | 🚨 Erro Servidor | Erro de comunicação entre servidores/proxy. |
| **503** | `Service Unavailable` | 🚨 Erro Servidor | Servidor caiu ou está cheio. |
| **504** | `Gateway Timeout` | 🚨 Erro Servidor | Tempo limite esgotado. |

# HTTP Persistente vs. Não Persistente

### 1. HTTP Não Persistente (Non-Persistent)
**Como funciona:**
Para cada arquivo (HTML, imagem, script), uma **nova conexão TCP** é estabelecida. O arquivo é transferido e a conexão é imediatamente fechada.

* **Processo:**
    1. Cliente pede a URL.
    2. Estabelece conexão TCP (1 RTT).
    3. Cliente pede o objeto (Ex: HTML).
    4. Servidor envia o objeto (1 RTT para request/response).
    5. **Conexão TCP é fechada.**
    6. *Repete-se tudo para cada imagem/CSS/JS (2 RTTs + tempo de transmissão por objeto).*

* **🔴 Desvantagens:**
    * Alto custo de tempo (overhead).
    * Consumo excessivo de recursos do servidor para abrir e fechar conexões repetidamente.

---

### 2. HTTP Persistente (Persistent)
**Como funciona:**
Uma **única conexão TCP** é mantida aberta pelo servidor para que o cliente possa solicitar vários objetos através dela, sem precisar reestabelecer a conexão a cada vez.

* **Processo:**
    1. Cliente pede a URL e estabelece conexão TCP.
    2. Cliente pede objetos (HTML, imagens, etc.) pela **mesma conexão**.
    3. Servidor envia os objetos.
    4. A conexão permanece aberta para futuras requisições ou é fechada após um tempo limite (*timeout*).

* **🟢 Vantagens:**
    * **Menos Latência:** Elimina o tempo de *handshake* TCP para cada objeto.
    * **Economia de Recursos:** Menos sobrecarga no processador do servidor e do cliente.
    * **Mais Rápido:** Permite o carregamento de páginas web complexas de forma muito mais eficiente.

* **⚙️ Implementação:**
    * É o padrão no **HTTP/1.1** e superiores.
    * Usa cabeçalhos como `Connection: Keep-Alive` (ou assume isso por padrão).

---

### 📊 Resumo das Diferenças

| Característica | HTTP Não Persistente | HTTP Persistente |
| :--- | :--- | :--- |
| **Conexão** | Uma conexão por objeto (fechada após cada). | Uma conexão para múltiplos objetos (reutilizada). |
| **Eficiência** | Baixa (muito overhead). | Alta (pouco overhead). |
| **Versão HTTP** | Padrão no HTTP/1.0. | Padrão no HTTP/1.1 e superiores. |
| **Custo (RTT)** | Alto (2 RTTs por objeto). | Baixo (1 RTT para vários objetos após conexão). |

## 📄 Arquivo HAR (HTTP Archive)
O **HAR** é um arquivo JSON gerado pelo navegador que registra todas as requisições e respostas feitas durante o carregamento de uma página. É um "raio-x" do tráfego.

### Para que serve
- **Diagnóstico:** Identificação de lentidão, erros de carregamento e falhas em APIs.
- **Análise de Performance:** Visualização do tempo de cada requisição (*waterfall*), tamanho dos arquivos e ordem de carregamento.
- **Depuração Técnica:** Permite ver headers, payloads e cookies trocados entre cliente e servidor.
- **Auditoria:** Verificação de segurança e códigos de status.

---

## 🍪 Cookie
Um pequeno arquivo de texto que o servidor solicita que o navegador armazene para manter informações de estado (stateful).

### Como funciona
1. **Envio:** O servidor envia o cookie no cabeçalho de resposta (`Set-Cookie`) ao navegador.
2. **Armazenamento:** O navegador salva o arquivo localmente.
3. **Retorno:** Em toda nova requisição para aquele domínio, o navegador envia o cookie de volta automaticamente.

### Para que serve
- **Sessão:** Manter o usuário logado entre páginas.
- **Preferências:** Salvar configurações como tema (dark/light) ou idioma.
- **Tracking:** Monitoramento para analytics e anúncios personalizados.

---

## 🛡️ Proxy
Um servidor intermediário que atua como uma "ponte" entre o dispositivo do usuário (cliente) e a internet (servidor de destino).

### Como funciona
1. O cliente faz uma requisição.
2. O tráfego passa pelo **Proxy** antes de ir para a internet.
3. O Proxy analisa, filtra ou modifica a requisição e a envia ao destino.
4. A resposta volta para o Proxy, que a entrega ao cliente.

### Para que serve
- **Privacidade:** Oculta o endereço IP real do usuário.
- **Segurança:** Bloqueia sites maliciosos e aplica filtros de conteúdo.
- **Controle:** Usado por empresas para restringir acessos na rede corporativa.
- **Acesso:** Permite contornar bloqueios geográficos.

---

## ⚡ Proxy Cache
Um tipo específico de proxy focado em otimização de performance, armazenando cópias de recursos estáticos.

### Como funciona
- **Cache HIT:** O conteúdo solicitado já está salvo no proxy → Entrega imediata (sem ir ao servidor original).
- **Cache MISS:** O conteúdo não está salvo → O proxy busca no servidor original, entrega ao usuário e salva uma cópia.

### Para que serve
- **Velocidade:** Reduz drasticamente o tempo de carregamento para o usuário final.
- **Economia de Banda:** Evita o download repetido de arquivos grandes.
- **Redução de Carga (Load):** Diminui o número de requisições que chegam ao servidor de aplicação (backend).
- **Estabilidade:** Pode servir conteúdo em cache mesmo se o servidor de origem estiver instável.

  # Relembrando: Métodos HTTP

* **GET:** Busca de dados
* **POST:** Inserção de dados

## Curl

### Comandos para GET

Comandos comuns no curl:

```bash
curl URL -I
curl URL -Iv
curl URL -L
curl URL -LI

# Salva a resposta em um arquivo com o mesmo nome do arquivo remoto
curl -O URL 

# Salva a resposta em um arquivo com um nome específico
curl -o nome_arquivo.html URL 

# Realiza a requisição ignorando verificação de certificado SSL (inseguro, usado em dev)
curl -k URL

curl -d '{
  "name": "Leonardo",
  "last_name": "Vidal",
  "cpf": "516.925.785-41",
  "email": "example@teste",
  "birth_data": "1996-10-29"
}' -X POST -H "content-type: application/json" localhost:5000/register

curl -d @arquivo.json -X POST -H "content-type: application/json" localhost:5000/register
