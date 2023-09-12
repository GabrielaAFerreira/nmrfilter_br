Esse código foi utilizado no artigo https://pubs.rsc.org/en/content/articlelanding/2019/fd/c8fd00227d. Para mais informações por favor acesse a pasta original, clicando aqui: https://github.com/stefhk3/nmrfilter

Esse fork possui como objetivo apenas explicar de maneira mais detalhada a instalação


Instalação
============

Para o NMRFilter funcionar é necessário ter a versão Java 1.8 ou superior, assim como a versão Python 3 (3.11 funcionava até o presente momento). As demais bibliotecas para instalação estão contidas no requirements.txt
Para uma instalação completa recomenda-se acompanhar os seguintes passos:

Linux/Ubuntu
---
Abra o terminal e insira os seguintes comandos:
1. python3 -m venv nmrfilter_env
2. cd nmrfilter_env/bin
3. source activate
	1. Esse comando é fundamental para ativar o ambiente virtual.
4. pip install --upgrade pip
	1. Esse comando atualizará o pip
5. pip install -r requirements.txt

No linux pode ser necessário modificar o arquivo nmrfilter.sh para um executável com chmod a+x nmrfilter.sh

Se o python-igraph apresentar uma mensagem de erro dê uma olhada nessa solução: https://stackoverflow.com/questions/34113151/how-to-install-igraph-for-python-on-windows

Anaconda
--------
Abra o terminal e execute os seguintes passos:
1. conda update -n base -c defaults conda
	1. Esse comando atualiza o anaconda. É recomendável sempre o manter atualizado.
2. conda create -c conda-forge -n nmrfilter_env
	1. Assim é criada uma pasta chamada "nmrfilter_env" que terá as bibliotecas funcionais.
3. conda activate nmrfilter_env
4. conda install pip
5. pip install -r requirements.txt

Utilizando o Jupyter notebook
----------------------

Se você quiser executar o código no jupyter notebook:

Ubuntu:
1. cd nmrfilter_env/bin
2. source activate
3. jupyter nbextension enable --py widgetsnbextension
4. jupyter notebook /home/gabrielaaferreira/Desktop/GitHub/

Anaconda:
1. conda activate nmrfilter_env
2. jupyter nbextension enable --py widgetsnbextension
3. jupyter notebook \Users\gabrielaaferreira\Desktop\Laabio(IPPN)

IMPORTANTE: Executando o Código
=======
O programa funciona com projetos em pastas individuais. Para exemplos dê uma olhada no repositório: https://github.com/stefhk3/nmrfilterprojects. 
As configurações para execução estão contidas no arquivo nmrproc.properties.
A propriedade datadir é onde os projetos/pastas são procurados. Se você baixou os exemplos nmrfilterprojects, configure-os para o diretório nmrfilterprojects.

Os seguintes dados/arquivos precisam ser fornecidos para executar uma análise na pasta do projeto na qual você deseja trabalhar:
* Uma lista de candidatos SMILES. Isso está nos arquivos especificados pela propriedade `msmsinput` (padrão testall.smi). Deve ter uma estrutura por linha.
* Os espectros medidos em `spectruminput` (padrão realspectrum.csv). Deve ser uma lista de turnos, separados por tabulação. Uma linha é um turno. Como padrão, os turnos HMBC e HSQC estão incluídos aqui.
* Defina a propriedade `solvente` para o solvente usado se for `Metanol-D4 (CD3OD)` ou `Clorofórmio-D1 (CDCl3)`. Caso contrário, use `Não relatado`.

Assim que esses arquivos estiverem no lugar, execute `nmrfilter.sh <projectname>` (linux) ou `nmrfilter.bat <projectname>` (windows). Isso deve produzir a lista de resultados. Substitua <projectname> pelo nome do projeto/pasta em que deseja trabalhar.

Os seguintes recursos são opcionais:
* Você pode incluir turnos HSQCTOCSY. Para isso, defina `usehsqctocsy=true` e inclua as mudanças HSQCTOSY no arquivo `spectruminput`.
* Você pode produzir alguma saída de depuração configurando `debug=true`. Você precisa de um arquivo chamado `testallnames.txt` para isso, que contém os nomes dos compostos na mesma ordem do arquivo `msmsinput`.
* Você pode definir parâmetros para tolerâncias e resoluções. Normalmente estes não precisam ser modificados.
* Com `useeeplearning=true` você pode ativar a previsão de respedição (https://jcheminf.biomedcentral.com/articles/10.1186/s13321-019-0374-3) em vez da previsão baseada no código HOSE. Isto dá melhores resultados, mas requer passos a mais de instalação, descritos no fork original.
