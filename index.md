## Bem vindo!

Nesse projeto será demonstrado a construção de um algoritmo de análise preditiva, baseado no modelo estatístico Bayesiano, com o objetivo de identificar inadimplentes dentro de uma base de crédito ficctícia.

Abaixo as ferramentas e dados utilizados para esse projeto:

 - [Rstudio] (https://rstudio.cloud/)
 - [Credit-G] (https://www.openml.org/d/31)

### Modelo Bayesiano

Existem diversos algoritmos e bibliotecas que utilizam a IA para modelos preditivos classificatórios, para este projeto será utilizado o algoritmo Naive Bayes, que é um modelo de classificação probalístico, ou seja, ela irá descartar a correlação entre as <i>features</i>, tratando cada uma de maneira independente e desta forma irá mensurar a probabilidade de cada varíavel de cada <i>feature</i> para as possíveis classificações.


### Pacotes

Para desenvolver essa aplicação será necessário fazer a instalação de alguns pacotes, abaixo segue o script com as instalações dos mesmos.

```markdown
Syntax highlighted code block
install.packages("caTools")
install.packages("e1071")
install.packages("caret")
library(caTools)
library(e1071)
library(caret)

# É possível saber mais sobre os pacotes instalados com o seguinte comando: ??[Nome do Pacote];
# Ex:
??e1071
```

### Divisão

Após as instalações dos pacotes iniciamos a construção do algoritmo. Após fazer a importação da base Credit-G, separamos a base em dois conjuntos de dados, um para treino (70%) e outro para teste (30%), esse tipo de divisão é chamada de <i>hold out</i>. 

```markdown
dados1 <- credit
divisao = sample.split(dados1$class, SplitRatio = 0.7)
base_treinamento = subset(dados1,divisao==TRUE)
base_teste = subset(dados1,divisao==FALSE)
```

### Modelo


Finalizando a divisão, iniciamos a construção do modelo classificatório, chamamos a função <i>naiveBayes()</i>, essa função pertence a biblioteca <i>e1071</i> e ela com base em calculos bayesianos retorna a relevância com base na probabilidade de cada variavel para a classificação.

Para treinar o modelo usaremos a nossa base de treinamento.

```markdown
classificador = naiveBayes(x = base_treinamento[,-21], y = base_treinamento$class)
```

Veja que são passados dois parametros para a função, x e y, isso nos remete a um plano cartesiano, onde o x recebe a base de treinamento sem a classificação que a fonte possui, que no caso se encontra na coluna 21, e no y informamos a base de treinamento com a classificação.

### Previsão

Com o modelo pronto usaremos agora o método <i>predict</i> para inferir o modelo criado e treinado sobre a base de teste. Para isso, retiramos a classificação que a base de teste possui e passamos como parametro o modelo criado.

```markdown
previsao = predict(classificador,newdata = base_teste[,-21])
```

### Validação

Ao concluir a previsão, precisamos validar a acurácia da previsão, para isso usamos uma matriz de confusão, que é uma comparação da previsão com a realidade, portanto, comparamos os resultados da previsão feita na base de teste com a classificação original dela.

```markdown
matriz = table(base_teste$class,previsao)
confusionMatrix(matriz)
```


### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
