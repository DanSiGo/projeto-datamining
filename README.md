# 📺 Análise de Preços de Smart TVs: Qual marca possui os preços mais em conta?

**Trabalho Conclusivo da Disciplina:** Data Mining e Web Scraping  
**Linguagem & Ferramentas:** Python, Jupyter Notebook, Pandas, BeautifulSoup, Seaborn, Matplotlib  
**Metodologia:** Micro-tasks modulares e controle de versão via Git  

---

## 🎯 Pergunta de Negócio
> *"Qual marca de Smart TV possui os preços mais em conta no e-commerce brasileiro?"*

### 📌 Resposta Executiva
Com base nos dados coletados e higienizados do e-commerce Buscapé:
* **Marca com Menor Preço Médio:** **Philco**, apresentando um preço médio de **R$ 889,00**.
* **Modelo Individual Mais Barato:** *Smart TV LED 32" Philco PTV32K34RKGB* por **R$ 889,00**.
* **Marcas Premium/Intermediárias:** Samsung, LG e TCL apresentaram maior variação de preços devido à presença de modelos com tecnologias avançadas (QLED, Mini LED e polegadas maiores).

---

## 🏗️ Estrutura do Repositório


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