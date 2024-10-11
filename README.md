# Opção 1
# Sistema de Monitoramento Agrícola

Este projeto visa criar um sistema de banco de dados relacional para monitorar dados coletados por sensores em plantações, possibilitando a otimização da irrigação e aplicação de nutrientes. O sistema processa informações em tempo real, fornece recomendações com base em ajustes anteriores e previsões para o futuro, ajudando a aumentar a produtividade agrícola.

## 1. Informações Relevantes e Dados Necessários

**Exemplo: Previsão de recursos necessários para a próxima safra**

### Informações Relevantes:
O sistema é capaz de prever os recursos necessários (água, fósforo, potássio) para uma safra futura, com base em análises do histórico de dados coletados pelos sensores de umidade, pH, fósforo e potássio, bem como ajustes de irrigação e aplicação de nutrientes anteriores.

### Dados Necessários:
- **Histórico de leituras dos sensores** (umidade, pH, fósforo e potássio) com data e hora de cada leitura.
- **Histórico de ajustes realizados**: dados sobre quantidade de água, fósforo e potássio aplicados em momentos específicos, com base nas recomendações do sistema.
- **Informações sobre a cultura plantada**: nome da cultura, data de plantio e período de crescimento.
- **Informações sobre a fazenda**: localização geográfica e características do solo.

Com esses dados, o sistema pode calcular padrões e sugerir a quantidade de recursos que serão necessários para a safra futura, ajudando a otimizar o uso de insumos agrícolas.

---

## 2. Entidades e Atributos

Para suportar as operações necessárias ao sistema, definimos as seguintes entidades e seus respectivos atributos:

### **Entidade: Sensor**
Esta entidade armazena informações sobre os sensores usados na fazenda.

- `id_sensor` (PK) – Identificador único do sensor. *(tipo: INT)*
- `tipo_sensor` – Tipo do sensor (umidade, pH, nutrientes). *(tipo: VARCHAR)*
- `localizacao` – Localização geográfica do sensor (latitude, longitude). *(tipo: VARCHAR)*

### **Entidade: Leitura**
Armazena as leituras realizadas pelos sensores ao longo do tempo.

- `id_leitura` (PK) – Identificador único da leitura. *(tipo: INT)*
- `id_sensor` (FK) – Identificador do sensor que fez a leitura. *(tipo: INT)*
- `data_hora` – Data e hora da leitura. *(tipo: DATETIME)*
- `valor` – Valor registrado pelo sensor (umidade, pH, fósforo ou potássio). *(tipo: DOUBLE)*

### **Entidade: Cultura**
Representa as diferentes culturas plantadas na fazenda.

- `id_cultura` (PK) – Identificador único da cultura plantada. *(tipo: INT)*
- `nome_cultura` – Nome da cultura (milho, soja, etc.). *(tipo: VARCHAR)*
- `data_plantio` – Data de plantio da cultura. *(tipo: DATE)*

### **Entidade: Ajuste_Aplicacao**
Armazena as informações sobre ajustes de aplicação de água e nutrientes.

- `id_ajuste` (PK) – Identificador único do ajuste. *(tipo: INT)*
- `id_cultura` (FK) – Identificador da cultura associada ao ajuste. *(tipo: INT)*
- `data_hora` – Data e hora do ajuste de aplicação. *(tipo: DATETIME)*
- `quantidade_agua` – Quantidade de água aplicada (litros). *(tipo: DOUBLE)*
- `quantidade_fosforo` – Quantidade de fósforo (P) aplicada (kg). *(tipo: DOUBLE)*
- `quantidade_potassio` – Quantidade de potássio (K) aplicada (kg). *(tipo: DOUBLE)*

### **Entidade: Fazenda**
Armazena informações sobre a fazenda onde os sensores estão instalados.

- `id_fazenda` (PK) – Identificador único da fazenda. *(tipo: INT)*
- `nome_fazenda` – Nome da fazenda. *(tipo: VARCHAR)*
- `localizacao_fazenda` – Localização (endereço, cidade, estado). *(tipo: VARCHAR)*

### **Entidade: Fazenda_Sensor**
Relacionamento entre *Fazenda* e *Sensor*. Armazena a associação de sensores a fazendas.

- `id_fazenda_sensor` (PK) – Identificador único do relacionamento. *(tipo: INT)*
- `id_fazenda` (FK) – Identificador da fazenda. *(tipo: INT)*
- `id_sensor` (FK) – Identificador do sensor. *(tipo: INT)*
- `data_inicio` – Data de início do uso do sensor na fazenda. *(tipo: DATE)*
- `data_fim` – Data de fim do uso do sensor (opcional). *(tipo: DATE)*

---

## 3. Cardinalidade dos Atributos

A cardinalidade dos atributos reflete as relações entre as entidades, conforme segue:

- **Um sensor** pode fazer **muitas leituras** ao longo do tempo (1:N).
- **Uma cultura** pode ter **muitos ajustes de aplicação** (1:N).
- **Uma fazenda** pode ter **muitos sensores**, e **um sensor** pode ser movido entre diferentes fazendas ao longo do tempo (N:N).

---

## 4. Relacionamentos entre as Entidades (MER)

Aqui estão os principais relacionamentos entre as entidades do sistema:

- **Sensor 1:N Leitura**: Um sensor pode realizar muitas leituras ao longo do tempo.
- **Cultura 1:N Ajuste_Aplicacao**: Uma cultura pode estar associada a vários ajustes de irrigação e aplicação de nutrientes.
- **Fazenda N:N Sensor**: Uma fazenda pode ter vários sensores, e um sensor pode ser reutilizado em diferentes fazendas.

---

## 5. Tipos de Dados dos Atributos

Abaixo estão os tipos de dados definidos para cada atributo nas entidades:

| **Entidade**         | **Atributo**            | **Tipo de Dado** |
|----------------------|-------------------------|------------------|
| **Sensor**           | id_sensor               | INT              |
|                      | tipo_sensor             | VARCHAR          |
|                      | localizacao             | VARCHAR          |
| **Leitura**          | id_leitura              | INT              |
|                      | id_sensor               | INT (FK)         |
|                      | data_hora               | DATETIME         |
|                      | valor                   | DOUBLE           |
| **Cultura**          | id_cultura              | INT              |
|                      | nome_cultura            | VARCHAR          |
|                      | data_plantio            | DATE             |
| **Ajuste_Aplicacao** | id_ajuste               | INT              |
|                      | id_cultura              | INT (FK)         |
|                      | data_hora               | DATETIME         |
|                      | quantidade_agua         | DOUBLE           |
|                      | quantidade_fosforo      | DOUBLE           |
|                      | quantidade_potassio     | DOUBLE           |
| **Fazenda**          | id_fazenda              | INT              |
|                      | nome_fazenda            | VARCHAR          |
|                      | localizacao_fazenda     | VARCHAR          |
| **Fazenda_Sensor**   | id_fazenda_sensor       | INT              |
|                      | id_fazenda              | INT (FK)         |
|                      | id_sensor               | INT (FK)         |
|                      | data_inicio             | DATE             |
|                      | data_fim                | DATE             |

---

## Conclusão

Esse modelo foi desenvolvido para suportar o monitoramento contínuo das condições da plantação, realizar ajustes em tempo real e prever os recursos necessários para otimizar a produção. Utilizando um banco de dados relacional, o sistema consegue armazenar e processar grandes quantidades de dados provenientes de sensores, gerando recomendações e previsões valiosas para os produtores rurais.

# Opção 2
# Monitoramento da Saúde do Solo e Microbioma

## 1. Informações Relevantes e Dados Necessários

**Exemplo:** Monitoramento da saúde do solo e seu bioma microbiano para otimização da produção agrícola.

### Informações Relevantes:

O sistema coleta e processa dados sobre a composição do solo e sua microbiota, monitorando aspectos como diversidade de microrganismos, condições de nutrientes e alterações ao longo do tempo. A saúde do solo é fundamental para uma boa produtividade, e a análise da presença de microrganismos benéficos e patogênicos permite ao sistema identificar possíveis intervenções, como a adição de fertilizantes orgânicos ou o manejo de pragas de solo.

### Dados Necessários:

- Leituras de sensores biológicos que coletam dados sobre a diversidade de microrganismos presentes no solo.
- Análises químicas do solo para medir níveis de nutrientes, pH e matéria orgânica.
- Histórico de intervenções no solo, como aplicação de fertilizantes, compostagem ou irrigação.
- Dados climáticos (temperatura, umidade) que influenciam as condições microbiológicas do solo.
- Tipo de cultura plantada e produtividade agrícola, associando os dados do solo com o desempenho da safra.

Esses dados permitem a criação de um panorama detalhado da saúde do solo, e o sistema pode sugerir intervenções para melhorar as condições microbianas, promovendo o equilíbrio do bioma do solo e uma produção mais sustentável.

## 2. Entidades e Atributos

Abaixo estão as entidades necessárias para representar essa solução em um modelo de banco de dados:

### Entidade: Sensor_Solo

Essa entidade armazena informações sobre os sensores utilizados para coletar dados microbiológicos e químicos do solo.

- **id_sensor (PK)** – Identificador único do sensor. (tipo: INT)
- **tipo_sensor** – Tipo do sensor (biológico, químico, de umidade, etc.). (tipo: VARCHAR)
- **localizacao** – Localização do sensor no campo (latitude, longitude). (tipo: VARCHAR)

### Entidade: Leitura_Solo

Armazena os dados coletados pelos sensores de solo, tanto microbiológicos quanto químicos.

- **id_leitura (PK)** – Identificador único da leitura. (tipo: INT)
- **id_sensor (FK)** – Identificador do sensor que coletou a leitura. (tipo: INT)
- **data_hora** – Data e hora da leitura. (tipo: DATETIME)
- **tipo_dado** – Tipo de dado coletado (diversidade microbiana, pH, níveis de nutrientes, etc.). (tipo: VARCHAR)
- **valor** – Valor registrado pelo sensor. (tipo: DOUBLE)

### Entidade: Microorganismo

Essa entidade representa os diferentes microrganismos detectados no solo.

- **id_microorganismo (PK)** – Identificador único do microrganismo. (tipo: INT)
- **nome_microorganismo** – Nome científico do microrganismo. (tipo: VARCHAR)
- **funcao_biologica** – Função que o microrganismo desempenha no solo (ex.: decompositor, fixador de nitrogênio, patógeno). (tipo: VARCHAR)

### Entidade: Cultura

Armazena as informações sobre as culturas plantadas em determinada área de solo.

- **id_cultura (PK)** – Identificador único da cultura plantada. (tipo: INT)
- **nome_cultura** – Nome da cultura (milho, soja, etc.). (tipo: VARCHAR)
- **data_plantio** – Data de plantio da cultura. (tipo: DATE)

### Entidade: Amostra_Solo

Armazena informações sobre amostras de solo coletadas para análises laboratoriais mais detalhadas, como sequenciamento de DNA do solo para estudos microbiológicos.

- **id_amostra (PK)** – Identificador único da amostra. (tipo: INT)
- **id_cultura (FK)** – Identificador da cultura associada. (tipo: INT)
- **data_coleta** – Data da coleta da amostra de solo. (tipo: DATETIME)
- **localizacao** – Localização geográfica da amostra. (tipo: VARCHAR)

### Entidade: Fazenda

Representa as fazendas monitoradas no sistema.

- **id_fazenda (PK)** – Identificador único da fazenda. (tipo: INT)
- **nome_fazenda** – Nome da fazenda. (tipo: VARCHAR)
- **localizacao_fazenda** – Localização da fazenda (endereço, cidade, estado). (tipo: VARCHAR)

## 3. Cardinalidade dos Atributos

A cardinalidade entre as entidades define as relações entre elas:

- Um sensor pode realizar muitas leituras de solo ao longo do tempo (1).
- Uma cultura pode estar associada a muitas amostras de solo (1).
- Uma amostra de solo pode ter muitos microrganismos identificados (1).
- Uma fazenda pode ter muitos sensores e culturas associados (1).

## 4. Relacionamento entre as Entidades (MER)

Aqui estão os principais relacionamentos entre as entidades no Modelo Entidade-Relacionamento (MER):

- **Sensor_Solo 1** → **Leitura_Solo:** Um sensor pode realizar várias leituras ao longo do tempo.
- **Cultura 1** → **Amostra_Solo:** Uma cultura pode ter várias amostras de solo associadas para análise.
- **Amostra_Solo 1** → **Microorganismo:** Uma amostra de solo pode identificar vários microrganismos diferentes.
- **Fazenda 1** → **Cultura:** Uma fazenda pode cultivar diferentes culturas ao longo do tempo.

Esses relacionamentos formam a base para o monitoramento detalhado da saúde do solo e sua microbiota.

## 5. Tipos de Dados a Serem Gravados

Aqui estão os tipos de dados que serão usados para armazenar as informações no banco de dados:

| Entidade        | Atributo                 | Tipo de Dado    |
|-----------------|--------------------------|------------------|
| Sensor_Solo     | id_sensor                | INT              |
|                 | tipo_sensor              | VARCHAR          |
|                 | localizacao              | VARCHAR          |
| Leitura_Solo    | id_leitura               | INT              |
|                 | id_sensor                | INT (FK)        |
|                 | data_hora                | DATETIME         |
|                 | tipo_dado                | VARCHAR          |
|                 | valor                    | DOUBLE           |
| Microorganismo   | id_microorganismo       | INT              |
|                 | nome_microorganismo      | VARCHAR          |
|                 | funcao_biologica        | VARCHAR          |
| Cultura         | id_cultura               | INT              |
|                 | nome_cultura             | VARCHAR          |
|                 | data_plantio            | DATE             |
| Amostra_Solo    | id_amostra               | INT              |
|                 | id_cultura               | INT (FK)        |
|                 | data_coleta              | DATETIME         |
|                 | localizacao              | VARCHAR          |
| Fazenda         | id_fazenda               | INT              |
|                 | nome_fazenda             | VARCHAR          |
|                 | localizacao_fazenda      | VARCHAR          |

## Conclusão

Esse modelo de banco de dados foi desenvolvido para suportar um sistema avançado de monitoramento da saúde do solo com foco em análise microbiológica. A solução permite acompanhar a diversidade e a função dos microrganismos no solo, integrando essas informações com a produtividade agrícola e sugerindo intervenções para manter o equilíbrio do bioma do solo. Este sistema visa promover práticas agrícolas mais sustentáveis e eficientes, contribuindo para a otimização do uso de recursos e a preservação da qualidade do solo ao longo do tempo.

Essa solução é inovadora, pois vai além do monitoramento padrão, incorporando a análise microbiológica do solo e integrando isso com a produtividade agrícola, algo que raramente é abordado em projetos de graduação. O foco na saúde do bioma do solo, em vez de apenas medir parâmetros físicos ou químicos, oferece uma perspectiva holística e sustentável.

