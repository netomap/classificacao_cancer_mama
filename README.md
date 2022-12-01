O notebook é de aprendizado na construção de uma rede neural, utilizando Pytorch, para um problema de classificação de presença de câncer benigno ou maligno através de imagens de ultrasom de mama.

## Fonte do dataset
https://data.mendeley.com/datasets/wmy84gzngw/1  
[Rodrigues, Paulo Sergio (2017), “Breast Ultrasound Image”, Mendeley Data, V1, doi: 10.17632/wmy84gzngw.1]  

## Descrição do projeto
- Criar uma rede neural profunda, utilizando [Pytorch](https://pytorch.org/), para classificar as imagens em câncer maligno ou benigno.  
- Foi definido um diconário das classes, tando tipo para índice quanto índice para tipo:
```
CANCERTYPE2IDX = {'benign': 0,'malignant': 1}
IDX2CANCERTYPE = {0: 'benign',1: 'malignant'}
```
- Também foi feita uma rápida análise exploratória do shape das imagens. Foi decidido redimensioná-las todas para **(wxh) = (100x100)**.  
- Também, foi criada a classe dataset e implementada a técnica de **[data augmentation]**(https://pytorch.org/vision/main/transforms.html), uma vez que o dataset é bem reduzido (possui somente 250 imagens).  

## Treinamento
- Para o treinamento foram utilizadas algumas as métricas de validação, como [acurácia](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.accuracy_score.html), [precisão](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.precision_score.html), [recall](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.recall_score.html)
- Também foram adotados outros hiperparâmetros do treinamento, que são:
```
BATCH_SIZE = 4
LEARNING_RATE = 2e-4
EPOCHS = 30
INPUT_SIZE = 100 # Tamanho que as imagens vão ser redimensionadas
THRESHOLD = 0.5

loss_fn = nn.BCELoss()
optimizer = torch.optim.Adam(params=model.parameters(), lr = LEARNING_RATE)
scheduler = torch.optim.lr_scheduler.StepLR(optimizer, step_size=10, gamma=0.6)
```
- Função Perda: [BCELoss](https://pytorch.org/docs/stable/generated/torch.nn.BCELoss.html)

# Resultados
- O treinamento teve um resultado satisfatório:  
![resultado](https://github.com/netomap/classificacao_cancer_mama/blob/main/resultado-metricas.png)

- E a rede treinada fez inferências em 25 imagens:  
![resultado](https://github.com/netomap/classificacao_cancer_mama/blob/main/resultado-imagens.png)

# Conclusão
- Foi possível desenvolver uma rede neural profunda para classificar tipos de câncer (maligno ou benigno), através de imagens de ultrasom da mama.  
- A rede neural teve uma performance boa porém é necessário avaliar com outras imagens. 
