# Apache Pulsar

## Introdução

O Apache Pulsar foi desenvolvido pela Yahoo em 2013 como uma solução interna para lidar com os desafios de escalabilidade e desempenho de suas plataformas, que exigiam processamento massivo de dados em tempo real. A Yahoo precisava de uma solução que unificasse as capacidades de streaming e message queuing, pois suas arquiteturas dependiam de dois sistemas diferentes para essas funcionalidades. O Pulsar foi criado para suportar essas necessidades de forma eficiente, integrando os melhores aspectos de sistemas como Apache Kafka e RabbitMQ, mas superando suas limitações em termos de escalabilidade, latência e tolerância a falhas.

Em 2016, a Yahoo decidiu compartilhar essa tecnologia com a comunidade open source, doando o projeto para a Apache Software Foundation, onde ele se tornou um projeto de alto nível. Desde então, o Pulsar tem evoluído rapidamente, ganhando a confiança de grandes empresas e comunidades de desenvolvedores por sua arquitetura flexível e alta performance.

## Principais motivações para o desenvolvimento do Pulsar

- **Alta Escalabilidade**: A Yahoo operava em uma escala massiva, e sistemas existentes como o Kafka apresentavam limitações de escalabilidade. O Pulsar foi desenvolvido para escalar horizontalmente, permitindo a adição de novos nós e partições sem degradação de desempenho.

- **Replicação Global**: A Yahoo precisava de um sistema que suportasse a replicação eficiente de dados entre diferentes data centers ao redor do mundo. O Pulsar foi projetado com replicação geográfica nativa, permitindo a transmissão de mensagens entre regiões de forma eficiente.

- **Baixa Latência e Alto Throughput**: Para plataformas como Yahoo Finance e Yahoo Mail, era necessário processar dados em tempo real com baixíssima latência. O Pulsar foi otimizado para fornecer latência na casa dos milissegundos e alto throughput.

- **Multi-tenancy**: O Pulsar oferece suporte nativo para multi-tenancy, permitindo que diferentes equipes ou aplicações compartilhem a mesma infraestrutura de mensagens com isolamento seguro entre os dados.

## Vantagens chave no design do Pulsar

- **Separação entre Computação e Armazenamento**: O Pulsar adota uma arquitetura modular, onde a camada de computação (brokers) é separada da camada de armazenamento (usando o Apache BookKeeper para persistência).

- **Persistência de Dados**: O Pulsar utiliza o Apache BookKeeper para gerenciar logs distribuídos, garantindo que os dados sejam armazenados de maneira confiável e distribuída.

- **Suporte a Mensagens de Longa Retenção**: O Pulsar foi projetado para suportar retenção de dados de longo prazo, com políticas de armazenamento configuráveis.

## Arquitetura

A arquitetura do Apache Pulsar é composta por três componentes principais:

1. **Brokers**: Responsáveis por receber e entregar mensagens aos consumidores, atuando como intermediários entre produtores e consumidores.

2. **BookKeeper**: Sistema de armazenamento distribuído usado para o armazenamento persistente das mensagens.

3. **Zookeeper**: Serviço de coordenação e gerenciamento de metadados, garantindo que a infraestrutura esteja sincronizada.

## Principais Características

1. **Modelo de Tópicos Multinível**: O Pulsar utiliza um modelo de publicação/assinatura com suporte a tópicos multinível, incluindo assinaturas `Exclusive`, `Shared` e `Failover`.

2. **Particionamento e Replicação**: O Pulsar distribui tópicos em várias partições e oferece replicação geográfica para garantir alta disponibilidade global.

3. **Persistência e Assinaturas Duráveis**: O Pulsar garante a persistência de dados e oferece políticas de retenção e entrega de mensagens configuráveis.

4. **Separação de Camadas de Computação e Armazenamento**: Permite escalar a computação e o armazenamento de forma independente.

5. **Multitenancy**: Suporte a multi-inquilinos, ideal para organizações que precisam isolar fluxos de mensagens.

6. **Baixa Latência e Alta Taxa de Transferência**: Oferece baixa latência no envio e recebimento de mensagens, com alta taxa de transferência.

7. **API Simples e Suporte a Várias Linguagens**: O Pulsar oferece APIs em várias linguagens como Java, Python, C++, Go, entre outros.

## Comparação com o Kafka

- **Arquitetura**: O Pulsar separa as camadas de armazenamento e computação, enquanto o Kafka combina ambas.
- **Consistência e Durabilidade**: O Pulsar utiliza replicação síncrona, garantindo maior consistência.
- **Performance em Latência**: O Pulsar é conhecido por sua baixa latência em comparação com o Kafka.

## Projeto
### Descrição
- O reposiótio consiste em dois projetos em python:
- **producer.py**: Emite mensagens para o consumidor.
- **consumer.py**: Recebe as mensagens do emissor.
### Download
- Com o Git instalado, criar um diretório, abrir o terminal e colar o seguinte comando:
```bash
# Inicializa um novo repositório Git
git clone https://github.com/SabrinaCoelho/Apache_pulsar_python_demonstration.git
```
### Apache Pulsar no Docker
- **Execução**: Com o Docker Desktop instalado na máquina, execute o comando:
```bash
# Inicializa um container com uma imagem do Pulsar
docker run -it -p 6650:6650  -p 8080:8080 --mount source=pulsardata,target=/pulsar/data --mount source=pulsarconf,target=/pulsar/conf apachepulsar/pulsar:3.3.1 bin/pulsar standalone
```
- **Execução**: Abrir o terminal no diretótio do projeto e colar o comando abaixo que instala a biblioteca cliente do Pulsar Python diretamente do PyPI
```bash
pip install pulsar-client
```
- **Execução**: Abrir o diretório com o repositório baixado e em terminais diferentes, execute os comandos:
```bash
# Inicializa o consumer.py
python consumer.py
# Inicializa o producer.py
python producer.py
```
- **Mensagens consumidas**: Podemos utilizar o comando abaixo para verificar as estatísticas do tópico específico. Na propriedade "msgInCounter" contém o número de mensagens que passaram pelo broker.
```bash
vcurl http://localhost:8080/admin/v2/persistent/public/default/my-topic/stats | python -m json.tool
```

## Conclusão

O Apache Pulsar é uma solução madura e altamente escalável para empresas que buscam uma plataforma confiável de mensagens e streaming em tempo real. Ele é eficaz em ambientes que exigem resiliência, alta disponibilidade e processamento de dados distribuído, sendo ideal para aplicações financeiras, monitoramento de redes e soluções IoT.

