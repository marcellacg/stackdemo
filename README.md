#stackdemo

PASSO-A-PASSO

Para criar o aplicativo, rode o comando $docker compose up -d
Cheque se o app está rodando com o comando $docker compose ps
Para fazer os testes utilize o comando $curl http://localhost:8000
'Desligue' o app com o comando $docker-compose down --volumes

PARA FAZER O REGISTRO
Uma vez que o swarm têm muitos Docker Engines há a necessidade de fazer um registro para distribuição
de imagens para todos no swarm. Utilize o comando:
$docker service create --name registry --publish published=5000,target=5000 registry:2

Verifique o status com $docker service ls
Cheque se está rodando com o curl com o comando $curl http://localhost:5000/v2/

Para fazer a distribuição do app pelo swarm dê o comando $docker-compose push
Para o deploy do stack, utilize $docker stack deploy --compose-file docker-compose.yml stackdemo
Para checar se app aplicação está rodando, digite $docker stack services stackdemo
Para o teste com o curl, utilize novamente o comando prévio $curl http://localhost:8000
Para acessar o nó-worker digite $curl http://address-of-other-node:8000 !ATENÇÃO! address-of-node será
o endereço ip da máquina-worker, que poderá ser vericado com o comando $hostname -I

Na máquina-worker deverá ser introduzido o token para se juntar ao swarm, e ele será visto quando o
manager der o comando $docker swarm init

Para 'desligar' o stack, digite $docker stack rm stackdemo
Para 'desligar' o registro, digite $docker service rm registry

Se você estiver usando uma máquina local, tire o Docker Engine do modo swarm com $docker swarm leave --force