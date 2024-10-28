Considerações: professor, tentei absolutamente de tudo para fazer funcionar o balanceamento de carga corretamente utilizando os 'DNS' do container através dos nomes dos serviços. Porém, eu não sei por qual motivo, que meus containers não consegue resolver esses nomes. Os meus arquivos estão todos como se estivessem configurados para funcionar balanceando, então favor considerar o que puder. Caso voce queira testar o funcionamento, basta fazer as seguintes alterações:

- No arquivo nginx.conf:
    - onde tiver 'proxy_pass http://backend_servers/;' trocar para 'proxy_pass http://localhost:5000;'
- No arquivo dockerfile (frontend):
    - na linha 'ENV REACT_APP_BACKEND_URL=http://backend:5000' trocar para 'ENV REACT_APP_BACKEND_URL=http://localhost:5000'

# Trabalho Containers PUC-MG
## Aluno: Gabriel Moraes Spelta

### Instruções para instalação:
Ao realizar o clone do repositorio fornecido pelo professor, mova a pasta 'frontend' para fora do diretório padrão, pois o docker-compose irá está uma pasta acima do diretório do jogo.

A pasta no qual você irá executar o docker-compose deverá conter a seguinte estrutura apenas:

```bash
glsp@GFT-wP4RUYCUTbo:~/docker-aula/trab01$ ls
docker-compose.yml  frontend  guess_game
```

O dockerfile do frontend com o nginx ficará dentro da pasta 'frontend' enquanto o do flask (backend) ficará na pasta 'guess_game'

Para o frontend, não execute nenhum build no seu computador, pois realizei essa etapa de build através de um container utilizando imagem node.



## Arquitetura escolhida:

- Temos o servidor nginx como frontend da nossa aplicação realizando o balanceamento de cargas para as requisições do backend em flask. Esse balanceamento está configurado no arquivo nginx.conf com as rotas definidas por lá.
- O database escolhido foi um postgres e está usando um volume próprio. A senha para acesso ao postgres é 'passtest'.
- Para a parte de network, criei uma rede chamada 'gamenetwork' e inseri todos os containers nessa mesma rede para possuírem total conexão.
  
## Exemplo de execução:

```bash
glsp@GFT-wP4RUYCUTbo:~/docker-aula/trab01$ ls
    docker-compose.yml  frontend  guess_game
glsp@GFT-wP4RUYCUTbo:~/docker-aula/trab01$ docker-compose up --build -d --scale backend=3
```
Acesse a aplicação utilizando http://localhost:80
