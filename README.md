# Previsão de Procura no Retalho: Walmart M5

> Comparação de modelos estatísticos, de Machine Learning, de Deep Learning e foundation models na previsão a 28 dias de 216 produtos da Walmart.

**Mestrado em Business Intelligence & Analytics (ISCAP)**, 2025/26

## O problema
Prever as vendas diárias de **216 produtos** (departamento FOODS_1, loja TX_1, Texas) com um horizonte de **28 dias**, igual ao da competição M5. Todos os modelos usam a mesma divisão cronológica e a mesma métrica principal, o **RMSSE**, para a comparação ser justa.

## Fases
| Fase | Notebook | Modelos |
|---|---|---|
| 1. Estatísticos | `01a`, `01b`, `01c` | Naive, Seasonal Naive, Historic Average, AutoETS, AutoARIMA, AutoARIMAX |
| 2. Machine Learning | `02` | Linear/Ridge, Random Forest, Extra Trees, XGBoost, LightGBM (multivariados e univariados) |
| 3. Deep Learning e foundation models | `03` | NHITS, LSTM, AutoNHITS, AutoLSTM, Chronos (Amazon), TimeGPT (Nixtla), AutoGluon |

## Resultados (validação, RMSSE: quanto menor, melhor)
| Modelo | Família | RMSSE |
|---|---|---|
| **AutoARIMAX** | Estatístico | **0,744** |
| AutoETS | Estatístico | 0,746 |
| TimeGPT (univariado) | Foundation model | 0,747 |
| XGBoost (univariado) | Machine Learning | 0,750 |
| Seasonal Naive | Baseline | 0,956 |

**Conclusão:** um modelo estatístico bem especificado (AutoARIMAX, com variáveis exógenas) bateu modelos muito mais complexos. Em séries de retalho intermitentes, a complexidade nem sempre compensa. A tabela completa está em `results/final_results.csv`.

## Stack
`statsforecast` · `mlforecast` · `scikit-learn` · `XGBoost` · `LightGBM` · `neuralforecast` · `Chronos` · `TimeGPT` · `AutoGluon` · `PyTorch`

## Como correr
Os notebooks foram feitos no Google Colab, com os dados no Google Drive.
1. Descarrega os dados da [competição M5 no Kaggle](https://www.kaggle.com/competitions/m5-forecasting-accuracy).
2. Ajusta o caminho do Drive na secção de configuração de cada notebook.
3. O TimeGPT precisa de uma chave da Nixtla, definida na variável de ambiente `NIXTLA_API_KEY` e nunca escrita no código. Esse bloco pode ser desligado nas *Execution Flags*.

## Autores
Beatriz Teixeira · João Coelho
