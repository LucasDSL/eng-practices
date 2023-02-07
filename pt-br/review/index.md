# Guia de Revisão de Código do Desenvolvedor 

## Introdução {#intro}

A revisão de código é um processo onde alguém além do autor do código o examina.

No Google, utilizamos o code review para manter a qualidade do nosso código e produtos. 

Essa documentação é a descrição canônica dos processos e políticas da revisão de código no Google. 



Essa página é um resumo do nosso processo de revisão de código. Há dois outros documentos que são parte desse guia: 

-   **[Como revisar código]()**: Um guia detalhado para revisores de código. 
-   **[O Guia do autor de uma CL]()**: Um guia detalhado para desenvolvedores que possuam CL em processo de revisão. 

## O Quê Revisores de Código Procuram? {#look_for}
Revisores de código devem procurar: 

-   **Design**: O código tem um bom design e está apropriado ao sistema ? 
-   **Funcionalidade**: O código tem o funcionamento que o autor almejava? A forma que o código funciona é adequada a seus usuários? 
-   **Complexidade**: O código poderia ser simples? Outros desenvolvedores entederão facilmente e poderão usar esse código quando lidarem com ele no futuro? 
-   **Testes**: O código tem testes bem feitos e corretos? 
-   **Nomes**: O desenvolvedor escolheu bons nomes para variáveis, classes, métodos etc? 
-   **Comentários**: Os comentários são concisos e úteis? 
-   **Estilo**: O código segue os nossos [style guide](http://google.github.io/styleguide/)?
-   **Documentação**: O desenvolvedor também enviou uma documentação relevante?

Veja **[Como Fazer uma revisão de Código]() para mais informações.

### Selecionando os melhores revisores {#best_reviewers}

Em geral, você deseja encontrar os *melhores* revisores que puder e for capaz de
responder a sua avaliação dentro de um prazo razoável.

O melhor revisor é a pessoa que poderá lhe fornecer as informações mais completas
e uma revisão decente para o pedaço de código que você está escrevendo. Isso geralmente significa o(s)
proprietário(s) do código, que podem ou não ser as pessoas no arquivo OWNERS.
Às vezes, isso significa pedir a diferentes pessoas que olhem para diferentes partes da
CL.

Se você encontrar um revisor ideal, mas ele não estiver disponível, você deve pelo menos CC (marcá-los)
eles em sua mudança.

### Exames presenciais (e programação em pares) {#in_person}

Se você programou em par um código com alguém qualificado para fazer uma
boa revisão de código nele, então este código pode ser considerado como revisado.

Você também pode fazer revisões de código pessoalmente, onde o revisor faz perguntas e o desenvolvedor das mudanças só as responde.

## Veja também {#seealso}

-   **[Como revisar código]()**: Um guia detalhado para revisores de código. 
-   **[O Guia do autor da CL]()**: Um guia detalhado para desenvolvedores que possuam CL em processo de revisão. 