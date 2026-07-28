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



