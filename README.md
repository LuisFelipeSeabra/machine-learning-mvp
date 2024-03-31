# MVP - Machine learning

## Descrição do conjunto de dados 📜

Este conjunto de dados oferece uma variedade de atributos valiosos para uma análise abrangente. 
Ele contém 555.719 instâncias e 22 atributos, uma mistura de tipos de dados categóricos e numéricos. 
É importante ressaltar que o conjunto de dados está completo sem valores nulos.
Aqui está uma análise dos atributos:

* Trans_date_trans_time:Timestamp da transação (data e hora).
* Cc_num: Número de identificação exclusivo do cliente.
* Comerciante: O comerciante envolvido na transação.
* Categoria: Tipo de transação (por exemplo, pessoal, assistência infantil).
* Valor: Valor da transação.
* Primeiro: Primeiro nome do titular do cartão.
* Sobrenome do titular do cartão.
* Gênero: gênero do titular do cartão.
* Rua: Endereço do titular do cartão.
* Cidade: Cidade de residência do titular do cartão.
* Estado: Estado de residência do titular do cartão.
* CEP: CEP do titular do cartão.
* Lat: Latitude da localização do titular do cartão.
* Long: Longitude da localização do titular do cartão.
* City_pop: População da cidade do titular do cartão.
* Cargo: Cargo do titular do cartão.
* Dob: Data de nascimento do titular do cartão.
* Trans_num: identificador exclusivo da transação.
* Unix_time: carimbo de data/hora da transação (formato Unix).
* Merch_lat:Localização do comerciante (latitude).
* Merch_long: localização do comerciante (longitude).
* Is_fraud: Indicador de transação fraudulenta (1 = fraude, 0 = legítima). Esta é a variável alvo para fins de classificação.

## Preparação de Dados ☕️

Utilizou-se algumas técnicas, durante o projeto, como:
#### One-hot Encoding
O One-Hot Encoding é uma técnica de pré-processamento de dados que converte variáveis categóricas em binários. Em outras palavras, ele cria uma nova coluna para cada valor único presente na variável categórica e atribui o valor 1 à coluna correspondente ao valor presente e 0 no resto das colunas

#### Label  Encoding
Label Encoding consiste em converter as classes categóricas em números que as representam (ex: masculino/feminino são convertidos em 0/1, Brasil/EUA/Japão serão convertidos em 0/1/2, etc.). 

#### Balancemaneto da base com SMOTE
A SMOTE (técnica de sobreamostragem minoritária sintética) é uma técnica estatística para aumentar o número de casos em seu conjunto de um modo equilibrado. O componente funciona gerando novas instâncias de casos minoritários existentes que você fornece como entrada.

#### Transformacao de datas de aniversário em idade

## Modelagem e treinamento 🎉

Foram utilizados os seguintes para treinar e testar:

modelo_knn = dict(nome = "KNN", modelo = KNeighborsClassifier())
modelo_cart = dict(nome = "CART", modelo = DecisionTreeClassifier())
modelo_nb = dict(nome = "NB", modelo = GaussianNB())
modelo_svm = dict(nome = "SVM", modelo = SVC())

Divisao da base entre teste e treino foi de 80/20

#### Utilizamos validacao cruzada:
Na validação cruzada k-fold, você divide os dados de entrada em subconjuntos de dados k (também chamados de folds). Você treina um modelo de ML em todos, menos em um (k-1) dos conjuntos de dados e, em seguida, avalia o modelo no conjunto de dados que não foi usado para treinamento.

## Avaliação de Resultados 🦄


#### One-hot Encoder
Utilizando one hot encoder, atingimos os seguintes valores de treino:
KNN: 0.996064 (0.000072)
CART: 0.996720 (0.000045)!
NB: 0.939459 (0.000839)
SVM: 0.996084 (0.000097)

Já para testes:
Acurácio do modelo KNN: 0.996014
Acurácio do modelo CART: 0.996869!
Acurácio do modelo NB: 0.940393
Acurácio do modelo SVM: 0.996293


#### Label Encoder
Utilizando label encoder, atingimos os seguintes valores de treino:
KNN: 0.996156 (0.000061)
CART: 0.996648 (0.000094)!
NB: 0.992168 (0.000859)
SVM: 0.996082 (0.000094)

Já para testes:
Acurácio do modelo KNN: 0.996257
Acurácio do modelo CART: 0.996779!
Acurácio do modelo NB: 0.992559
Acurácio do modelo SVM: 0.996284


#### SMOTE + label encoder
Utilizando SMOTE para balancear a base, atingimos os seguintes valores de treino:
KNN: 0.986253 (0.000079)
CART: 0.988424 (0.000028)!
NB: 0.814953 (0.003902)

Já para testes:
Acurácio do modelo KNN: 0.980197
Acurácio do modelo CART: 0.988169!
Acurácio do modelo NB: 0.976373


## Conclusão 🔥

Em todos os testes e treinamentos, CART obteve a maior acurácia!

Porém KNN(utilizando SMOTE) conseguiu o melhor desempenho em encontrar fraudes(357), em contrapartida, apresentou muitos falsos positivos(2132). 
Esse modelo previu, corretamente, que 108586 casos não eram fraudes e errou apenas 69(falso negativo).

Já o Cart(one-hot encoder), com acurácia de 0.996869, encontrou 252 fraudes e apresentou poucos falsos positivos(174).
Esse modelo previu, corretamente, que 110544 casos não eram fraudes e encontrou 174 falsos negativos.

A melhor opcao encontrada para evitar fraudes foi o KNN(utilizando Smote), uma vez que conseguiu prever o maior numero de fraudes, cerca de 357 casos.
Apesar da quantidade de falsos positivos, o modelo foi o que mais previu fraudes e o que menos apresentou casos falso negativo: 69.