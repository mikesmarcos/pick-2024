# Day-2: Trabalhando com imagens e Dockerfile
### Execução do projeto Giropops Senhas

O desafio para este dia consiste em montar o Dockerfile para a aplicação Giropops Senhas.
Durante o desafio, foi necessário corrigir erros de compilação do projeto, além de subir um container de REDIS e realizar a comunicação entre o container do app giropops-senhas e o container do REDIS.


### Passo-a-passo do desafio para execução local e teste

1. Clone o repositório:

```
git clone https://github.com/badtuxx/giropops-senhas.git
```

2. Entre no diretório de trabalho:

```
cd giropops-senhas
```

3. Atualize o sistema operacional:

```
sudo apt update -y
```

4. Certifique-se de ter o Python instalado e instale o gerenciador de pacotes Pip:

```
sudo apt install python3-pip -y
```

5. Instale os pacotes requeridos para o app:

```
pip install --no-cache-dir -r requirements.txt
```

6. Nesta etapa, podem surgir erros, que devem ser sanados. Não irei descrevê-los e proponho que investigue por conta própria para a solução.

7. Instale o Redis, uma dependência do projeto:

```
sudo apt install redis -y
```

8. Inicie o Redis:

```
sudo systemctl start redis
```

9. Crie uma variável de ambiente para que a aplicação encontre o Redis:

```
export REDIS_HOST=localhost
```

10. Iniciando a aplicação:

```
flask run --host=0.0.0.0
```

### Agora no Docker!

1. Criamos o Dockerfile, utilizando a imagem que achar mais apropriada para o desenvolvimento do desafio.
Os comandos RUN dentro do dockerfile precisarão receber parte dos comandos executados localmente na etapa anterior, então, é necessária atenção e escolha da melhor maneira de montar o arquivo para etapa de build.


2. Build:

```
docker build -t mikesmarcos/linuxtips-giropops-senhas:1.0 .
```

3. O desafio pede implicitamente que um container REDIS seja executado em paralelo para pleno funcionamento do app giropops-senhas, sendo assim, vamos executá-lo manualmente de forma direta:

    3.a. No meu caso, preferi dar stop nos serviços do redis localmente para poder usar a mesma porta de exposição do container:

    ```
    sudo systemctl stop redis && sudo systemctl stop redis-server
    ```
    3.b. Run no container do REDIS:

    ```
    docker container run -d -p 6379:6379 --name redis redis:alpine3.19
    ```

4. Vamos anotar o IP do container do Redis:

```
docker inspect redis | grep "\"IPAddress\":" | tail -n1 | cut -d: -f2 | cut -d, -f1
```

5. Run no giropops-senhas:

```
docker run -d -p 5000:5000 --env REDIS_HOST=IP_DO_CONTAINER_REDIS --name giropops-senhas mikesmarcos/linuxtips-giropops-senhas:1.0
```

6. Teste se está tudo up and running 😀 :

Acesse <http://localhost:5000/>.