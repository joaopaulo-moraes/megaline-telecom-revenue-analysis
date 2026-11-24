# Análise de Receita e Comportamento de Clientes — Megaline

Neste projeto, analisei uma amostra de 500 clientes da operadora de telecomunicações **Megaline** ao longo de 2018 (2.293 registros mensais consolidados entre chamadas, mensagens e tráfego de internet) para responder a uma pergunta comercial: **qual dos dois planos pré-pagos (`Surf` ou `Ultimate`) gera mais receita média e deve receber maior investimento em publicidade?**

## Preparação e Agregação dos Dados

Utilizando **Python**, **Pandas** e **NumPy**, estruturei e limpei as 5 tabelas da operação:

* **Padronização e tipos:** Converti datas (`reg_date`, `churn_date`, `call_date`, `message_date`, `session_date`) para `datetime` e valores monetários para `float`.
* **Regras de tarifação:** Apliquei o arredondamento para cima (`np.ceil`) na duração individual de cada chamada (minutos) e no consumo mensal total de dados (GB), conforme a política de cobrança da operadora.
* **Consolidação mensal:** Cruzei chamadas, minutos, SMS e dados por cliente e mês (`user_id` e `month`), calculando o excedente sobre a franquia de cada plano (`Surf`: US$ 20/mês; `Ultimate`: US$ 70/mês) para obter a receita mensal exata por usuário.

## Principais Resultados

* **Consumo semelhante entre planos:** A duração média das chamadas (entre 300 e 470 min/mês) e o consumo de internet (cerca de 15 a 18 GB/mês no segundo semestre) são bastante próximos nos dois planos, com crescimento gradual ao longo do ano.
* **Receita mais alta e previsível no Ultimate:** Enquanto o plano **Ultimate** mantém uma receita média estável próxima a **US$ 70–74/mês** o ano inteiro, o plano **Surf** começa em **US$ 20/mês** em janeiro e sobe até **US$ 70,11/mês** em dezembro devido às cobranças por excedente (com alta variância entre usuários).
* **Testes de Hipóteses (Teste t de Student, $\alpha = 0,05$):**
  1. **Receita média (`Surf` vs. `Ultimate`):** $p = 9,47 \times 10^{-9}$ — rejeitamos $H_0$, confirmando que há diferença estatisticamente significativa entre a receita média dos dois planos.
  2. **Receita por região (`NY-NJ` vs. demais regiões):** $p = 0,0408$ — rejeitamos $H_0$, indicando diferença estatisticamente significativa na receita média dos clientes da área metropolitana de Nova York/Nova Jersey em relação ao restante do país.

## Arquivos e Ferramentas
* `megaline-telecom-revenue-analysis.ipynb`: Notebook com a limpeza, agregação mensal, gráficos exploratórios e testes estatísticos.
* **Stack:** Python 3, Pandas, NumPy, SciPy (`stats`), Matplotlib e Jupyter Notebook.
