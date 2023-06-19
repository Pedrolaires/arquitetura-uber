## Um pouco da história


A ideia da Uber foi concebida por Travis Kalanick e Garrett Camp. Ambos fundaram a empresa em 2009 em São Francisco, nos Estados Unidos, inicialmente como um serviço de limusine para o mercado de elite. Desde então, a empresa se expandiu rapidamente para se tornar uma das maiores empresas de transporte do mundo.

Assim, a Uber foi lançada em São Francisco em 2010 como um serviço de compartilhamento de caronas. Com o tempo, a empresa se expandiu para outras cidades dos Estados Unidos e, posteriormente, para o resto do mundo, tornando-se uma das maiores empresas de transporte do mundo. 

<br>

![Uber](/images/Uber.png)


## Sobre o aplicativo

O aplicativo permite ao passageiro solicitar corridas, e para isso busca sua localização e destino, método de pagamento e provê um sistema de avaliação de motoristas e usuários. Ele permite que usuários solicitem o serviço do motorista de onde estiverem e a proposta é que o carro chegue em minutos. Para atingir esse alvo, ele precisa ser capaz de processar solicitações em tempo real, ter previsões de trajeto precisas, integração com outras plataformas e ter uma experiência de usuário fluida e rápida. Além disso, ele deve ser confiável, seguro e ter uma interface acessível. Uma outra preocupação importante é a escalabilidade já que a Uber oferece o serviço para milhões de usuários em todo mundo e necessita se adaptar a diferentes regras e peculiaridades de cada mercado.


- Sistema de pagamentos:
> O sistema de pagamentos administra todos as transações entre passageiro e motorista. A segurança é crítica, sendo prezada a todo custo.

- Sistema analítico
> A uber acompanha diversas métricas dos usuários, podendo ser de solicitações de transporte, cancelamento dessas solicitações, pagamento, avaliação etc. Todas essas métricas coletadas são usadas para otimizar o serviço.

- banco de dados geoespacial
> É a base da dados responsavel por armazenar a localização em tempo real dos motoristas e passageiros, sua importância é tanta que as solicitações de corrida entre um passageiro e um motorista que realmente está na área só acontece devido à este serviço.

- Mapas
> O serviço de mapas provê para o aplicativo mapas em tempo real e localizações para ambos os usuários, seus requisitos são primordialmente o tempo de resposta, a veracidade do mapa e as rotas com um certo grau de acurácia.

- Serviço de mensageria
> O serviço de mensageria provê um serviço de mensagens em tempo real entre os passageiros e motoristas, devendo suportar diversos canais para tal: Sms, notificações ou mensagens no próprio aplicativo.

- Segurança
> A segurança do sistema deve ser a base de tudo, a prevensão de fraudes é um dos pontos significativos da segurança pois há dados sensiveis e financeiros em transação. São utilizados alguns mecanismos de criptografia, autenticação e a autorização para garantir a segurança e privacidade de todos.


- Infraestrutura
> O sistema da uber requer uma infraestrutura muito robusta para encarar os números que solicitam seus serviços seja eles de corridas ou de transações ao final delas. Este setor da a plicação abrange os servidores, armazenamento, conexões dos serviços e integração dos componentes.
___

Em suma, com toda essa infraestrutura apresentada já podemos saber que sua arquitetura deve ser extremamente escalável e distribuída pois requer o uso de diversastecnologias para garantir o bom funcionamento da aplicação

___

## A arquitetura

A arquitetura  Uber é composta por vários sistemas interconectados que trabalham juntos para fornecer um serviço de transporte eficiente e confiável.

Varios sitemas interconectados compõem a arquitetura da Uber, juntos eles trabalham para fornecer o serviço confiável prometido pelo aplicativo. Em suma, sua arquitetura pode ser resumida em três camadas principais:

- ***Aplicação***: É a camada onde o aplicativo móvel reside, usado pelos passageiros e motoristas, o aplicativo se comunica com vários serviços que a uber proporciona, como o serviço de localização, pagamentos, comunicação, etc. 

- ***Serviços***: Camada composta por diversos serviços responsáveis pelo gerenciamento de diversos aspectos do aplicativo, tais como os citados na camada de aplicação.
  
- ***Infraestrutura***: É onde reside os componentes que suportam a arquitetura da Uber, incluindo servidores, bancos de dados, armazenamento entre outros. 


A arquitetura de um software dessa magnitude conseguir ser resumida em apenas três pontos é apenas "diferente". Segundo seus idealizadores antigamente o aplicativo era um monolito enorme com uma base de dados única que administrava tudo. As tecnologias empregadas nesse sistema arcaico eram um backend em Python com SQLAlchemy como ORM para  abase da dos. Esse sistema funcionou durante o crescimento pois os números eram completamente ínfimos comparados aos de hoje.
Com os números crescendo absurdamente, em 2014 o time decidiu transformar o monolito em uma arquitetura orientada a serviços, assim, escalando também para o delivery de comida e objetos diversos.



>![Arquitetura em alto nível Uber](/images/Arquitetura_alto_nivel_Uber.png)
*Arquitetura a partir de 2014*


- ### DISCO
  O sistema de DISpatCh Optimization é utilizado para rastrear e entregar suas demandas, o sistema de dispatch utiliza o celular e toma a responsabilidade de conectar o passageiro do motorista.
  
  Em suma, o sistema divide o mapa em pequenas células geográficas com um Id único e utiliza esse Id como uma partição de dados no DISCO. Assim que o motorias recebe a solicitação do passageiro, a localização é atualizada utilizando o Id da célula. Basicamente, assim que o passageiro faz a solicitação, o sistema desenha um circulo ao redor dele e filtra todos as células que estão na região desenhada para enviar a solicitação.

  A vantagem que esse sistema criou para o Uber foi imensa. Sua escalabilidade é consistente pois é construído em NodeJS, que lida muito bem com eventos assíncronos.

- ### ARM64 

  A Uber decidiu utilizar o ARM64, uma arquitetura de processador de 64 bits amplamente utilizada em dispositivos móveis e data centers, para avaliar os benefícios em termos de economia de custos, consumo de energia e desempenho de computação. Inicialmente, consideraram criar suporte básico em uma zona isolada para experimentação, mas logo perceberam a importância de oferecer suporte completo ao ARM64 em sua infraestrutura principal. Isso permitiria reduzir os custos de computação, aumentar a diversidade de capacidade e modernizar a plataforma da Uber.

  Para alcançar seus objetivos, a Uber utilizou ferramentas como "zig cc" para compilar binários ARM64 e considerou o Zig como uma alternativa interessante para o desenvolvimento nessa arquitetura. A empresa enfrentou desafios técnicos ao habilitar o suporte completo para o ARM64 em sua infraestrutura central, mas buscou diversificar sua capacidade e reduzir os custos de computação por meio dessa adoção.

___

  


## Fontes utilizadas:

- https://www.geeksforgeeks.org/system-design-of-uber-app-uber-system-architecture/
- https://www.techaheadcorp.com/blog/uber-architecture-design/
- https://www.uber.com/en-BR/blog/bootstrapping-ubers-infrastructure-on-arm64-with-zig/
