# Avaliação de modelos de Machine Learning na Detecção de Ataques GNSS (Spoofing & Jamming) em VANTs

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Scikit-Learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![USP](https://img.shields.io/badge/ICMC-USP-0055A5?style=for-the-badge)](https://www.icmc.usp.br/)

Este repositório contém uma investigação avançada sobre a aplicação de algoritmos de **Machine Learning** na identificação de interferências maliciosas e ataques de cibersegurança em **Veículos Aéreos Não Tripulados (VANTs / Drones)**. 

Trata-se de uma expansão de estudos anteriores sobre a segurança de sistemas aéreos, incorporando agora a classificação multiclasse não apenas de múltiplos níveis de **Spoofing de GPS**, mas também de cenários de **Jamming**. O projeto se trata principalmente da tentativa de replicação de um artigo científico publicado no SBSeg 2024.

---

## Contexto & Base de Dados

Os dados utilizados neste estudo têm como base o trabalho dos pesquisadores **Gustavo Gualberto Rocha de Lemos** e **Rodrigo Augusto Cardoso da Silva**. A coleta foi realizada a partir de um **receptor GNSS de 8 canais** embarcado em drones reais.

O dataset é composto por **13 features técnicas** extraídas continuamente nos 8 canais paralelos de satélites visíveis.

### Classes de Sinais Analisadas
1. **Sinal Autêntico:** Operação normal do receptor GNSS.
2. **Spoofing Simplista:** Injeção de sinais sem alinhamento fino de fase/frequência.
3. **Spoofing Intermediário:** Falsificação com sincronização parcial de parâmetros.
4. **Spoofing Sofisticado:** Falsificação coordenada de alta precisão.
5. **Jamming:** Interferência intencional por ruído/potência para bloqueio do canal.

---

## Features do Dataset

| Feature | Descrição Técnica | Unidade |
| :--- | :--- | :---: |
| **`PRN`** | *Pseudo-Random Noise:* Identificador único do satélite | ID |
| **`DO`** | *Carrier Doppler:* Deslocamento Doppler da portadora | Hz |
| **`PD`** | *Pseudorange:* Pseudodistância estimada até o satélite | m |
| **`RX`** | Tempo de recepção registrado pelo receptor | s |
| **`TOW`** | *Time of Week:* Tempo decorrido desde o início da semana GPS | s |
| **`CP`** | *Carrier Phase Cycles:* Diferença de fase da portadora (ciclos) | ciclos |
| **`EC`** | *Early Correlator:* Saída do correlator antecipado ($\frac{1}{2}$ chip) | - |
| **`LC`** | *Late Correlator:* Saída do correlator atrasado ($\frac{1}{2}$ chip) | - |
| **`PC`** | *Prompt Correlator:* Medida de correlação do sinal recebido | - |
| **`PIP`** | *Prompt In-Phase Component:* Componente em fase ($I$) do correlator | - |
| **`PQP`** | *Prompt Quadrature Component:* Componente em quadratura ($Q$) do correlator | - |
| **`TCD`** | *Tracking Carrier Doppler:* Doppler estimado pelos loops de rastreio | Hz |
| **`CN0`** | *Carrier-to-Noise Ratio:* Relação sinal-ruído da portadora | dB-Hz |

---

## Metodologia & Pipeline

O fluxo de trabalho foi desenhado para respeitar as restrições físicas de séries temporais embarcadas em hardware de drones:

1. **Análise Exploratória & Estatística:** Avaliação da distribuição de sinais e verificação de dependências lineares/não-lineares via **Matriz de Correlação de Spearman**.
2. **Pré-processamento Consciente:** Tratamento de tipos de dados, formatação decimal e validação de consistência sem perda de dinâmica de temporalidade.
3. **Engenharia de Features:** Extração de métricas derivativas para capturar inconsistências físicas (ex: discrepâncias entre Doppler e TCD).
4. **Modelagem Multiclasse:** Treinamento de modelos de classificação ensemble e baseados em árvores/kernels otimizados para detecção com baixo tempo de inferência.

---

## Tecnologias & Bibliotecas

- **Linguagem:** Python 3.x
- **Manipulação de Dados:** `pandas`, `numpy`
- **Visualização de Dados:** `matplotlib`, `seaborn`
- **Machine Learning & Validação:** `scikit-learn`

---

## ✒️ Autor

Desenvolvido por **Luís Henrique Varela Medeiros Bezerra**  
* Bacharelado em Ciência de Computação (BCC) — **ICMC / USP**  
* GitHub: [@luishvarela](https://github.com/luishvarela)
