# AWS Lambda Docker Python Pillow

Registrar conteúdo de aprendizagem sobre AWS Lambda, utilizando Docker para um runtime python instalando
a lib Pillow.

O uso do docker para gerenciar a função lambda, foi escolhido por facilitar o processo de instalação e manutenção
das dependencias do projeto.

O objetivo final é comparar a performance com diferentes libs de resize e imagens, tendo um mesmo ambiente base para as funções lambda.

## 0. Requisitos
- AWS Cli ([link sobre instalação](https://docs.aws.amazon.com/pt_br/cli/latest/userguide/getting-started-install.html))
- AWS Sam ([link sobre instalação](https://docs.aws.amazon.com/pt_br/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html))
-  clonar este repositorio localmente:
```bash
git clone git@github.com:carlossantoswd/aws-lambda-docker-pillow.git .
```
## 1. Testar a função lambda local
```bash
sam build && sam local invoke DockerPillowFunction
```
## 2. Caso faça alterações no app.py após ter dado build:
```bash
docker rmi $(docker image ls dockerpillowfunction -q) && sam build && sam local invoke DockerPillowFunction
```

## 3. Deploy para amazon
```bash
sam deploy --stack-name docker-pillow  --resolve-s3 --resolve-image-repos --capabilities CAPABILITY_AUTO_EXPAND CAPABILITY_IAM
```