# Instalando e testando o ambiente com Docker

1. Garanta que possui privilégios para usar o comando "sudo"

2. Execute os comandos:

```
curl -fsSL https://get.docker.com/ | bash
```

Em seguida, vamos dar permissões para que você possa executar o docker de modo não privilegiado (sem usar o root diretamente ou sudo):

```
dockerd-rootless-setuptool.sh install
```

O comando acima pode pedir que você faça alguma instalação de pacote a mais. Caso aconteça, siga as instruções e depois execute o comando novamente.

Por último, adicione seu usuário ao grupo docker para evitar ter quaisquer problemas ao utilizar forward de portas (para sistemas com iptables e iptables-legacy) ao executar seus containers:

```
sudo usermod -a -G docker $USER
```

Por último, mas não menos importante, vamos habilitar o autocomplete do docker para facilitar seu uso na command line:

Para bash:

```
sudo apt install bash-completion -y

sudo curl https://raw.githubusercontent.com/docker/docker-ce/master/components/cli/contrib/completion/bash/docker -o /etc/bash_completion.d/docker.sh

```

Para zsh: 
 - Para o ZSH, recomendo a instalação do [oh-my-zsh](https://ohmyz.sh/), e ativar os plugins relacionados ao docker e também o de kubernetes.
 - Existem diversos plugins bacanas disponíveis, como o de Terraform, por exemplo. Olhe a lista e ative apenas os que são úteis para seus estudos e uso diário.

 Reinicie seu dispositivo e bora partir para os testes!

3. Executando o primeiro container:

```
docker container run alpine:latest
```

4. Listando todos os containers:

```
docker container ls -a
```

5. Parando um Container sem destruir:

```
docker container stop [CONTAINER ID]
```

6. Reiniciando um container:

```
docker container restart [CONTAINER ID]
```

7. Retomando atividade de um container parado:

```
docker container unpause [CONTAINER ID]
```

8. Verificando estatísticas de um container:

```
docker container stats [CONTAINER ID]
```

9. Verificando logs de um container:

```
docker container logs -f [CONTAINER ID]
```

10. Removendo um container:

```
docker container rm [CONTAINER ID]
```

11. Forçando a remoção de um container (em status running):

```
docker container rm -f [CONTAINER ID]
```