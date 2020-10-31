<p  align="center">
<img  alt="GitHub language count"  src="https://img.shields.io/github/languages/count/pedrorenan/js-expert-week">
<img  alt="Repository size"  src="https://img.shields.io/github/repo-size/pedrorenan/js-expert-week">
<a  href="https://www.twitter.com/pedrorenan/">
<img  alt="Siga no Twitter"  src="https://img.shields.io/twitter/url?url=https://github.com/pedrorenan/js-expert-week">
</a>
<a  href="https://github.com/tgmarinho/README-ecoleta/commits/master">
<img  alt="GitHub last commit"  src="https://img.shields.io/github/last-commit/pedrorenan/js-expert-week">
</a>
<img  alt="License"  src="https://img.shields.io/badge/license-MIT-brightgreen">
<a  href="https://github.com/pedrorenan/js-expert-week/stargazers">
<img  alt="Stargazers"  src="https://img.shields.io/github/stars/pedrorenan/js-expert-week?style=social">
</a>
</p>

### Pré-requisitos

 
Desde que você tenha instalado no seu computador [Docker](https://www.docker.com/get-started), o [VSCode](https://code.visualstudio.com/download) e a extensão [Remote-Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers), não tem pré-requisito algum, é só rodar o projeto! 😲

  

Instruções:

  
```bash
# Clone este repositório
$ git clone https://github.com/pedrorenan/js-expert-week.git

# Acesse a pasta do projeto no terminal/cmd
$ cd js-expert-week

# Abra o projeto com o VSCode
$ code .
```

Quando o [VSCode](https://code.visualstudio.com/download) abrir você verá uma mensagem informando que foram detectadas as configurações necessárias para que a extensão [Remote-Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) faça a mágica acontecer.



<p  align="center">

<img  alt="Remote Containers Dialog"  title="Remote Containers Dialog"  src="./assets/remote-containers-dialog.png"  width="400px">

</p>

  

Clique em "Reopen in Container". O [VSCode](https://code.visualstudio.com/download) vai reiniciar e é só aguardar o ambiente ficar pronto para você. Pode demorar um pouco na primeira vez se você nunca tiver feito o download dos containers necessários 🕐. Mas vale a pena!
  

Quando finalizar, você terá um terminal dentro do [VSCode](https://code.visualstudio.com/download) que já está dentro do container. Tudo integrado! Tipo [Inception](https://www.imdb.com/title/tt1375666/) mesmo 🍿.


💡 Tudo que você executar nesse terminal será executado dentro do container apenas!


>Eu escrevi um post sobre [VSCode](https://code.visualstudio.com/download) e [Remote-Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers), se quiser ler um pouco mais sobre o assunto, é só acessar ["Em busca da independência para o ambiente de desenvolvimento"](https://medium.com/@pedrorenan/em-busca-da-independ%C3%AAncia-para-o-ambiente-de-desenvolvimento-2adc22f6f250).


## Aula 01

```bash
#execute o script que gera os vídeos em vários formatos
$ sh script.sh
```

>🕐 Pode ser que demore um pouco, depende do seu ambiente. Verifique as pastas que vão sendo criadas em *assets/timeline*.

## Aula 02

1. Use dois terminais dentro do VSCode.

```bash
#Terminal 1
#execute o CDN
$ npm run assets
```

```bash
#Terminal 2
#execute a aplicação
$ npm run dev
```

2. No seu navegador de internet, acesse http://localhost:8080 ou http://127.0.0.1:8080

3. Clique na miniatura da Semana JS EXPERT e aperte o play!

## Aula 03


Você precisa de uma conta AWS e de Access Key ID e Secret access key, com permissões para S3 e CloudFront, para configurar a aws cli:


```bash
#configure a aws cli
$ aws configure

# Digite a Access Key ID
$ AWS Access Key ID []:xxxxxxxxxxxxxxxxxxxx

# Digite a Secret Access Key
$ AWS Secret Access Key []: xxxxxxxxxxxxxxxxxxxx

# Digite o nome da região que irá utilizar na AWS
$ Default region name []: us-east-1

# Digite o formato de saída
$ Default output format []: json

```


Você precisa de uma conta Serverless para realizar o deploy automático:
```bash
#faça o login na sua conta Serverless
$ sls login
```


Depois de serguir as instruções e estar autenticad@, você fará o deploy automático do CDN e da aplicação:

```bash
#acesse a pasta do CDN
$ cd assets

#faça o deploy
$ sls deploy

#você deverá receber uma infomação como essa ao final do deploy
bucket:          website-hericxb
distributionUrl: https://dsf7go5wikho4.cloudfront.net
bucketUrl:       http://website-hericxb.s3-website.us-east-1.amazonaws.com
url:             https://dsf7go5wikho4.cloudfront.net
```

Copie a url exibida na mensagem de sucesso que você recebeu e coloque na linha 5 do arquivo */public/manifest.json*  e salve o arquivo.

```json
5 "production": "https://dsf7go5wikho4.cloudfront.net",
```

Faça o deploy da aplicação:

```bash
#retorne um nível 
$ cd ..

#acesse a pasta da aplicação
$ cd public

#faça o deploy
$ sls deploy

#você deverá receber uma infomação como essa ao final do deploy
bucket:          website-erxflbt
distributionUrl: https://d1ax6alpfo7qd2.cloudfront.net
bucketUrl:       http://website-erxflbt.s3-website.us-east-1.amazonaws.com
url:             https://d1ax6alpfo7qd2.cloudfront.net
```

Aguarde uns 10 minutos. Confira se o deploy está pronto no painel do CloudFront da AWS. Para visualizar o projeto, use a url exibida na mensagem de sucesso seguida de /index/index.html, como no exemplo abaixo:


https://d1ax6alpfo7qd2.cloudfront.net/index/index.html


### IMPORTANTE

>💸 Não esqueça de parar suas aplicações para evitar custos desnecessários. Tem uma forma bem simples de fazer isso:

```bash
#acesse a pasta do CDN
$ cd assets

#remova a aplicação
$ sls remove

#retorne um nível 
$ cd ..

#acesse a pasta da aplicação
$ cd public

#remova a aplicação
$ sls remove

```

>💵 Sempre confira o painel do CloudFront na AWS para verificar se as aplicações não estão disponíveis e gerando custos.