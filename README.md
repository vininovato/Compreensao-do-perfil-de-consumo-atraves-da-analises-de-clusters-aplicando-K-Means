# Compreensao-do-perfil-de-consumo-atraves-da-analise-de-clusters-aplicando-K-Means
PoC  - pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".
### Resumo
Em uma realidade de mercado cada vez mais competitiva e dinâmica, mostrou-se necessário entender a persona, ou seja, a representação do cliente ideal para determinado produto ou serviço. A necessidade trouxe novos desafios para o marketing, tanto em termos competitivos, como na compreensão dos perfis de compra em escala global. Dessa forma, o marketing tradicional precisou se aliar a ferramentas estatísticas para condensar, processar e compreender o imenso volume das transações. Otimizar e personalizar são os termos que guiam empresas com nível considerável de conhecimento operacional e estratégico. Neste trabalho, será utilizado uma base de dados com informações demográficas e histórico de compras. O intuito é compreender os dados e como relacionar os atributos de forma a estabelecer perfis de consumo através de algoritmos de clusterização

### 1. Introdução
As ferramentas de machine learning são largamente aplicadas ao marketing, e nesse trabalho, a proposta foi a aplicação de algoritmos não-supervisionados para entender a relação dos dados.

A aplicação dos métodos de clusterização, em segmentação de clientes, permite extrair insights poderosos para as empresas. O conhecimento extraído desses algoritmos permite entender como, dentro de um espaço de atributos, diversos agrupamentos demonstram os diferentes perfis de compra. 

Essa capacidade possibilita agir de forma segmentada, através da criação de novos serviços e produtos, campanhas promocionais específicas, e até mesmo manuais operacionais voltados para atividades comerciais.

Portanto, o intuito foi entender relações mais básicas entre os diversos atributos, e validar a similaridade dos dados dentro dos clusters e a dissimilaridade entre clusters.  


### 2. Modelagem
Na análise exploratória, uma das primeiras necessidades, foi o tratamento de missing values, através da exclusão dos dados. Como eram poucas instâncias, optar pela exclusão mostrou-se plausível. Através dos diagramas Boxplot foram detectados alguns outliers, para os atributos idade e salário (income). Alguns atributos não demonstraram relevância direta, após análise visual. Seriam os atributos Z_CostContact e Z_Revenue, os quais eram constantes.
Um dos passos mais importantes nessa aplicação, foi a fase de data wrangling. Os atributos demográficos e de histórico de compras permitiram criar variáveis. Foram somadas as colunas referentes à quantas pessoas continham na família para criar apenas um atributo. Para o estado civil (Marital_Status) a transformação dos dados mostrou-se necessária, pois informações diferentes caracterizavam a mesma coisa. Para o nível de educação também foi necessário manipular, e dessa forma diminuir o número de valores categóricos.

Para o histórico de consumo, optei novamente por uma abordagem mais simples. Os dados demonstram produtos de diferentes categorias consumidos por cada pessoa. Nesse caso, foram apenas somadas todas as colunas para criar outro atributo que caracteriza o consumo total. As análises serão ainda mais profundas se os produtos estiverem separados agregados por categoria.

O histograma de idades foi necessário para avaliar de forma mais compacta a distribuição dos dados.

Dessa forma ficou mais fácil condensar os dados em grupos de idade e assim visualizar numericamente, através de tabelas sumarizadas, quais atributos indicariam possíveis análises iniciais.
Considerando algumas análises mais básicas de marketing, a manipulação dos dados permitiu entender a taxas de engajamento proporcional, por grupo de idade, e a proporção de compras realizadas através de desconto.  
Após a manipulação dos dados e criação de atributos, alguns atributos foram excluídos.  
Posteriormente, foi aplicado o encoder nos poucos atributos categóricos e consequentemente o Standard Scaler para o algoritmo K Means. Para a parte de feature selection, apliquei o PCA a fim de manter o número de colunas com variância acumulada de aproximadamente 96%. Nesse caso, o plot demonstrou redução para 15 atributos. 
Finalmente, foram aplicados os métodos de avaliação para auxiliar o número de clusters. Nessa fase foram aplicados os métodos de Inércia, silhouette score e silhouette diagram (visualização).


### 3. Resultados
Antes da aplicação dos modelos, a avaliação para decidir os N Clusters foi feita através do silhouette score e diagram.
![image](https://github.com/user-attachments/assets/3d85da0e-ef09-47c9-880b-039a0ca82fdd)
O gráfico demonstrou cotovelo de 3 para 4 clusters. Os valores calculados para cada cluster mostram que, dentro do intervalo de avaliação do silhouette score [-1,1], os valores positivos e próximos de 0 indicam parte dos dados de diferentes clusters com sobreposição. 
![image](https://github.com/user-attachments/assets/ef5e850b-fbf4-4b65-a128-be85686f957a)
Considerando uma avaliação visual, o silhouette diagram demonstra o número de clusters, linha tracejada vertical que indica a média do silhouette score, e o tamanho de cada cluster.
![image](https://github.com/user-attachments/assets/8e50830b-1d6b-4a2a-b436-96602eaab314)
O método indica a escolha otimizada deve considerar silhuetas que demonstrem quantidade de dados semelhante e que passem da linha tracejada. Nesse caso, a escolha foi reforçada para 3 e 4 clusters.
Conforme gráficos abaixo, o silhouette score para 3 clusters indica maior dissimilaridade. Para 4 clusters é possível notar a sobreposição dos dados. As duas relações devem ser validadas analisando a relação dos atributos com os labels em cada cluster.
![image](https://github.com/user-attachments/assets/029456fe-7442-4455-ad80-63fe1d9b03ad)
![image](https://github.com/user-attachments/assets/f6174191-b58e-4bec-88e5-0c5fb4fb656f)
![image](https://github.com/user-attachments/assets/62c34a1d-23dc-4b99-b4a5-c59d70950e10)

A distribuição de dados para 3 clusters também foi mais equilibrada.

![image](https://github.com/user-attachments/assets/d645cbe0-8cf6-4381-a6bc-8c1b7cd40da5)

A distribuição para 4 cluster, além de demonstrar maior desigualdade na quantidade de dados, também indicou a superposição na fronteira entre clusters.
![image](https://github.com/user-attachments/assets/f6df721d-194f-4aba-9ca3-4181fffa33b1)


### 4. Conclusões

Com o intuito de interpretar se os dados de cada cluster tem sentido real, foram plotados três gráficos de dispersão. Para o eixo x dos gráficos foram mantidos a feature ‘Age_on_2014’ e para o eixo y foram considerados as três features (‘Deal_Dependency’, ‘Total_Amount_Spent’, ‘MntSweetProducts’)

O foco inicial, para validar a qualidade dos clusters, foi a análise no cluster 3.
Para o primeiro gráfico de dispersão, a distribuição foi semelhante para diferentes idades. A princípio, esse cluster aponta um perfil de consumo com baixa taxa de compras através de desconto. 
![image](https://github.com/user-attachments/assets/a22ce8fc-adc9-41f0-b153-c164da94ac7d)
Complementar ao gráfico acima, os dados abaixo demonstram que esse grupo é o que mais consome.
![image](https://github.com/user-attachments/assets/0a4854d9-293d-4b81-8a0e-9bd6e098cb94)
O gráfico abaixo foi uma interpretação arbitrária, entre um determinado produto e o tamanho da família.
![image](https://github.com/user-attachments/assets/f60bede4-1ddc-4138-ad00-0fabb7150a94)
Finalmente, os diferentes diagramas boxplot apontam que a renda para o cluster 3 é a mais alta. Esse fato reforça as informações anteriores. 

É normal que o perfil de consumo do grupo com maior poder aquisitivo apresente características como; 

-menor dependência de compra através de descontos
-tamanho da família é menor
-consumo superior.

![image](https://github.com/user-attachments/assets/82a85128-6f8e-4861-b157-3789be6444c6)

Portanto, é plausível concluir que o comportamento dos clusters apresenta relação real entre os atributos. Considerações para os outros clusters podem ser utilizadas como ferramentas de suporte à decisão para equipes comerciais e de marketing. Para mais desdobramentos, é possível tratar as análises em níveis de categoria de produto, testes A/B para campanhas online e mecânicas de desconto. 

---

Matrícula: 123.456.789

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*




