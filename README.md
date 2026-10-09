# Atividade-Valendo-nota-LEO

UNICESUMAR
SISTEMAS OPERACIONAIS 

O MODELO DE PROCESSOS
SALA DE AULA INVERTIDA

Alunos: Nicollas Azalim Prado. RA: 25013758-2
Felipe Piva. RA: 25054343-2

Londrina 2026

---

Nicollas Azalim Prado. RA: 25013758-2
Felipe Piva. RA: 25054343-2

O MODELO DE PROCESSOS
SALA DE AULA INVERTIDA

Relatório técnico apresentado à disciplina de Sistema Operacional, do curso de Engenharia de Software, da Unicesumar, como atividade avaliativa.

Professor: Leonardo Rocha

Londrina 2026

---


# 1. INTRODUÇÃO

Atualmente, os sistemas computacionais estão presentes em diversas atividades do nosso dia a dia, desde tarefas simples, como acessar um site, até operações mais complexas, como realizar pagamentos, consultar informações e comprar ingressos pela internet. Com o avanço da tecnologia e o aumento do número de pessoas utilizando serviços digitais, tornou-se cada vez mais importante desenvolver sistemas capazes de atender a várias solicitações ao mesmo tempo, mantendo a segurança, a organização e a confiabilidade das informações. Para que isso seja possível, os Sistemas Operacionais desempenham um papel fundamental, pois são responsáveis por gerenciar os recursos do computador e coordenar a execução dos programas. Dentro desse contexto, o estudo dos processos e das threads permite compreender melhor como os sistemas conseguem executar diferentes atividades de maneira concorrente. Um processo representa um programa em execução e possui recursos necessários para seu funcionamento, enquanto as threads correspondem às linhas de execução que existem dentro de um processo. Por meio delas, uma aplicação pode organizar diferentes tarefas, permitindo que várias atividades avancem de forma concorrente. Essa organização contribui para o aproveitamento dos recursos computacionais e pode melhorar o desempenho de aplicações que precisam atender a muitos usuários simultaneamente. Entretanto, permitir que várias tarefas sejam executadas ao mesmo tempo também apresenta desafios. Quando diferentes processos ou threads precisam acessar um mesmo recurso compartilhado, é necessário estabelecer regras para organizar esse acesso e evitar que uma operação interfira indevidamente em outra. Sem esse controle, o sistema pode apresentar falhas, inconsistências e resultados diferentes daqueles esperados. Por esse motivo, compreender o funcionamento da concorrência é essencial para entender não apenas como os sistemas são executados, mas também quais cuidados precisam ser adotados durante o desenvolvimento de aplicações confiáveis. Para demonstrar essa situação de maneira prática, será utilizado como exemplo um sistema de venda de ingressos para um grande show de rock. Imagine que milhares de pessoas estejam aguardando o início das vendas e que dois usuários tentem comprar praticamente ao mesmo tempo o assento A-15. Se o sistema permitir que ambos consultem a disponibilidade desse lugar antes que a primeira compra seja efetivamente registrada, os dois poderão receber a informação de que o assento está livre. Caso as solicitações não sejam controladas corretamente, existe o risco de o sistema confirmar duas compras para um único lugar, provocando transtornos para os compradores e prejuízos para a organização do evento. Esse cenário representa um problema conhecido como condição de corrida, que acontece quando o resultado de uma operação depende da ordem ou do momento em que diferentes execuções acessam e modificam um recurso compartilhado. Embora o exemplo utilizado esteja relacionado à compra de ingressos, esse tipo de situação também pode ocorrer em sistemas bancários, plataformas de comércio eletrônico, aplicações de reservas e outros serviços que precisam processar várias solicitações simultaneamente. Dessa maneira, percebe-se que a concorrência não deve ser tratada apenas como uma questão de desempenho, mas também como um aspecto importante para garantir a consistência dos dados e o funcionamento correto das aplicações. Diante desse problema, torna-se necessário compreender os mecanismos utilizados para organizar a execução das tarefas e controlar o acesso aos recursos compartilhados. Entre os conceitos importantes nesse contexto estão a sincronização, a exclusão mútua e as regiões críticas. A sincronização permite coordenar diferentes execuções, enquanto a exclusão mútua busca garantir que somente uma execução por vez acesse determinado trecho protegido do código. Já a região crítica corresponde ao trecho da execução em que ocorre o acesso a um recurso compartilhado e que, por isso, precisa de proteção adequada para evitar conflitos.

Outro aspecto importante abordado neste trabalho é a diferença entre threads em modo usuário e threads em modo núcleo, também conhecido como kernel. Esses modelos apresentam características distintas em relação ao gerenciamento, ao escalonamento e à participação do Sistema Operacional no controle das linhas de execução. Compreender essas diferenças ajuda a identificar como as aplicações podem organizar suas tarefas e quais fatores influenciam o desempenho, o consumo de recursos e a capacidade de executar atividades simultaneamente. Além disso, será discutida a importância das threads em aplicações que precisam atender a um grande volume de usuários, como no caso da venda de ingressos. Em uma situação na qual milhares de pessoas acessam uma plataforma ao mesmo tempo, a maneira como as solicitações são organizadas pode influenciar diretamente o uso dos recursos do computador e a capacidade de resposta do sistema. As threads podem contribuir para esse processamento concorrente, mas seu uso precisa estar acompanhado de mecanismos adequados de sincronização sempre que houver compartilhamento de dados ou recursos que não podem ser modificados de maneira descontrolada. Portanto, este trabalho tem como objetivo analisar os conceitos apresentados na Aula 7 de Sistemas Operacionais, relacionando os fundamentos teóricos de processos, threads e concorrência a uma situação prática que pode ocorrer em sistemas utilizados no cotidiano. A partir do exemplo do assento A-15, busca-se demonstrar como a ausência de controle sobre operações simultâneas pode comprometer o funcionamento de uma aplicação e como a utilização adequada de mecanismos de sincronização pode evitar resultados incorretos. Assim, o estudo pretende contribuir para uma compreensão mais clara da importância do gerenciamento de processos e threads, mostrando que o desenvolvimento de um sistema eficiente depende não apenas da velocidade de execução, mas também da capacidade de garantir a integridade, a organização e a confiabilidade das operações realizadas.

# 2. DESENVOLVIMENTO

## 2.1. Síntese Teórica (Pesquisa)

Um processo pode ser entendido como um programa em execução e como um agrupamento dos recursos necessários para que esse programa funcione. Baseado na aula 7, o processo possui espaço de endereçamento, uma linha de execução, resentado por uma thread. Entre os recursio de um processo estão o código e os dados do programa, arquivos abertos e outras informações utilizadas pelo sistema operacional.

Uma Thread, representa uma linha de execução dentro de um processo. No processo pode possuir várias threads, permitindo que diferentes atividades sejam executadas de maneira concorrente. As Threads, representam as linhas de execução do programa. Um processo pode ter apenas uma Threads ou várias Threads executando tarefas ao mesmo tempo. As Threads de um processo compartilham o espaço de endereçamento e diversos recursos do processo, possuindo informações próprias para controlar a sua execução, como contados de programa(PC), registradores e pilha. Em outros materias como o da microsft, define o processo como a estrutura possui o espaço virtual, o código e recursos do sistema. Já as Thread, ele define sendo unidades que podem ser escalonadas para receber o tempo de processamento.

### 2.1.1. Porque as threads são mais leves para o Sistema Operacional?

As Threads de um processo, vão compartilhar o espaço de endereçamento. Dessa forma, várias Threads irão utilizar o mesmo código, dados globaise outros recursos do processo, enquanto cada thread deixa suas informaçõe particulares de execução, como sua pilha e seus registradores. Com isso, vai reduzir o custo de criação e o gerenciamento comparado á criação de vários outros processos. Threads no modo geral, são mais rápidas de criar e destruir que processos.

No caso, se 100.00 usuários entrarem no site no momento da abertura das vendas. Para tratar das solicitações simultaneas, uma abordagem de processos será usada para criar uma grande quantidade de processos independentes. Cada processo terá seu espaço de endereçamento e estruturas de gerenciamento, aumentando o consumo de recursos e o trabalho do sistema operacional. Utilizando as Threads, as linhas de execução serão organizadas dentro de processos servidores, para que, elas compartilhem o espaço de endereçamento do processo e evitando manter um espaço de endereçamento completamente independente para cada linha.

## 2.2. Threads em modo usuário e modo kernel

### 2.2.1. Threads em modo usuário

As threads no modo usuário serão implementadas normalmente por meio de uma biblioteca de execução. A criação, a exclusão e o escalonamento dessas Threads podem ocorrer sem que o kernel tenha conhecimento individual de cada uma delas.

### 2.2.2. Threads em Modo Núcleo (Kernel)

Nas Threads em Modo Núcleo, o próprio Sistema Operacional possui informações sobre as Threads e participa diretamente do seu gerenciamento e escalonamento.

### 2.2.3. Comparação entre Threads em Modo Usuário e Modo Núcleo

| Característica | Modo Usuário | Modo Núcleo (Kernel) |
|---|---|---|
| *Gerenciamento* | Biblioteca ou ambiente de execução | Sistema Operacional |
| *Kernel conhece as Threads individualmente?* | Não necessariamente | Sim |
| *Escalonamento* | Feito no espaço do usuário | Feito pelo kernel |
| *Custo de gerenciamento* | Geralmente menor | Geralmente maior |
| *Bloqueio de uma Thread* | Pode afetar outras Threads, dependendo da implementação | Outras Threads podem continuar executando |
| *Paralelismo em múltiplos processadores* | Depende do modelo utilizado | Suportado diretamente pelo escalonamento do kernel |

## 2.3. Diagnóstico do Problema (O gargalo)

Condição de corrida ocorre quando duas ou mais operações acessam um unico recurso compartilhado ao mesmo tempo, gerando resultados incorretos e erros. Como no caso do show de rock, dois usuários tentam comprar o mesmo assento A-15. Caso o sistema não consiga controlar essas operações, ele pode confirmar as duas comprtas para uma única cadeira. Porém para evitar esse tipo de ocorrência, pode-se utilizar a exclusão mútua ou seja ela controla o acesso à região crítica e garante apenas uma compra seja confirmada para aquele determinado assento. Portanto para evitar condições de corrida é viavel utilizar métodos de sincronização apropriados como, locks, semáforos ou operações atômicas, são colocados para garantir que apenas um processo ou thread possa acessar os dados compartilhados em um dado momento.

## 2.4. A Solução Arquitetural

A Solução Arquitetural:

Para resolver este problema , é necessário utilizar um mecanismo de sincronização que controle esses acessos simultâneos dos usuários ao mesmo assento. Conforme apresentado na aula 7, a sincronização permite coordenar a execução de diferentes processos ou threads que compartilham recusros, evitando conflitos e resultados incorretos. Como no caso do assento A-15, os usuários A e B tentam realizar a compra praticamente simultâniamente. Caso o sistema não consiga controlar essas solicitações, os dois usuários poderão verificar que o assento está disponível antes que a primeira comptra seja registrada, possibilitando uma venda dupliacada. Para evitar este probelma, o sistema deve-se organizar o processamento das solicitações e garantir que a disponibilidde do assento seja verificada novamente no momento de confirma a compra. Quando for feita a primeira reserva, a disponibilidade do asento deverá ser atualizada. Sendo assim, quando outro usuário for comprar, o sistema identificará que a cadeira ja está ocupada. Portanto o controle da concorrência garante a integridade das informações, evitando reservas dupliacadas e permitindo que o sistema funcione corretamente mesmo quando vários outros usuários tentam comprar ingressos ao mesmo tempo. Entretanto todavia o conceito de região crítica se encaixa para eliminar está condição de corrida, pois é simples basta garantir a exclusão mútua na execução dos trechos críticos dos processos.

# 3. CONCLUSÃO

A partir do desenvolvimento deste trabalho, foi possível compreender a importância dos processos e das threads no funcionamento dos Sistemas Operacionais, relacionando os conceitos estudados na Aula 7 a uma situação prática de concorrência. A pesquisa permitiu analisar como os processos organizam os recursos necessários à execução de programas e como as threads possibilitam a realização de diferentes atividades dentro de um mesmo processo. Também foi possível compreender as diferenças entre threads em modo usuário e em modo núcleo, considerando aspectos como gerenciamento, escalonamento, custo e paralelismo. Esses conceitos ajudam a entender como as aplicações podem organizar suas tarefas e utilizar os recursos computacionais.

A análise do cenário de venda de ingressos demonstrou como a condição de corrida pode comprometer a confiabilidade de um sistema. No exemplo do assento A-15, a ausência de controle sobre as operações simultâneas poderia permitir que dois usuários recebessem a confirmação de compra do mesmo lugar. Para evitar esse problema, foram abordados os conceitos de sincronização, exclusão mútua e região crítica, que contribuem para organizar o acesso aos recursos compartilhados e impedir resultados inconsistentes. Dessa forma, considera-se que os objetivos propostos foram alcançados, pois o trabalho apresentou os conceitos teóricos, identificou o problema de concorrência e relacionou uma possível solução ao cenário analisado. A pesquisa bibliográfica e a análise do exemplo prático foram adequadas para relacionar os conteúdos estudados ao funcionamento de sistemas utilizados no cotidiano. Conclui-se que o gerenciamento correto de processos e threads é importante não apenas para o desempenho, mas também para a integridade e a confiabilidade das aplicações. O uso adequado de mecanismos de sincronização permite controlar operações simultâneas e reduzir o risco de inconsistências, contribuindo para o funcionamento correto de sistemas que atendem a muitos usuários.

# 4. REFERÊNCIAS BIBLIOGRÁFICAS

DOS SANTOS, Wildson Luiz Pereira. Aspectos sócio-científicos em aulas de química. Disponível em: <https://www.semanticscholar.org/paper/38c534baf8fadbe2b2d91da27c546cd93c8d3fdc>. Acesso em: 8 out. 2026.

GOMES, Pedro Demarchi; GARCIA, Islene Calciolari. Análise de desempenho e propostas de melhoria para as Transparent Huge Pages do kernel Linux. Thesis—[S.l.: S.n.], 2025.

CASTAGNA, Marcia. Devs e devas, vocês sabem o que é RACE CONDITION?. Disponível em: <https://pt.linkedin.com/pulse/devs-e-devas-voc%C3%AAs-sabem-o-que-%C3%A9-race-condition-marcia-castagna>. Acesso em: 9 out. 2026.