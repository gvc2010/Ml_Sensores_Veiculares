## Atividade Aprendizagem de Máquina - Spark MLLib

Considerando o dataset detalhado a seguir, aplique as técnicas solicitadas
Dataset dados de sensores veicular

    Arquivo disponível em /ML_Sensores_Veiculares/treinamento.csv
    Arquivo disponível em /ML_Sensores_Veiculares/teste.csv
    Dados relativos a sensores de internet das coisas (IoT) para detecção de estados dos medidores

| # | Nome do campo | Descrição | |---- |------------------------- |------------------------------------------------------------------------------- | | 0 | Hora | Hora média das medições | | 1 | Minuto | Minuto médio das medições | | 2 | Temp_minima | Temperatura mínima das medições | | 3 | Temp_maxima | Temperatura máxima das medições | | 4 | Latitude_media | Latitude média das medições | | 5 | Longitude_media | Longitude média das medições | | 6 | Classe | Estado do medidor (Frio, Moderado, Quente, Alerta) |

Informações a serem extraídas:

## 1 - Calcule a acurácia de classificação na base de testes para os seguintes classificadores:
        Árvore de Decisão (from pyspark.ml.classification import DecisionTreeClassifier)
        Random Forest com 5 arvores (from pyspark.ml.classification import RandomForestClassifier, e numTrees=5 no construtor do RandomForestClassifier)
        Random Forest com 100 arvores (numTrees=100 no construtor do RandomForestClassifier)
## 2 - Determine qual a quantidade de eventos Alerta (label = 3.0) classificados erroneamente como outra classe (falso-negativo) para os classificadores
        Árvore de Decisão (from pyspark.ml.classification import DecisionTreeClassifier)
        Random Forest com 5 arvores (from pyspark.ml.classification import RandomForestClassifier, e numTrees=5 no construtor do RandomForestClassifier)
        Random Forest com 100 arvores (numTrees=100 no construtor do RandomForestClassifier)
## 3 -  Determine qual a quantidade de eventos não Alerta (label = 0.0, ou label = 1.0, ou label = 2.0) classificados erroneamente como classe Alerta (falso-positivo) para os classificadores
        Árvore de Decisão (from pyspark.ml.classification import DecisionTreeClassifier)
        Random Forest com 5 arvores (from pyspark.ml.classification import RandomForestClassifier, e numTrees=5 no construtor do RandomForestClassifier)
        Random Forest com 100 arvores (numTrees=100 no construtor do RandomForestClassifier)
## 4 - Faça votação entre os classificadores da etapa 1.A, 1.B e 1.C para atribuir a classe do evento de acordo com a maioria das classes entre os classificadores
        Dicas: Para isto, voce irá precisar fazer o join das predições de cada classificador de acordo com os IDs dos eventos. Posteriormente voce pode manipular o dataframe, após o join, para determinar qual classe de cada evento possuiu maior votação =). Exemplo de código:


    import pyspark.sql.functions as func
    
    predicaoDT.select(func.col('prediction').alias('prediction_dt'),
                        func.col('label'),
                        func.col('id'))\
    .join(predicaoRF.select(func.col('prediction').alias('prediction_rf'),
                        func.col('id')), ['id'])

    Considerando que voce possui apenas duas classes: Não Alerta e Alerta. Calcule a acurácia de classificação na base de testes para os seguintes classificadores:
        Árvore de Decisão (from pyspark.ml.classification import DecisionTreeClassifier)
        Random Forest com 20 arvores (from pyspark.ml.classification import RandomForestClassifier, e numTrees=20 no construtor do RandomForestClassifier)
        Random Forest com 100 arvores (numTrees=100 no construtor do RandomForestClassifier)
            Dicas: Para isto, você irá precisar manipular o dataframe para alterar os valores da coluna label, por exemplo através de uma UDF
    Determine qual a quantidade de eventos Alerta (label = 3.0) classificados erroneamente como outra classe (falso-negativo) para os classificadores do item 5
    Faça busca de parametros dos classificadores desenvolvidos no item 5. Plote um gráfico relacionando a acurácia e os parametros otimizados
        Árvore de Decisão varie o parametro maxDepth de 1 a 20
        Random Forest varie o numTrees de 1 a 20

Dicas:

    Crie uma célula (Insert -> Insert Cell Below) para cada informação solicitada
    A análise deve ser feita sobre os dados do HDFS
    Inicialize o seu cluster executando o script em: Desktop/ambientes/spark/inicializar.sh
    Acesse o seu cluster executando o script em: Desktop/ambientes/spark/abrir_navegador.sh
