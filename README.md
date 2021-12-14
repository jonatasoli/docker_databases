# Ambiente Docker


## O que preciso fazer antes de rodar?
* Instalar o Docker
* Instalar o Docker-compose

## Passos para executar
* Acessar a pasta infra
* Rodar docker compose conforme a ferramenta que você quer usar

## Recursos
* basic.yml - Roda Prisma, GraphQL, Kong, Konga, Redis, Postgres
* queue.yml - Roda Pulsar
* metabase.yml - Roda Metabase
* apm.yml - Roda o elastic stack
* code-analysis.yml - Roda o Sonarqube
* monitoring-tools.yml - Roda a stack Grafana + Prometheus

Obs: Sempre precisa rodar ao menos o basic.yml os outros são opcionais
```
docker-compose -f basic.yml -f queue.yml -f metabase.yml -f apm.yml -f code-analysis.yml -f monitoring-tools.yml up -d
```
* Aguardar 5 min para criar os databases e rodar as migrações
* Entrar no console do konga
[Konga Console](http://localhost:1337)
* Criar um usuário no konga
* Entrar em conections e criar a ligação com o Konga
```
Name *: Kong
Kong Admin URL *: http://kong:8001
```
* Ir em snapshots
* Clicar em importfile
* Selecionar o arquivo bkp_mac.json
* Clicar em import
* Clicar em details
* Clicar em Restore e escolher services e routes
* Verificar se o redirecionamento está funcionando no link abaixo:
[Link de teste](http://localhost/sns)

## O que contem nesse projeto?

* API Gateway
** Kong
* Gerenciador
** [Konga](http://localhost:1337)
* Database
** Postgres
* NOSQL
** Redis
* GraphQL
** Prisma
** Yoga
* Relatórios
** Metabase

# Instalar o Istioctl

* Criar uma pasta .istio
* Baixar o istio do site e descompactar
[Istio](https://istio.io/)
* Copiar o conteúdo pra pasta .istio
* Colocar .istio/bin no path do bashrc ou no zshrc
```
export .istio/bin:Path
```

# Dashboards Monitoração

* Kiali
```
istioctl dashboard kiali
```
* Grafana
```
istioctl dashboard grafana
```
* Jager
```

# Sonarqube

* Logar
```
user: admin
senha: admin
```
* Clicar em "create new project"
* Criar um project key
```
app-web
```
* Gere um token
```
app-token
```
* Clique em generate
* Copiar o token gerado
* Colocar linguagem outros
* Colocar o SO
* Baixar o sonarscanner
* Rodar o comando gerado dentro do app-web toda vez que ouver um commit
```
sonar-scanner \
  -Dsonar.projectKey=app-web \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login=seutoken
```
* Vai demorar mas, no final vai aparecer os dados no admin do sonarqube
* Ir para o projeto
* Vai Administration
* Vai em Market Place
* Adicione python e Js
* Clicar em reiniciar o servidor
* Pode fazer o procedimento para qualquer projeto
* Terminando o scanner você pode entrar no sonarqube e ir no projeto.
