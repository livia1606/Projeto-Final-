# Classificação de Imagens com Abordagem Clássica: GLCM (Haralick) + Filtros de Gabor

Projeto Final da disciplina de **Processamento de Imagens** – UTFPR-CP (Prof. Claiton de Oliveira)

## Equipe
- Lívia Pontes Argenton (projeto individual)

## Descrição da abordagem
Abordagem **clássica**: extração de características + classificadores tradicionais, executada no **Google Colab (Python)**.

**Pipeline:** leitura → escala de cinza → redimensionamento 224×224 → filtro de mediana 3×3 → CLAHE → extração de características → classificação → avaliação.

### Extração de características (diferentes dos métodos vistos em aula)
Em aula foram vistos SIFT + Bag of Visual Words, HOG, LBP e histogramas de cor. Neste projeto foram usados:

| Descritor | Tipo | Detalhes | Tamanho |
|---|---|---|---|
| **GLCM / Haralick** | Textura (2ª ordem) | imagem quantizada em 32 níveis; distâncias 1, 3 e 5; ângulos 0°, 45°, 90° e 135° (média dos ângulos); contraste, dissimilaridade, homogeneidade, energia, correlação, ASM e entropia | 21 |
| **Banco de filtros de Gabor** | Textura (espaço-frequência) | 4 orientações × 3 comprimentos de onda (4, 8 e 16 px); média, desvio padrão e energia de cada resposta | 36 |

Vetor final (GLCM + Gabor): **57 características** por imagem. Foi feito também um estudo de ablação (cada descritor isolado e combinado).

### Classificadores
- **SVM** (kernel RBF) e **Random Forest**
- Padronização (`StandardScaler`) dentro de um `Pipeline`, para evitar vazamento de dados
- Ajuste de hiperparâmetros com `GridSearchCV` (validação cruzada estratificada de 5 dobras, métrica F1 macro), usando **apenas o conjunto de treino**
- Divisão **holdout 80% treino / 20% teste**, estratificada e com semente fixa (`random_state=42`)

### Métricas
Matriz de confusão, precisão, recall, F1-score, suporte e acurácia, calculados no conjunto de teste.

## Links
- **Repositório (código e vídeo, sem o dataset):** <LINK>
- **Vídeo de apresentação:** <LINK>
- **Dataset utilizado:** <LINK>

## Resultados
Resultados do conjunto de teste da melhor configuração:

| Configuração | Acurácia | Precisão (macro) | Recall (macro) | F1-score (macro) |
|---|---|---|---|---|
| <GLCM + Gabor> + <SVM> | <0.xxxx> | <0.xxxx> | <0.xxxx> | <0.xxxx> |

**Acurácia obtida: <0.xxxx>**

## Instruções de uso
1. Abra `Projeto_Final_Processamento_de_Imagens.ipynb` no Google Colab.
2. Coloque o dataset no Google Drive, com uma subpasta por classe (ex.: `dataset/COVID` e `dataset/Normal`).
3. Na célula de configuração, ajuste `DATASET_DIR` para o caminho da pasta.
4. Execute: *Ambiente de execução → Executar tudo*.

**Bibliotecas:** OpenCV, NumPy, scikit-image, scikit-learn, Matplotlib, Seaborn, Pandas, Joblib.


