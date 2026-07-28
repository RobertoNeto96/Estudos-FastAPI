. Para começarmos a preprarar o ambiente instalamos algumas extensões no python sendo eles:
    . install pipx
    . pipx install poetry
    . pipx inject poetry poetry-plugin-shell

------------------------------------------------------------------------------------------------------------------------------------------------

. Após as instalações vamos criar um novo projeto com o comando do poetry: 
    . poetry new --flat fastapi_zero 
    . Esse comando cria uma pasta com os arquivos do novo projeto

------------------------------------------------------------------------------------------------------------------------------------------------

. Vamos instalar uma versão especifica do Python para acompanhamento do curso e mais compatibilidade
    . poetry python install 3.13

------------------------------------------------------------------------------------------------------------------------------------------------

. Depois vamos mostrar ao poetry qual versão do python vamos utilizar, com o comando: 
    . poetry env use 3.13    

------------------------------------------------------------------------------------------------------------------------------------------------

. Vamos instalar agora o fastapi com o comando:
    .poetry add "fastapi[standard]"    

------------------------------------------------------------------------------------------------------------------------------------------------

. Agora vamos começar criando o arquivo "app.py" , importamos o fastapi , criamos uma instancia do fastapi com uma variavel "app" e depois definimos uma função:
    . from fastapi import FastaAPI

     app = FastAPI()

     @app.get('/')
     def read_root():
        return{'message':'Olá Mundo!'}

------------------------------------------------------------------------------------------------------------------------------------------------

. Para executarmos ou iniciarmos o servidor com o FastAPI usamos:
    . poetry run fastapi dev fastapi_zero/app.py
    . Lembrando que o "fast_zero" é nome do projeto que estamos trabalhando nesse curso, nomes podem ser diferentes em projetos solos

------------------------------------------------------------------------------------------------------------------------------------------------

. Um ponto importante é que quando executamos o comando de criação de conexão, podemos acessar a documentação do nosso FastAPI e executar comando diretos pela documentação e testar alterações, no endereço copiado quando executamos a inialização do servidor, adicionamos o /docs no final do endereço, para acessarmos a pagina:
    . http://127.0.0.1:8000/docs
    . Nesse formato padrão, chamamos de Swegger, é uma documentação interativa

. Temos um outro formato padrão alem do /docs, que é o /redoc:
    . http://127.0.0.1:8000/redoc
    . Diferente do swagger, essa documentação não é interativa    

------------------------------------------------------------------------------------------------------------------------------------------------

. Ferramentas que ajudam no desenvolvimento

------------------------------------------------------------------------------------------------------------------------------------------------
    . Ruff --> Linter e formatador que ajuda a procurar erros no código
        . Analisar o codigo de forma estatica (linter): verificações se estamos programando de acordo com boas praticas do Python
        . Formatar o codigo (formatter): Efetua verificações do codigo para padronizar um estilo de codigo pré-definido
        . Para instalação: 
        . poetry add --group dev ruff
    . Após instalado, precisamos configurar o Ruff no arquivo pyproject.toml, configurações onde serão distintas em 3 tabelas diferentes

    . CONFIGURAÇÃO GLOBAL:
        . [tool.ruff]
          line-length = 79  -->  Tamanho maximo da extensão da linha de codigo, maximo de colunas que uma unica linha pode ter
          extend-exclude = ['migrations']  --> Regra que definimos para qual pasta/arquivo queremos que o Python NÃO olhe, ou mexa

    . CONFIGURAÇÃO LINTER
        . [I] ISORT --> Ordenação de imports em ordem alfabetica
        . [F] PYFLAKES --> Procura por alguns erros em relação a boas praticas de codigo
        . [E] PYCODESTYLE --> Erros de estilo de codigo
        . [W] PYCODESTYLE --> Avisos sobre estilo de codigo
        . [PL] PYLINT --> Erros em relação a boas praticas de codigo
        . [PT]FLAKE8-PYTEST --> Boas praticas do pytest
        . Para configurarmos vamos ao pyproject.toml e definimos:
        [tool.ruff.lint]
        preview = true
        select = ['I','F','E','W','PL','PT']

    CONFIGURAÇÃO FORMATTER
        . Nessa configuração a unica coisa que vamos alterar é o uso das aspas duplas para aspas simples: 
        . No arquivo pyproject.toml:
            .[tool.ruff.format]
            preview = true
            quote-style = 'single'

. Comando muito importantes do RUFF, são os comandos de verificar se há algum "erro" no codigo digitado, e o comando de corrigir todo o codigo de acordo com as boas praticas do python:
    . poetry run ruff check  -->  Verifica todas as linhas de codigos ja digitadas e menciona tudo o que há de errado, de acordo com as boas praticas do Python
    . poetry run ruff format  -->  Atualiza todas as linhas de codigo de acordo com as boas praticas do Python            

------------------------------------------------------------------------------------------------------------------------------------------------

    . Pytest --> Ferramenta para escrever testes
        . Ferramenta onde escrevemos e executamos nossos testes, e configuramos ele para reconhecer o caminho base para a execução dos testes na raiz do projeto, instalamos o pytest e o pytest coverage com o comando:
            . poetry add --group dev pytest pytest-cov
        . Após a instalaçao vamos configurar o pytest no arquivo pyproject.toml:
            . [tool.pytest.ini_options]
              pythonpath = "."
              addopts = '-p no:warnings'    
    . Para executarmos o pytest e ver quais codigos estao sendo testados, utilizamos o comando: 
        . pytest
        . obs: Caso o comando nao funcione, inicie o ambiente virtual primeiro com o poetry  -->  poetry shell   

-----------------------------------------------------------------------------------------------------------------------------------------------               

    . Taskipy --> Ferramenta que encurta comandos, codigos mais intuitivos 
        . Para instalarmos o Taskipy utilizamos o comando: 
            . poetry add --group dev taskipy 
    . Após a instalação vamos as configurações do taskipy
        . No arquivo pyproject.toml:
            [tool.taskipy.tasks]
            lint = 'ruff check'
            format = 'ruff format'
            run = 'fastapi dev fast_zero/app.py'
            test = 'pytest -s -x --cov=fast_zero -vv'        
