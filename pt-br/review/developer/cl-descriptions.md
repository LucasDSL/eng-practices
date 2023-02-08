# Escrevendo boas descrições de CL



Uma descrição de CL é um registro público de **quais** alterações estão sendo feita e **por quê**
foram feitas. Ele se tornará uma parte permanente de nosso histórico de controle de versão e
possivelmente será lido por centenas de pessoas além de seus revisores ao longo do
anos.

Os futuros desenvolvedores procurarão sua CL com base em sua descrição. Alguém no futuro pode estar procurando por sua mudança por causa de uma vaga lembrança de sua
relevância, mas sem os detalhes à mão. Se todas as informações importantes forem
no código e não na descrição, vai ser muito mais difícil para eles
localizar sua CL.

## Primeira linha {#firstline}

* Breve resumo do que está sendo feito.
* Frase completa, escrita como se fosse uma ordem.
* Seguido por uma linha vazia.

A **primeira linha** de uma descrição de CL deve ser um breve resumo de
*especificamente* **o quê** *está sendo feito pela CL*, seguido por uma linha em branco.
Isso é o que aparece nos resumos do histórico de controle de versão, portanto, deve ser
informativo o suficiente para que futuros pesquisadores de código não precisem ler sua CL ou a
descrição completa para entender o que sua CL realmente *fez* ou como ele difere
de outros CLs. Ou seja, a primeira linha deve ficar isolada, permitindo que os leitores
percorra o histórico do código muito mais rapidamente.

Tente manter sua primeira linha curta, focada e direta ao ponto. A clareza e
utilidade para o leitor deve ser a principal preocupação.

Por tradição, a primeira linha de uma descrição CL é uma frase completa, escrita
como se fosse uma ordem (uma frase imperativa). Por exemplo, diga
\"**Exclue** o FizzBuzz RPC e **o substitui** pelo novo sistema." em vez de
de \"**Excluindo** o FizzBuzz RPC e **substituindo** pelo novo sistema."
Você não precisa escrever o restante da descrição como uma frase imperativa,
no entanto.

## O corpo é Informativo {#informative}

A [primeira linha](#firstline) deve ser um resumo curto e focado, enquanto o resto
da descrição deve preencher os detalhes e incluir qualquer
informações que um leitor precise para entender a lista de alterações de forma holística. Pode ser
que inclua uma breve descrição do problema que está sendo resolvido e por que isso é
a melhor abordagem. Se houver alguma falha na abordagem, ela deve ser
mencionada. Se relevante, inclua informações básicas, como números de bugs,
resultados de benchmark e links para documentos de design.

Se você incluir links para recursos externos, considere que eles podem não estar visíveis
para futuros leitores devido a restrições de acesso ou políticas de retenção. Onde for
possível inclua contexto suficiente para revisores e futuros leitores entenderem
a CL.

Mesmo pequenas CLs merecem um pouco de atenção aos detalhes. Coloque o contexto da CL

## Descrições de CLs ruins {#bad}

"Corrigir bug" é uma descrição de CL inadequada. Que erro? O que você fez para consertar?
Outras descrições igualmente ruins incluem:

- "Conserta compilação."
- "Adiciona correção."
- "Movendo o código de A para B."
- "Fase 1."
- "Adicionar funções de conveniência."
- "matar URLs estranhos."

Algumas dessas são descrições reais de CL. Embora curtos, não fornecem
informações úteis suficientes.

## Boas descrições de CL {#good}

Aqui estão alguns exemplos de boas descrições.

### Mudança de funcionalidade

Exemplo:

> rpc: remove o limite de tamanho na lista gratuita de mensagens do servidor RPC.
>
> Servidores como o FizzBuzz têm mensagens muito grandes e se beneficiariam com a reutilização.
> Aumenta a freelist e adicione uma goroutine que libera as entradas da freelist
> lentamente ao longo do tempo, para que os servidores ociosos eventualmente liberem todos as entradas de 
> freelists

As primeiras palavras descrevem o que o CL realmente faz. O resto do
descrição fala sobre o problema que está sendo resolvido, por que esta é uma boa solução,
e um pouco mais de informações sobre a implementação específica.

### Reestruturação

Exemplo:

> Construir uma tarefa com um TimeKeeper para usar seus métodos TimeStr e Now.
>
> Adicione um método Now a Task, para que o método getter borglet() possa ser removido (que
> foi usado apenas pelo OOMCandidate para chamar o método Now do borglet). Isso substitui os
> métodos em Borglet que delegam a um TimeKeeper.
>
> Permitir que o Tasks forneça agora é um passo para eliminar a dependência de
> Borglet. Eventualmente, os colaboradores que dependem de obter o Now da Task
> deve ser alterado para usar um TimeKeeper diretamente, mas isso tem sido um
> acomodação para refatoração em pequenos passos.
>
> Continuando o objetivo de longo prazo de refatorar a Hierarquia Borglet.

A primeira linha descreve o que a CL faz e como isso é uma mudança do
passado. O restante da descrição fala sobre a implementação específica, o
contexto da CL, que a solução não é ideal, e possível direção futura.
Também explica *por quê* essa mudança está sendo feita.

### Pequeno CL que precisa de algum contexto

Exemplo:

> Cria uma regra de compilação Python3 para status.py.
>
> Isso permite que os consumidores que já estão usando isso como em Python3 dependam de um
> regra que está ao lado da regra de criação de status original em vez de em algum lugar
> sua própria árvore. Ele encoraja novos consumidores a usar Python3 se puderem,
> em vez de Python2, e simplifica significativamente algumas
>  ferramentas automatizadas de refatoração de arquivos que estão em desenvolvimento. 

A primeira frase descreve o quê está sendo feito. O resto da
descrição explica *por quê* a mudança está sendo feita e dá ao revisor muito contexto.

## Descrição de CLs geradas

Algumas Cls são geradas por ferramentas. Sempre que possível, suas 
descrições devem seguir o conselho aqui. Isto é, suas primeiras linhas 
devem ser curtas, diretas e isoladas, e a descrição da CL deve
conter detalhes informativosque ajude os revisores e quem quer que busque no código a entender o efeito de cada CL. 

## Revise a descrição antes de enviar a CL 

CLs podem passar por muitas mudanças durante uma revisão. Pode ser vantajoso revisar a descrição da CL antes de enviá-la, para garantir que a descrição 
ainda reflete o que a CL faz. 

Próximo: [Pequenas CLs](./small-cls.md)