# Sistema Distribuído P2P na Cloud (Chord, Bully e Replicação)

**Estado:** Concluído (Projeto Acadêmico - Sistemas Distribuídos)
**Tecnologias:** Python, gRPC, Protocol Buffers, Google Cloud Platform (GCP)

> **Nota de Integridade Acadêmica:** O código-fonte original deste projeto encontra-se em um repositório privado no GitLab institucional para respeitar as políticas da universidade. Este repositório funciona como uma vitrine técnica, contendo o relatório da arquitetura, resultados de testes e a demonstração do sistema em funcionamento.

## O Desafio
O objetivo central consistiu na concepção e implementação de uma arquitetura de Sistemas Distribuídos focada na escalabilidade, eficiência e alta disponibilidade. Para simular a latência e os desafios de uma rede global real, o sistema foi implementado na Google Cloud Platform (GCP) através de 4 Máquinas Virtuais (VMs) distribuídas por diferentes regiões geográficas globais (Ásia, Europa e EUA).

## Arquitetura e Algoritmos Implementados

A comunicação entre os nós da rede é realizada de forma assíncrona utilizando **gRPC** e **Protocol Buffers**. A arquitetura baseia-se na integração profunda dos seguintes algoritmos clássicos de sistemas distribuídos:

### 1. Encaminhamento P2P com Chord (DHT)
* Implementação de uma Tabela de Hash Distribuída (DHT) com topologia em anel.
* Otimização da pesquisa de chaves com *Finger Tables*, garantindo uma complexidade logarítmica $O(\log n)$ nas operações de *Lookup*.
* Manutenção autônoma da integridade do anel perante a entrada e saída de nós (*Peer Churn*).

### 2. Tolerância a Falhas (Primary-Backup Replication)
* Para assegurar a durabilidade dos dados em caso de falha de um nó, as chaves são automaticamente replicadas no sucessor imediato no anel.
* Redirecionamento dinâmico de pedidos de leitura (*Get*) para os nós de backup em caso de indisponibilidade do nó primário.

### 3. Eleição de Líder (Algoritmo Bully)
* Implementação de um protocolo de coordenação descentralizada.
* Detecção automática de falhas do nó líder (via *HealthChecks*) e desencadeamento de um processo de eleição simultâneo, garantindo que o nó ativo com maior ID assuma o controle da rede de forma imediata.

### 4. Consenso Distribuído
* Protocolo de votação gerido pelo líder para manter a consistência de estado compartilhado (variável global) entre todos os nós da rede.
* Execução paralela da coleta de votos e disseminação de resultados, evitando qualquer dessincronização dos estados locais.

---
*Desenvolvido em dupla por Guilherme Ferreira e Kairé Giovanetti (2025)*
