# trabalho_cba2026

Detecção de arritmia em sinais de ECG usando **XGBoost + Optuna**, testando 9 cenários de ablação de features pra descobrir o que realmente importa: o sinal bruto, as estatísticas globais, ou os pedacinhos antes/depois do pico R.

## A pergunta central

> O sinal sozinho já basta? As estatísticas ajudam? Combinar tudo é redundante ou é ganho de verdade?

## Os 9 cenários

| # | Conteúdo |
|---|---|
| 1 | Sinal |
| 2 | Estatística global |
| 3 | Global + antes do pico R |
| 4 | Global + depois do pico R |
| 5 | Global + antes + depois |
| 6 | Sinal + global |
| 7 | Sinal + global + antes |
| 8 | Sinal + global + depois |
| 9 | Sinal + global + antes + depois |

Classificação **binária**: `0 = normal`, `1 = anormal (arritmia)`.

## Como foi feito

- Otimização de hiperparâmetros com **Optuna** (50 trials, maximizando o **MCC**)
- **GroupKFold** dentro do Optuna, paralelizado com **Joblib**
- `scale_pos_weight` pra lidar com o desbalanceamento de classes
- Split treino/teste feito **uma única vez** e reaproveitado em todos os cenários (pra ninguém trapacear na comparação 👀)
- Gráficos nativos do Optuna: contorno, importância e histórico de otimização

## Arquivos

- `main.ipynb` — o notebook com toda a mágica (treino, otimização, avaliação)
- `Instruções.txt` — o enunciado original do trabalho
- `resultados_cenarios.xlsx` — métricas (acurácia, sensibilidade, especificidade, precisão, F1, MCC, AUC ROC) por cenário
- `predicoes_detalhadas.parquet` — predições por amostra, com `y_true`, `aami_label` e as probabilidades de cada um dos 9 cenários

## Métricas avaliadas

Acurácia · Sensibilidade · Especificidade · Precisão · F1 Score · MCC · AUC ROC

---

Para o **71º CBA 2026**.
