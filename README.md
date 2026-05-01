# Trabalho CBA 2026 — Classificação de ECG

Projeto desenvolvido para o CBA 2026. O objetivo é classificar sinais de ECG como **normal ou anormal (arritmia)** usando XGBoost, testando diferentes combinações de features pra ver o que realmente faz diferença no resultado.

---

## O que o projeto faz

Roda 9 cenários de ablação, variando as features usadas pelo modelo:

| Cenário | Features |
|---------|----------|
| 1 | Sinal bruto |
| 2 | Estatísticas globais |
| 3 | Estatísticas globais + antes do pico R |
| 4 | Estatísticas globais + depois do pico R |
| 5 | Estatísticas globais + antes + depois |
| 6 | Sinal + estatísticas globais |
| 7 | Sinal + estatísticas globais + antes |
| 8 | Sinal + estatísticas globais + depois |
| 9 | Sinal + estatísticas globais + antes + depois |

A ideia é entender o que cada bloco de features contribui e se tem algum que não vale a pena incluir.

---

## Como funciona

- **Modelo:** XGBoost
- **Otimização:** Optuna (50 trials, maximizando o MCC)
- **Validação:** GroupKFold com processamento paralelo (Joblib)
- O split treino/teste é feito **uma única vez** e reaproveitado em todos os cenários pra garantir comparação justa

---

## Arquivos

- `main.ipynb` — notebook com todo o código
- `resultados_cenarios.xlsx` — métricas de cada cenário (acurácia, F1, MCC, AUC ROC...)
- `predicoes_detalhadas.parquet` — predições por amostra, com probabilidades de cada cenário
- `Instruções.txt` — especificação completa do experimento

---

## Como rodar

```bash
git clone https://github.com/RenanCatini/trabalho_cba2026.git
cd trabalho_cba2026
pip install xgboost optuna joblib scikit-learn pandas numpy pyarrow openpyxl
jupyter notebook main.ipynb
```

---

**Autor:** Renan Catini
