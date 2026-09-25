# 📺 Análise de Preços de Smart TVs: Qual marca possui os preços mais em conta?

**Trabalho Conclusivo da Disciplina:** Data Mining e Web Scraping  
**Linguagem & Ferramentas:** Python, Jupyter Notebook, Pandas, BeautifulSoup, Seaborn, Matplotlib  
**Metodologia:** Micro-tasks modulares, Kanban e controle de versão via Git  

---

## 🎯 Pergunta de Negócio
> *"Qual marca de Smart TV possui os preços mais em conta no e-commerce brasileiro?"*

### 📌 Resposta Executiva
Com base nos dados coletados e higienizados do e-commerce Buscapé:
* **Marca com Menor Preço Médio:** **Philco**, apresentando um preço médio de **R$ 889,00**.
* **Modelo Individual Mais Barato:** *Smart TV LED 32" Philco PTV32K34RKGB* por **R$ 889,00**.
* **Marcas Premium/Intermediárias:** Samsung, LG e TCL apresentaram maior variação de preços devido à presença de modelos com tecnologias avançadas (QLED, Mini LED e telas maiores).

---

## 🏗️ Estrutura do Repositório

```
├── data/
│   ├── dados_brutos.csv        # Dados brutos coletados via Web Scraping (44 registros)
│   └── dados_tratados.csv      # Dados limpos e padronizados para análise (17 registros únicos)
├── notebooks/
│   ├── 01_coleta_dados.ipynb         # Módulo 1: Web Scraping no Buscapé
│   ├── 02_limpeza_tratamento.ipynb   # Módulo 2: Limpeza, RegEx de preços e parsing de marcas
│   └── 03_analise_exploratoria.ipynb # Módulo 3: Agrupamento estatístico e geração de gráficos
├── reports/
│   └── figures/
│       ├── preco_medio_por_marca.png        # Gráfico comparativo de médias
│       └── distribuicao_precos_boxplot.png  # Gráfico de dispersão de preços
└── README.md                   # Relatório executivo do projeto
```

---

## 🔄 Fluxo de Desenvolvimento

### 1. Coleta de Dados (Web Scraping)

* **Pivot Metodológico:** Tentativa inicial no Mercado Livre bloqueada por restrições HTTP 403 (Antibot). Alterado com sucesso para o **Buscapé** (`https://www.buscape.com.br/tv`).
* **Extração:** Utilização das bibliotecas `requests` e `BeautifulSoup` para captura dos cards de produtos e expressões regulares (`re`) para resgatar nomes, preços e lojas.

### 2. Limpeza e Pré-processamento

* Conversão dos valores monetários formatados (`R$ 3.279,00`) para o tipo de dado `float64` (`3279.00`).
* Extração automatizada da marca via busca textual padronizada (Samsung, LG, TCL, Philco, etc.).
* Remoção de inconsistências, registros duplicados e valores nulos.

### 3. Análise Exploratória e Visualização

* Agrupamento por fabricante para cálculo de Média, Mediana, Mínimo, Máximo e Desvio Padrão.
* Exportação dos gráficos comparativos em alta resolução na pasta `reports/figures/`.

---

## 📊 Gráficos Gerados

| Preço Médio por Marca | Distribuição e Dispersão |
| --- | --- |
|  |  |

---

## 🛡️ Aspectos Éticos e Legais

Análise das diretrizes de raspagem responsável adotadas durante o projeto:

* **Acesso Público aos Dados:** Todos os dados extraídos (nome do produto, preço e loja) estavam publicamente acessíveis em páginas de busca do e-commerce Buscapé, sem necessidade de autenticação, login ou quebra de sistemas de proteção.
* **Uso de APIs como Alternativa:** Tentou-se utilizar a API pública do Mercado Livre no início do projeto, contudo, enfrentaram-se restrições de acesso (HTTP Status 403). A raspagem HTML no Buscapé foi adotada como alternativa viável para fins acadêmicos.
* **Privacidade e Dados Pessoais:** Nenhum dado pessoal identificável (PII) de usuários, compradores ou vendedores foi coletado. A raspagem foi estritamente limitada a dados operacionais de produtos e preços.
* **Impacto no Servidor:** A requisição foi realizada de forma pontual e com volume reduzido (apenas 1 página/requisição), gerando consumo insignificante de largura de banda do servidor de origem.

### 💡 3 Boas Práticas para Coleta Responsável em Empresas:

1. **Respeito ao `robots.txt` e Rate Limiting:** Implementar intervalos de pausa (*delays*) entre as requisições para evitar sobrecarga nos servidores de origem.
2. **Identificação Transparente do User-Agent:** Configurar o cabeçalho HTTP com informações claras e de contato dos responsáveis pela coleta.
3. **Priorização de APIs Oficiais e Cache Local:** Dar preferência a integrações via APIs autenticadas e armazenar cópias locais (*cache*) para evitar requisições redundantes ao mesmo recurso.

---

## ⚙️ Proposta de Automação do Pipeline

Para que este processo funcione de forma contínua em um ambiente corporativo, propõe-se a orquestração diária do pipeline de dados:

```
    A[🌐 Internet / E-commerce Buscapé] -->|1. Coleta Diária às 8h| B[🐍 Script Web Scraping: requests + BeautifulSoup]
    B -->|2. Exportação| C[📁 Data Lake / S3: data/dados_brutos.csv]
    C -->|3. Disparo da Limpeza| D[🧹 Script de Pré-processamento: Pandas + RegEx]
    D -->|4. Persistência| E[🗄️ Banco de Dados / S3: data/dados_tratados.csv]
    E -->|5. Atualização de Métricas| F[📊 Script EDA & Estatísticas]
    F -->|6. Renderização| G[📈 Dashboard / Relatório Executivo]

```

### 🔁 Fluxo Operacional

* **Agendamento (Cronjob / Apache Airflow):** Disparo diário e automático às 08:00 AM para capturar oscilações de preços do varejo.
* **Monitoramento e Alertas:** Envio automático de notificações via Slack/Email em caso de falhas de conexão (erros HTTP 4xx/5xx) ou inconsistência nos esquemas dos dados (*Data Quality*).

---

## 🎯 Conclusões e Insights Baseados em Dados

### 📌 Resposta à Pergunta de Negócio

A marca **Philco** apresentou os preços mais em conta no ecossistema analisado, registrando o **menor preço médio (R$ 889,00)** e comercializando o **modelo de TV mais barato da amostra (Smart TV LED 32" Philco PTV32K34RKGB por R$ 889,00)**.

### 💡 3 Insights Extraídos da Análise Quantitativa:

1. **Dominância da Philco no Segmento de Entrada (32"):** A Philco concentra sua oferta em modelos HD/Full HD de porte menor (32 polegadas), o que reduz drasticamente sua média de preços em comparação a marcas focadas em telas maiores.
2. **Amplitude e Dispersão de Preços na TCL:** A TCL apresentou uma amplitude de preços expressiva, variando de modelos de entrada FHD (R$ 2.069,10) até Smart TVs premium Mini LED de 75" (atingindo R$ 5.859,73), demonstrando uma estratégia de portfólio altamente diversificada.
3. **Concentração de Marcas Premium em Tecnologias Superiores:** Marcas como Samsung e LG apresentaram preços médios elevados devido à forte presença de modelos 4K, OLED e QLED no topo dos resultados de busca.