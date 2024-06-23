# 📘 Guia Prático: Rede IPv6 e Containers com Docker

Este guia fornece um passo a passo para criar redes IPv6, construir imagens Docker, criar containers e realizar testes de conectividade.

## 🔧 Criando Rede IPv6

1. **Criar uma rede IPv6:**
    ```bash
    docker network create --ipv6 --subnet=2001:db8:3::/64 network_ipv6
    ```
    > Cria uma rede Docker com suporte a IPv6 usando o intervalo de endereços especificado.

2. **Criar uma rede IPv6 com driver bridge:**
    ```bash
    docker network create --driver bridge --ipv6 --subnet fd00::/64 my_ipv6_network
    ```
    > Cria uma rede IPv6 com o driver `bridge`, permitindo comunicação entre containers no mesmo host.

## 🏗️ Buildando Imagens

1. **Construir a imagem do Squid:**
    ```bash
    docker build -t squidimg .
    ```
    > Cria uma imagem Docker chamada `squidimg` a partir do Dockerfile no diretório atual.

2. **Construir a imagem do SOCKS5:**
    ```bash
    docker build -t socks5-ipv6-ubuntu .
    ```
    > Cria uma imagem Docker chamada `socks5-ipv6-ubuntu`.

## 🐳 Criando Containers IPv6

1. **Criar um container Squid:**
    ```bash
    docker run -d --name squid-container3 --network my_ipv6_network squidimg
    ```
    > Cria e executa um container `squid-container3` na rede `my_ipv6_network` usando a imagem `squidimg`.

2. **Criar um container SOCKS5:**
    ```bash
    docker run -d --name container01 --network my_ipv6_network socks5-ipv6-ubuntu
    ```
    > Cria e executa um container `container01` na rede `my_ipv6_network` usando a imagem `socks5-ipv6-ubuntu`.

3. **Criar outro container SOCKS5:**
    ```bash
    docker run -d --name ctn --network=rede_ipv6 socks5-ipv6-ubuntu
    ```
    > Cria e executa um container `ctn` na rede `rede_ipv6` usando a imagem `socks5-ipv6-ubuntu`.

## 🔍 Capturando Endereço IPv6 do Container

1. **Listar todos os containers:**
    ```bash
    docker ps -a
    ```
    > Lista todos os containers, incluindo os que não estão em execução.

2. **Inspecionar um container:**
    ```bash
    docker inspect idContainer
    ```
    > Exibe todas as informações de infraestrutura do container.

3. **Filtrar endereço IPv6:**
    ```bash
    docker inspect nomeContainer | grep "IPv6Address"
    ```
    > Exibe apenas o endereço IPv6 do container.

4. **Capturar endereço IPv6 diretamente:**
    ```bash
    docker inspect -f '{{range .NetworkSettings.Networks}}{{.GlobalIPv6Address}}{{end}}' idContainer
    ```
    > Captura diretamente o endereço IPv6 do container especificado.

## 📡 Testando Conexão IPv6

1. **Testar conexão com cURL:**
    ```bash
    curl -x [2001:db8:3::3]:3128 https://www.google.com/
    ```
    > Testa a conexão via cURL usando o endereço IPv6 do container.

2. **Ping IPv6:**
    ```bash
    ping6 2001:db8:3::3
    ```
    > Testa a conectividade pingando o endereço IPv6 do container.

## 🔍 Ver Containers

1. **Listar containers em execução:**
    ```bash
    docker ps
    ```
    > Lista todos os containers em execução.

## 🛠️ Acessar Docker Container via SH

1. **Entrar no container:**
    ```bash
    docker exec -it nomeContainer sh
    ```
    > Acessa o terminal do container especificado.

2. **Verificar IPs:**
    ```bash
    ip addr show
    ```
    > Exibe as informações de IP, incluindo IPv6.

3. **Monitorar logs:**
    ```bash
    tail -f /var/log/squid/access.log
    ```
    > Acompanha os logs de acesso do Squid em tempo real.

## 🧰 Comandos Gerais

1. **Ver logs do container:**
    ```bash
    docker logs nomeContainer
    ```
    > Exibe os logs de execução do container especificado.

2. **Verificar portas abertas:**
    ```bash
    docker exec -it nomeContainer netstat -tuln
    ```
    > Verifica se o Squid está escutando na porta 3128 dentro do container.

---

Este documento oferece uma visão clara e objetiva dos comandos e etapas essenciais para configurar e gerenciar redes IPv6 e containers Docker. 🚀 Utilize os emojis para facilitar a navegação pelos tópicos e etapas. Assinado, [AdaUpSoft](https://adaupsoft.com) 🌐
