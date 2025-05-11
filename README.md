# Modelo de Machine Learning no Azure

#### Criação de um modelo de regressão no Azure Machine Learning para predição das vendas de sorvetes de acordo com a temperatura

## _Base de Dados_

O dataset com 100 registros foi criado de forma aleatória com código Python.
<center><img src="Prints-desafioUm/46.png" width="400"></center>

O resultado ficou assim:
<center><img src="Prints-desafioUm/48.png" width="300"></center>

## _Criação da subscription, resource group e acesso ao Azure Machine Learning Studio_

Na página inicial do Azure accese o _resource group_ para criar um grupo de recursos, local que armazenara todo o trabalho e arquivos.
<center><img src="Prints-desafioUm/02.png" width="600"></center>

Dentro do _resource group_, criamos uma _subscription_, o _resource group_ e escolhemos a região.
<center><img src="Prints-desafioUm/03.png" width="400"></center>

Após criado, o _resource group_ fica assim:
<center><img src="Prints-desafioUm/05.png" width="700"></center>

Dentro dele, pesquisamos pelo Azure Machine Learning e clicamos em _create_.
<center><img src="Prints-desafioUm/07.png" width="450"></center>

Confirmamos a _subscription_, o _resource group_ e a região.
<center><img src="Prints-desafioUm/08.png" width="600"></center>

Após criado, o Azure Machine Learning  fica assim:
<center><img src="Prints-desafioUm/09.png" width="600"></center>

Clicamos em _Lauch Studio_ para entrar no _Azure Machine Learning Studio_.
<center><img src="Prints-desafioUm/12.png" width="450"></center>

## _Escolha da Computação_

Para treinar os dados e criar modelos, é imprescindível criar uma instância de computação que atenda a necessidade do trabalho. Para isso, vamos em _Computação_ e escolhemos uma instância de computação. O Azure oferece várias opções por preços acessíveis, escolha uma que se encaixa nas suas necessidades.
<center><img src="Prints-desafioUm/14.png" width="500"></center>

Também é importante escolher um _cluster de computação, que será utilizado na criação do pipeline.
<center><img src="Prints-desafioUm/15.png" width="500"></center>

## _Configuração do Jupyter Notebook e o Upload dos arquivos_

No seu computador crie uma pasta com a base de dados em formato _.csv_ e o Jupyter Notebook com o script de treinamento em Python e o arquivo _.json_ com as informações adicionais para a configuração da credential.
<center><img src="Prints-desafioUm/47.png" width="300"></center>

Faça o upload da pasta para a seção _Notebooks_ do Azure Machine Learning Studio.
<center><img src="Prints-desafioUm/13.png" width="400"></center>

## _Início do Job no ML Automatizado_

Criamos um ativo de dados a partir do upload do mesmo dataset.
<center><img src="Prints-desafioUm/17.png" width="700"></center>

O Azure automaticamente armazena os dados no Storage Blog. Recomendo manter essa configuração.
<center><img src="Prints-desafioUm/18.png" width="600"></center>

Configuramos quais são as colunas o Azure irá trabalhar. Também é importante confirmar o tipo de dado (inteiro ou decimal) dos valores e é possível alterar. Nesse caso, os dados da Temperatura foram alterados de decimal para inteiro.
<center><img src="Prints-desafioUm/20.png" width="500"></center>

Confirmamos se o tipo de dado está como tabular.
<center><img src="Prints-desafioUm/21.png" width="500"></center>

Em _ML automatizado_, escolhemos o tipo de tarefa, nesse caso, a Regressão.
<center><img src="Prints-desafioUm/22.png" width="600"></center>

Além disso, é possível escolher o algoritmo no qual desejamos que o Azure utilize. Nesse caso, queremos somente o _XGBoostRegressor_.Portanto bloqueamos todos os outros.
<center><img src="Prints-desafioUm/23.png" width="650"></center>

Selecionamos a coluna de destino, nesse caso, a _Quantidade de Sorvetes_ é a principal variável que o modelo de regressão vai trabalhar.
<center><img src="Prints-desafioUm/24.png" width="600"></center>

Configuramos o número máximo de nós, o tempo limite do experimento e também da iteração.
<center><img src="Prints-desafioUm/25.png" width="500"></center>

Escolhemos a instância de computação, nesse caso, o cluster de cálculo. O Azure irá utilizar a instância que foi criada anteriormente. Confirmamos todas as informações e colocamos o experimento para rodar.
<center><img src="Prints-desafioUm/26.png" width="500"></center>

Após o experimento ser finalizado, ele aparecerá como concluído.
<center><img src="Prints-desafioUm/41.png" width="500"></center>

Clicamos no experimento e podemos ver os modelos e trabalhos-filhos.
<center><img src="Prints-desafioUm/42.png" width="600"></center>

É possível ver as métricas de cada modelo, analisá-los e ver qual é o melhor.
<center><img src="Prints-desafioUm/43.png" width="700"></center>

Após escolher um modelo, é só implantá-lo.
<center><img src="Prints-desafioUm/44.png" width="500"></center>

## _Criação do Pipeline_

Também podemos criar um pipeline do experimento. Para isso vamos na seção _Designer_.
<center><img src="Prints-desafioUm/27.png" width="450"></center>

Selecionamos o dataset que foi carregado.
<center><img src="Prints-desafioUm/28.png" width="500"></center>

Para montar o pipeline, vamos selecionando os componentes. Aqui foi escolhido o componente _Select Columns in Dataset_.
<center><img src="Prints-desafioUm/32.png" width="400"></center>

Em cada componente, vamos configurando os parâmentros. Aqui escolhemos as colunas que possuem os valores que importam para o modelo.
<center><img src="Prints-desafioUm/40.png" width="400"></center>

Aqui foi escolhido o componente _Split Data_.
<center><img src="Prints-desafioUm/29.png" width="650"></center>

Configuração dos parâmetros: Será treinado apenas 20% do dataset.
<center><img src="Prints-desafioUm/30.png" width="400"></center>

Ligamos um componente ao outro.
<center><img src="Prints-desafioUm/33.png" width="500"></center>

Configuração dos parâmetros: Coluna selecionada para o treinamento.
<center><img src="Prints-desafioUm/35.png" width="500"></center>

Escolhemos a tarefa: Regressão Linear.
<center><img src="Prints-desafioUm/34.png" width="300"></center>

Após conectar todos os componentes, o pipeline fica assim:
<center><img src="Prints-desafioUm/36.png" width="600"></center>

Finalizamos o pipeline, dando-lhe um nome:
<center><img src="Prints-desafioUm/37.png" width="500"></center>

E selecionando a instância de computação:
<center><img src="Prints-desafioUm/39.png" width="600"></center>

Pronto! Agora o trabalho de Machine Learning foi criado.