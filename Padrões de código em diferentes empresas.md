# Padrões de código em diferentes empresas - o que devo usar?

No mundo da programação, é muito comum que existam convenções e regras de estilização específicas para que a ordem seja mantida durante a criação de soluções dos mais variados tipos. Geralmente, essas convenções são criadas a partir das ideias iniciais de design previamente
desenvolvidas para aquela linguagem, fazendo com que todo código criado naquela tecnologia siga um padrão específico. Um grande exemplo que percebi ao longo da minha carreira foi o conjunto de regras que existe no C#, a linguagem C-like da Microsoft desenvolvida para rodar no runtime .NET (muito similar a Java, por sinal, inclusive em algumas convenções específicas). 

Por exemplo, no C#, a nomeação de classes, propriedades públicas e métodos (não irei me aprofundar sobre o que são nesse artigo em específico) é por convenção realizada em **PascalCase** - um casing onde as palavras são separadas por uma letra maiúscula (similar ao **camelCase**, onde a primeira letra do casing é minúscula, e a separação das outras letras ocorre com letras maiúsculas indefinidamente). Mesmo assim, em diferentes empresas que trabalhei com .NET (e outras linguagens também, mas vamos focar no .NET por agora), existe a utilização de padrões de código que vão contra essas convenções, inclusive em alguns lugares foram criados sistemas de regras inteiros para ditar como devem ser os padrões a serem seguidos devido a decisões e necessidades internas. 

Um grande exemplo onde convenções se adaptam melhor se direcionadas às necessidades do negócio, é por exemplo, uma empresa que utiliza diversas tecnologias para montar uma mesma solução - visto a presença de times multidisciplinares, peças da solução que se adaptam melhor a tecnologias específicas ou limitações de negócio que fazem com que certas partes da solução tenham que ser construídas com essas tecnologias. Leve em consideração uma empresa hipotética que utilize **lambdas python**, que depois de diversas análises técnicas por parte de times de engenharia e arquitetura se mostraram a forma mais rápida e efetiva de prototipar e montar peças de solução. A mesma empresa conta com uma vasta gama de desenvolvedores C#, fazendo com que várias soluções (como workers e REST APIs) sejam feitas utilizando a linguagem, e por isso uma solução interessante para se manter no padrão entre comunicações fosse simplesmente alterar o casing das respostas de APIs e outras requisições para **snake_case**, beneficiando assim a utilização de python no ambiente de desenvolvimento.

Quando se fala de padrões de código, também podem ser levados em consideração conjuntos de práticas que são realizadas para montar um programa. O melhor exemplo para falar sobre conjuntos de práticas é o JavaScript (ou TypeScript), sendo uma linguagem extremamente flexível onde é possível utilizar diversos paradigmas diferentes em uma mesma aplicação. Por exemplo, algumas empresas utilizam o framework **NestJS** para o desenvolvimento de aplicações web, esse framework é extremamente baseado em programação orientada a objetos - que por sua vez conta com vasta utilização de classes, herança assim como vários design patterns, onde o que mais se destaca é a injeção de dependências.

> Injeção de dependência (Dependency Injection, em inglês) é um padrão de desenvolvimento de programas de computadores utilizado quando é necessário manter baixo o nível de acoplamento entre diferentes módulos de um sistema. Nesta solução as dependências entre os módulos não são definidas programaticamente, mas sim pela configuração de uma infraestrutura de software (container) que é responsável por "injetar" em cada componente suas dependências declaradas. - *Wikipedia*

Geralmente, as soluções montadas em Nest utilizam um pattern de serviços para identificar peças de funcionalidades que podem ser reutilizadas de maneira desacoplada, como no exemplo:

```js
import { Injectable } from '@nestjs/common';
import { Cat } from './interfaces/cat.interface';

@Injectable()
export class CatsService {
  private readonly cats: Cat[] = [];

  findAll(): Cat[] {
    return this.cats;
  }
}
```

Já outras empresas utilizam uma arquitetura mais livre, geralmente baseada em módulos e métodos ou até mesmo "features", passando as dependências como argumentos nas funcionalidades que irão precisar fazer seu uso, fazendo assim com que a utilização desses métodos também seja possível em ambientes de testes e outras ocasiões. Um exemplo, diretamente de um projeto pessoal que fiz anteriormente, pode ser:

```ts
const createPendingMessage = async (
    input: CreatePendingMessageOptions,
    token: string,
    db: Database
) => {
    const sentAt = new Date().toISOString();
    const uuid = randomUUID();

    await checkJwtOwnership(token, input.senderId);

    await db
        .insert(pendingMessageTable)
        .values({
            uuid,
            sentAt,
            senderId: input.senderId,
            receiverId: input.receiverId,
            content: input.content
        });

    return uuid;
}
```

## Mas afinal, o que utilizar?

Do ponto de vista profissional, se adequar ao ambiente de trabalho é uma soft skill essencial para "sobreviver". Obviamente não estou falando de aceitar decisões ruins sem questionamento, mas sim para buscar entender o motivo de certas decisões serem implementadas e de onde elas vieram, só assim é possível acumular experiência para poder confrontar decisões de design futuras. O correto é sempre procurar se adaptar ao design utilizado por sua equipe ou empresa, e se cabível, questionar e implementar gradualmente mudanças dependendo do seu nível de influência. Isso não significa que fora do ambiente de trabalho seja necessário utilizar essas mesmas decisões de design, afinal, uma das características de uma boa pessoa programadora é a adaptabilidade.
