# Predição de Rentabilidade em Streaming de Música 🎵 | Projeto DataMaster

Este repositório contém a solução completa para o desafio de predição de rentabilidade (margem líquida), abrangendo desde a ingestão e tratamento de grandes volumes de dados até a modelagem preditiva e análise de eficiência operacional.

---

## 📌 Visão Geral do Projeto
O objetivo deste projeto é prever a **Margem Líquida** do cliente para o mês seguinte. O case utiliza dados de uma plataforma de streaming de música, processando aproximadamente **11 milhões de registros** para extrair padrões de comportamento e consumo que impactam o resultado financeiro.

## 🎯 O Problema de Negócio
A previsibilidade financeira é crucial para a sustentabilidade de serviços de assinatura. Antecipar a rentabilidade permite:
* Identificar perfis de clientes deficitários.
* Otimizar campanhas de marketing baseadas em LTV (Lifetime Value).
* Melhorar a provisão de caixa através de estimativas precisas de margem.

---

## 🏗️ Arquitetura e Pipeline
O projeto foi estruturado em módulos para garantir escalabilidade e organização:

* **01_Functions:** Biblioteca customizada de funções para automação de saneamento e visualização.
* **02_Initial_EDA:** Exploração das bases de transações, logs e usuários, identificando padrões de nulos e integridade das chaves.
* **03_DataPrep & Target:** Definição da *Spine Table* (Safra) e aplicação de **Winsorização (1%/99%)** no target para controle de outliers.
* **04_Final_EDA:** Análise detalhada da relação entre variáveis explicativas e a margem líquida.
* **05_Feature_Engineering:** Criação de *Books* de variáveis temporais (médias/somas de 3 e 6 meses) para capturar a inércia do comportamento do usuário.
* **06_Feature_Selection:** Redução de dimensionalidade via filtros de variância, correlação e V de Cramer (de ~300 para 70 features).
* **07_08_Modelling:** Comparação entre Elastic Net, Random Forest e LightGBM com otimização via HyperOPT.
* **09_Post_Model:** Clusterização de erros e análise de incerteza das predições.

---

## 🚀 Estratégia de Modelagem

### Trade-off e Decisão
Embora modelos lineares (Elastic Net) tenham apresentado performance robusta devido à qualidade da engenharia de features, o **LightGBM** foi selecionado como modelo finalista por:
1.  **Velocidade:** Superioridade em processamento de grandes volumes (11M+ linhas).
2.  **Arquitetura Leaf-wise:** Melhor captura de padrões não-lineares em variáveis de comportamento de uso.
3.  **Estabilidade:** Consistência superior na validação *Out-of-Time* (OOT).

| Modelo | Vantagem Principal | Interpretabilidade |
| :--- | :--- | :--- |
| **Elastic Net** | Baixo custo e Baseline robusto | Máxima (Coeficientes) |
| **Random Forest** | Robustez a outliers (pós-winsor) | Média (Feature Importance) |
| **LightGBM** | **Performance e Eficiência** | **Média (SHAP Values)** |

---

## 🛠️ Tecnologias Utilizadas
* **Linguagens/Processamento:** Python, PySpark, Polars.
* **Machine Learning:** Scikit-Learn, LightGBM, HyperOPT.
* **Tratamento de Dados:** Winsorization, Target Encoding, One-Hot Encoding.
* **Infraestrutura:** Parquet para armazenamento particionado por safra.

---

## 📈 Conclusões e Resultados
* A **Engenharia de Variáveis Temporais** foi o diferencial do projeto, transformando dados transacionais brutos em preditores de comportamento de longo prazo.
* O modelo final demonstrou alta capacidade de distinguir os decis de maior e menor rentabilidade, validando a estratégia de separação de bases In-Time e Out-of-Time.

---

## 👤 Autor
**Gustavo**
*Especialista em Validação de Modelos | Ciência de Dados aplicada a Risco e Finanças.*
