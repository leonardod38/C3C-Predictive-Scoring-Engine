# ⚙️ Motor C3C: Pipeline de Escoragem Preditiva e MLOps (Python + Oracle)

## 📌 Visão Geral
O **Projeto C3C** é uma arquitetura de dados e aprendizado de máquina ponta a ponta. Este motor foi desenvolvido para demonstrar o ciclo de vida completo de um pipeline de dados corporativo, integrando a robustez de bancos de dados **Oracle (PL/SQL)** com a flexibilidade analítica do **Python** e **TensorFlow**. 

Utilizando dados de sorteios de loterias brasileiras (Lotofácil) como dataset numérico, o sistema realiza ETL avançado, engenharia de features, e aplica modelos preditivos para classificar e gerar scores estatísticos em milhares de combinações possíveis.

## 🚀 Arquitetura e Tecnologias
* **Linguagem Principal:** Python 3.x
* **Machine Learning:** TensorFlow, Scikit-Learn
* **Banco de Dados:** Oracle Database (PL/SQL, Table Spaces, Packages)
* **Governança de Dados:** Orquestração de pipelines e versionamento de histórico

## 🧠 Lógica de Processamento (Sniper Layer 4)
O núcleo do processamento iterativo ocorre no módulo **Sniper**, desenhado para filtrar e reter apenas as predições de altíssima probabilidade matemática:
* **Ingestão e Filtragem:** O script `main_layer4_sniper.py` conecta-se diretamente à tabela `TB_LAYER4_SNIPER` no Oracle.
* **Escoragem:** De um pool inicial de **3285 candidatos** gerados e pontuados pelo modelo `.pk1`, o motor seleciona cirurgicamente um limite máximo de **50 registros**.
* **Threshold de Precisão:** Apenas os candidatos com score na faixa otimizada de **21.7699 a 50** avançam no pipeline.
* **Tracking e Auditoria:** A cada ciclo de execução, o sistema limpa o estado atual e salva o histórico completo e consolidado de forma incremental no arquivo `ranking.txt`.
* **Regras de Negócio PL/SQL:** Utilização de loops customizados no banco para validação condicional (ex: regras ativadas caso as dezenas atinjam determinados limites).

## 📁 Estrutura do Repositório
* `/sql`: Scripts DDL/DML, Procedures, e criação da `TB_LAYER4_SNIPER`.
* `/scripts`: Rotinas Python para raspagem e higienização (ETL).
* `/models`: Arquivos dos modelos treinados (versões em `.pk1`) e logs.
* `/core`: Lógica principal (`main_layer4_sniper.py`).

## 💡 Impacto e Casos de Uso
Embora aplicado a um dataset lúdico (Lotofácil), a arquitetura C3C simula perfeitamente problemas corporativos reais, como:
* Escoragem de crédito (Credit Scoring) filtrando os melhores clientes.
* Detecção de anomalias ou fraudes em transações massivas.
* Segmentação de risco para o mercado de seguros.
