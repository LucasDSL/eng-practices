# Emergências

Às vezes, existem CLs de emergência que devem passar por toda a revisão do código
tão rápido quanto for
possível.



## O que é uma emergência? {#what}

Um CL de emergência seria uma **pequena** alteração que: permite que um grande lançamento
continue, corrige um bug que afeta significativamente os usuários em
produção, lida com uma questão legal urgente, fecha uma grande falha de segurança, etc.

Em emergências, realmente nos preocupamos com a velocidade de todo o processo de revisão do código, não apenas a [velocidade de resposta](revisor/speed.md). Nesse caso
*apenas*, o revisor deve se preocupar mais com a velocidade da revisão e o
correção do código (ele realmente resolve a emergência?) do que qualquer outra coisa. Além disso (talvez obviamente) essas revisões devem ter prioridade sobre todas as outras
revisões de código, quando surgirem.

No entanto, depois que a emergência for resolvida, você deve examinar as CLs de emergência
novamente e dar a elas uma [revisão mais completa](revisor/procurando.md).

## O que NÃO é uma emergência? {#not}

Para ser claro, os seguintes casos *não* são uma emergência:

- Querer lançar esta semana em vez da próxima (a menos que haja algum
     [prazo fixo](#deadlines) real para lançamento, como um contrato de parceria).
- O desenvolvedor trabalhou em um recurso por muito tempo e realmente
     deseja obter o CL.
- Os revisores estão todos em outro fuso horário onde é noite ou
     eles estão fora do local.
- É o fim do dia em uma sexta-feira e seria ótimo receber a
     CL antes que o desenvolvedor saia para o fim de semana.
- Um gerente diz que esta revisão deve ser completa e a CL verificado
     hoje por causa de um [prazo flexível (não rígido)](#deadlines).
- Revertendo uma CL que está causando falhas de teste ou quebras de construção.

E assim por diante.

## O que é um prazo rígido? {#prazos}

Um prazo rígido é aquele em que **algo desastroso aconteceria** se você não o cumprisse. Por exemplo:

- O envio da sua CL até uma determinada data é necessário para uma obrigação contratual.
- Seu produto falhará completamente no mercado se não for lançado numa
     determinada data.
- Alguns fabricantes de hardware enviam hardware novo apenas uma vez por ano. Se você perder
     o prazo para enviar o código a eles, isso pode ser desastroso, dependendo do tipo de código você está tentando enviar.

Atrasar um lançamento por uma semana não é desastroso. Perder uma conferência importante
pode ser desastroso, mas muitas vezes não é.

A maioria dos deadlines são soft deadlines(prazos flexíveis), não hard deadlines(prazos rígidos). Eles representam um desejo
para um recurso ser feito em um determinado momento. Eles são importantes, mas você
não deve sacrificar a integridade do código para criá-los.

Se você tiver um longo ciclo de lançamento (várias semanas), pode ser tentador sacrificar
qualidade de revisão de código para obter um recurso antes do próximo ciclo. No entanto, esse
padrão, se repetido, é uma maneira comum dos projetos acumularem
dívida técnica. Se os desenvolvedores estiverem enviando as CLs rotineiramente perto do final do
ciclo, somente pois aquela mudança "deve estar presente" apenas com revisão superficial, então a equipe deve
mudar seu processo para que grandes mudanças de recursos ocorram no início do ciclo e
tenha tempo suficiente para uma boa revisão.