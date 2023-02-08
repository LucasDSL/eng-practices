# CLs pequenos



## Por que escrever CLs pequenos? {#why}

CLs pequenas e simples são:

- **Revisadas mais rapidamente.** É mais fácil para um revisor encontrar cinco minutos
     várias vezes para revisar pequenas CLs do que reservar um bloco de 30 minutos para
     revise uma grande CL.
- **Revisada mais detalhadamente.** Com grandes mudanças, revisores e autores tendem
     ficar frustrado com grandes volumes de comentários detalhados voltando e
     adiante - às vezes até o ponto em que pontos importantes são perdidos ou deixados de lado.
- **Menor probabilidade de apresentar bugs.** Como você está fazendo menos alterações, é
     mais fácil para você e seu revisor raciocinar efetivamente sobre o impacto de
     o CL e ver se um bug foi introduzido.
- **Menos trabalho desperdiçado se forem rejeitados.** Se você escrever uma CL enorme e depois
     seu revisor diz que a direção geral está errada, você desperdiçou muito tempo
     de trabalho.
- **Mais fácil de mesclar.** Trabalhar em uma grande CL leva muito tempo, então você pode
     ter muitos conflitos quando você mesclar, e você terá que mesclar
     frequentemente.
- **Mais fácil de projetar bem.** É muito mais fácil aperfeiçoar o design e a saúde do código de uma pequena mudança do que refinar todos os detalhes de uma grande
     mudança.
- **Menos bloqueio de comentários.** Enviando partes independentes de sua CL permite que você continue codificando enquanto espera pela sua
     CL em análise.
- **Mais simples de reverter.** Uma CL grande provavelmente tocará em arquivos que foram
     atualizados no período entre o envio inicial da CL e um rollback da CL, complicando
     a reversão (os CLs intermediários provavelmente precisarão ser revertidos
     também).

Observe que **os revisores podem rejeitar suas alterações imediatamente para o
única razão de ser muito grande. ** Normalmente eles vão agradecer por sua
contribuição, mas pedir que, de alguma forma, a transforme numa série de
mudanças. Pode ser muito trabalhoso dividir uma mudança depois que você já a fez, ou exigir muito tempo discutindo sobre por que o revisor deveria aceitar
sua grande mudança. É mais fácil apenas escrever pequenos CLs em primeiro lugar.

## O que é pequeno? {#what_is_small}

Em geral, o tamanho certo para um CL é **uma alteração independente**. Isso significa
que:

- O CL faz uma alteração mínima que aborda **apenas uma coisa**. Isso é
     geralmente apenas uma parte de um recurso, em vez de um recurso inteiro de uma vez. Em
     geral, é melhor errar do lado de escrever CLs que são muito pequenas vs.
     CLs muito grandes. Trabalhe com seu revisor para descobrir o que é um
     tamanho aceitável.
- A CL deve [incluir código de teste relacionado](#test_code).
- Tudo o que o revisor precisa entender sobre a CL (exceto futuro desenvolvimento) está na CL, na descrição da CL, na base de código existente ou numa
     CL que ele já revisou.
- O sistema continuará funcionando bem para seus usuários e para os desenvolvedores
     após o check-in da CL.
- A CL não é tão pequena a ponto de suas implicações sejam difíceis de entender. Se
     você adiciona uma nova API, você deve incluir um uso da API no mesmo CL para
     que os revisores possam entender melhor como a API será usada. Isso também
     impede o check-in de APIs não utilizadas.

Não há regras rígidas e rápidas sobre quão grande é "grande demais". 100 linhas é
geralmente um tamanho razoável para um CL, e 1000 linhas geralmente é muito grande, mas
cabe ao julgamento do seu revisor. O número de arquivos que uma alteração é
espalhada também afeta seu "tamanho". Uma alteração de 200 linhas num arquivo pode ser
ok, mas distribuído em 50 arquivos, geralmente seria muito grande.

Tenha em mente que, embora você tenha estado intimamente envolvido com seu código desde
no momento em que você começa a escrevê-lo, o revisor geralmente não tem contexto. O que
parecer uma CL de tamanho aceitável para você pode ser opressor para o seu revisor.
Em caso de dúvida, escreva CLs menores do que você acha que precisa escrever.
Os revisores raramente reclamam de obter CLs muito pequenos.

## Quando os CLs grandes estão corretos? {#large_okay}

Existem algumas situações em que grandes mudanças não são tão ruins:

- Normalmente, você pode contar a exclusão de um arquivo inteiro como sendo apenas uma linha de
     mudança, porque não leva muito tempo para o revisor revisar.
- Às vezes, uma grande CL foi gerado por uma ferramenta de refatoração automática
     em que você confia totalmente, e o trabalho do revisor é apenas verificar e dizer
     que eles realmente querem a mudança. Essas CLs podem ser maiores, embora alguns
     das ressalvas acima (como fusão e teste) ainda se aplicam.

### Divisão por arquivos {#splitting-files}

Outra maneira de dividir uma CL é por agrupamentos de arquivos que exigirão
revisores diferentes, mas são alterações autocontidas.

Por exemplo: você envia uma CL para modificações em um buffer de protocolo e
outra CL para alterações no código que usa esse protocolo. Você tem que enviar o
protocolo CL antes do código CL, mas ambos podem ser revisados simultaneamente. Se
você fizer isso, você pode querer informar ambos os conjuntos de revisores sobre a outra CL
que você escreveu, para que tenham contexto das mudanças. 

Outro exemplo: você enviou uma CL para a mudança de código e outra para a configuração ou experimento que use aquele código; isso também é fácil de reverter, se necessário, já que arquivos de configuração/experimentação às vezes vão pra produção mais rápido do que mudanças de código. 

## Refatorações separadas {#refactoring}

Geralmente é melhor fazer refatorações em CLs separadas das alterações de recursos ou
correções de bugs. Por exemplo, mover e renomear uma classe deve estar numa CL diferente
de corrigir um bug nessa classe. É muito mais fácil para os revisores entenderem
as mudanças introduzidas por cada CL quando separadas.

Pequenas limpezas, como corrigir um nome de variável local, podem ser incluídas dentro de um
mudança de recurso ou correção de bug numa CL própria, no entanto. Cabe ao julgamento dos desenvolvedores e
revisores para decidir quando uma refatoração é tão grande que tornará a revisão
mais difícil se incluída na CL atual.

## Mantenha o código de teste relacionado na mesma CL {#test_code}

CLs devem incluir código de teste relacionado. Lembre-se que [pequenez](#what_is_small)
aqui remete a ideia conceitual de que a CL deve ser focado e não é um
função simplista na contagem de linha.

Uma CL que adiciona ou altera a lógica deve ser acompanhada por testes novos ou atualizados
para o novo comportamento. CLs de refatoração pura (que não se destinam a alterar
comportamento) também devem ser cobertos por testes; idealmente, esses testes já existem,
mas se não tiverem, você deve adicioná-los.

Modificações de teste *independentes* podem entrar primeiro em CLs separados, semelhante ao
[diretrizes de refatoração](#refactoring). Isso inclui:

* Validação de código submetido pré-existente com novos testes.
     * Garante que a lógica importante seja coberta pelos testes.
     * Aumenta a confiança nas refatorações subsequentes no código afetado. Por exemplo, se você quiser refatorar o código que ainda não está coberto por
         testes, enviar CLs de teste *antes* de enviar CLs de refatoração pode
         validar que o comportamento testado permanece inalterado antes e depois da
         reestruturação.
* Refatorar o código de teste (por exemplo, introduzir funções auxiliares).
* Apresentando um código de estrutura de teste maior (por exemplo, um teste de integração).

## Não quebre a build {#break}

Se você tiver várias CLs que dependem uns dos outros, você precisa encontrar uma maneira de
certificar-se de que todo o sistema continua funcionando após o envio de cada CL. De outra forma
você pode interromper a build para todos os seus colegas desenvolvedores por alguns minutos
entre seus envios de CL (ou até mais se algo der errado inesperadamente
com seus envios CL posteriores).

## Não é possível torná-lo pequeno o suficiente {#cant}

Às vezes, você encontrará situações em que parece que sua CL *tem* que ser
grande. Isso raramente é verdade. Os autores que praticam a escrita de CLs pequenos podem
quase sempre encontram uma maneira de decompor a funcionalidade em uma série de pequenas
mudanças.

Antes de escrever uma CL grande, considere se precedê-la com uma CL somente de refatoração poderia abrir caminho para uma implementação mais limpa. Converse com sua equipe e
veja se alguém tem alguma ideia de como implementar a funcionalidade em pequenas CLs.

Se todas essas opções falharem (o que deve ser extremamente raro), obtenha consentimento
de seus revisores com antecedência para revisar uma grande CL, para que sejam avisados sobre
o que está por vir. Nesta situação, espere passar pelo processo de revisão
por muito tempo, fique atento para não introduzir bugs e seja extremamente diligente
sobre como escrever testes.

Próximo: [Como lidar com os comentários do revisor](handling-comments.md)

