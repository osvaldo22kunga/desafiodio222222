# desafiodio222222
Entrega do Desafio

1. Introdução
A primeira parte do curso serve para estabelecer as bases da segurança ofensiva e explicar por que razão as palavras-passe continuam a ser um dos principais alvos dos atacantes.

A segurança ofensiva consiste em testar sistemas de forma controlada para identificar vulnerabilidades antes que pessoas mal-intencionadas as explorem. É aqui que entram o penetration testing (teste de intrusão), a auditoria de segurança e o ethical hacking.

Durante este curso, trabalhamos principalmente com três elementos:
- Kali Linux: sistema operacional que disponibiliza ferramentas de auditoria e testes de segurança.
- Metasploitable 2: máquina virtual intencionalmente vulnerável, utilizada para praticar num ambiente isolado.
- Credenciais: nomes de utilizador, palavras-passe e outros mecanismos utilizados para confirmar a identidade de alguém.
O objetivo não é apenas aprender comandos. É perceber como um atacante identifica um serviço, reconhece um mecanismo de autenticação, procura falhas e como um profissional de defesa pode detetar e impedir esse comportamento.
2. Principais tipos de ataques
Antes de utilizar ferramentas, precisamos de compreender as técnicas que elas podem apoiar.









Força bruta (Brute Force)

Consiste em testar diferentes palavras-passe até encontrar uma combinação válida. Dependendo da ferramenta e do alvo, as tentativas podem ser feitas contra um serviço ou contra hashes de palavras-passe obtidos anteriormente.












Credential Stuffing

Utiliza pares de utilizador e palavra-passe que foram expostos numa fuga de dados para verificar se as mesmas credenciais foram reutilizadas noutro serviço. O problema central é a reutilização de palavras-passe.












Password Spraying

Testa um pequeno número de palavras-passe comuns em várias contas, em vez de experimentar muitas palavras-passe numa única conta. Isso pode reduzir a probabilidade de atingir os limites de bloqueio por conta, mas continua a poder ser detetado pelos sistemas de segurança.












Ataques contra formulários Web

Procuram identificar falhas na autenticação de aplicações Web, como políticas de palavras-passe fracas, ausência de limitação de tentativas ou mensagens de erro que revelam a existência de contas.



Há ainda ataques por engenharia social, phishing, exploração de serviços vulneráveis e roubo de sessões. Cada um tem mecanismos diferentes, mas todos podem comprometer a identidade digital de um utilizador.

A principal lição é que uma palavra-passe forte, isoladamente, não resolve todos os problemas: também são necessárias autenticação multifator, monitorização, proteção das sessões e políticas adequadas de acesso.
3. Password Spraying e Credential Stuffing
Estes dois conceitos são fundamentais porque demonstram que os problemas de autenticação nem sempre resultam de uma palavra-passe tecnicamente fraca.
Password Spraying
Imagina uma empresa com 100 funcionários. Um atacante descobre os nomes de utilizador e verifica se existe uma política de palavras-passe fraca.

Em vez de experimentar centenas de palavras-passe numa conta, a técnica de Password Spraying consiste em testar poucas palavras-passe comuns em diferentes contas.

Exemplo conceptual:
- Conta A: uma palavra-passe candidata.
- Conta B: a mesma palavra-passe candidata.
- Conta C: a mesma palavra-passe candidata.
O risco é a utilização de palavras-passe previsíveis. Mesmo que uma organização limite as tentativas por conta, tentativas distribuídas podem escapar a uma deteção simplista.

Como prevenir: autenticação multifator (MFA), bloqueios inteligentes, deteção de tentativas distribuídas, palavras-passe proibidas e monitorização dos registos de autenticação.
Credential Stuffing
Aqui, o cenário é diferente. O atacante já possui pares de credenciais provenientes de uma fuga de dados e tenta verificar se os utilizadores reutilizaram as mesmas credenciais noutros serviços.

Por exemplo, alguém utiliza a mesma palavra-passe no correio eletrónico e numa rede social. Se uma das plataformas sofrer uma fuga de dados, a reutilização pode colocar a outra conta em risco.

Diferença principal:
Técnica	O que é utilizado
Password Spraying	Poucas palavras-passe candidatas em várias contas
Credential Stuffing	Pares de credenciais previamente expostos
Força bruta	Muitas combinações possíveis para encontrar uma válida

No laboratório, o objetivo é reconhecer os padrões dessas técnicas e compreender como os registos de autenticação ajudam a identificar comportamentos suspeitos.
4. Hydra no Kali Linux









Hydra

O Hydra é uma ferramenta de testes de autenticação que suporta vários protocolos e serviços, como SSH, FTP e alguns serviços Web. É utilizada para avaliar a resistência dos mecanismos de autenticação em testes autorizados.


Como funciona?
O Hydra comunica com um serviço de autenticação e verifica se as credenciais fornecidas são aceites. O comportamento exato depende do protocolo, da configuração do serviço e do módulo utilizado.

Por exemplo, num laboratório, podemos estudar um servidor SSH configurado intencionalmente para permitir autenticação por palavra-passe. A auditoria procura determinar se as proteções implementadas são adequadas.
Como reconhecer a ferramenta
No Kali Linux, podes consultar a ajuda e os protocolos disponíveis:
hydra -h


Para verificar a versão instalada:
hydra -v


A ajuda permite conhecer os parâmetros, os módulos e as opções de controlo.
O que deves explicar como formador
1. O Hydra não descobre magicamente todas as palavras-passe.
2. A sua eficácia depende do serviço, dos dados testados e das proteções existentes.
3. Tentativas excessivas podem gerar alertas, bloqueios e registos de segurança.
4. O resultado da ferramenta deve ser confirmado e documentado.
5. A ausência de sucesso não prova que um sistema é seguro.
Lição defensiva: limitar tentativas, utilizar MFA, desativar autenticação por palavra-passe quando apropriado e monitorizar falhas repetidas de autenticação.
5. Ncrack no Kali Linux









Ncrack

O Ncrack é uma ferramenta de auditoria de autenticação de serviços de rede, desenvolvida para avaliar a resistência de mecanismos de login em protocolos suportados.


Para que serve?
Enquanto o Nmap é amplamente conhecido pela descoberta de hosts, portas e serviços, o Ncrack concentra-se nos mecanismos de autenticação dos serviços que suporta.

Por exemplo, durante uma auditoria autorizada, o profissional pode identificar um serviço remoto acessível e, depois de obter autorização específica, avaliar a sua configuração de autenticação.

Para consultar a ajuda:
ncrack --help


O que deves saber
- A porta aberta não significa que o acesso foi comprometido.
- Um serviço acessível pode ter uma autenticação forte.
- A velocidade das tentativas deve ser controlada para não prejudicar a disponibilidade.
- O resultado deve ser interpretado em conjunto com os registos do servidor.
Diferença entre Hydra e Ncrack: ambos podem avaliar autenticação em serviços suportados, mas têm opções, módulos e características operacionais diferentes. Não deves assumir que todos os protocolos ou comportamentos são iguais nas duas ferramentas.
6. John the Ripper no Kali Linux









John the Ripper

O John the Ripper é utilizado para avaliar a resistência de palavras-passe através da análise de hashes. É diferente das ferramentas que testam diretamente o login num serviço remoto.


O que é um hash?
Um hash é o resultado de uma função matemática aplicada a dados. Nos sistemas de autenticação, as palavras-passe devem ser armazenadas através de mecanismos apropriados de derivação e hashing, em vez de serem guardadas em texto simples.

Quando um utilizador inicia sessão, o sistema verifica a palavra-passe fornecida através do processo de autenticação configurado.

Durante uma auditoria offline autorizada, o John pode comparar candidatos de palavras-passe com os hashes disponíveis.
Exemplo de utilização segura
Consulta a versão:
john --list=build-info


Consulta os formatos suportados:
john --list=formats


Estes comandos permitem conhecer a instalação e os formatos disponíveis sem iniciar um ataque a contas.
O que deves explicar aos alunos
- Hash não é sinónimo de encriptação: normalmente, não se descodifica diretamente um hash.
- Um hash rápido e inadequado pode facilitar a descoberta de palavras-passe por tentativa.
- Algoritmos próprios para palavras-passe, como Argon2id, scrypt ou configurações apropriadas de bcrypt, tornam as tentativas mais dispendiosas.
- O salt individual ajuda a impedir que hashes iguais revelem diretamente palavras-passe iguais e dificulta ataques com tabelas pré-computadas.
Lição defensiva: avaliar o algoritmo de armazenamento, a força das palavras-passe e a existência de credenciais comprometidas, sem expor dados reais dos utilizadores.
7. WPScan no Kali Linux









WPScan

O WPScan é um scanner especializado em WordPress. Ajuda a identificar versões, componentes, temas, plugins e possíveis problemas de segurança.


O que é WordPress?
É um sistema de gestão de conteúdos (CMS) utilizado para criar websites, portais, blogs e lojas online.

Um website WordPress pode apresentar riscos quando utiliza plugins desatualizados, temas vulneráveis, configurações incorretas ou contas com privilégios excessivos.
Como consultar a ferramenta
wpscan --version


Para consultar as opções:
wpscan --help


O que analisar numa auditoria
1. Versão do WordPress e respetivo estado de atualização.
2. Plugins e temas instalados.
3. Exposição de informações desnecessárias.
4. Configuração das contas administrativas.
5. Alertas de vulnerabilidades conhecidos.
O WPScan também dispõe de funcionalidades de auditoria de autenticação. Essas funcionalidades devem ser usadas apenas quando estiverem expressamente autorizadas e dentro dos limites definidos para o teste.

Importante: encontrar um plugin ou uma versão antiga não significa automaticamente que o website esteja vulnerável. É necessário confirmar a versão, as condições de exploração e a existência de medidas de mitigação.
8. Patator no Kali Linux









Patator

O Patator é uma ferramenta modular de testes que pode automatizar diferentes tipos de verificações, incluindo testes de autenticação em serviços suportados.


Como funciona?
A ferramenta organiza os testes através de módulos e parâmetros. Isso permite adaptar uma auditoria ao tipo de serviço, às respostas recebidas e às condições definidas para o ensaio.

O seu caráter modular torna importante compreender o que cada parâmetro controla. Uma configuração incorreta pode provocar um volume excessivo de pedidos ou interpretar incorretamente as respostas do serviço.

Para conhecer a instalação:
patator --help


Se a instalação disponibilizar um comando diferente ou não reconhecer essa opção, consulta o manual e os ficheiros de documentação da versão instalada.
Quando faz sentido utilizá-lo?
- Em laboratórios de testes de autenticação.
- Na validação controlada de políticas de segurança.
- Em testes repetíveis, com parâmetros bem documentados.
- Na investigação de respostas diferentes entre pedidos válidos e inválidos.
O que deves destacar: automatizar testes não substitui a compreensão do protocolo. O profissional precisa de saber interpretar os resultados e evitar falsos positivos.
9. Ambiente com Kali Linux e Metasploitable 2
Esta é uma das partes mais importantes do curso, porque transforma a teoria num laboratório prático.




















5








Papel de cada máquina
- Kali Linux: máquina de auditoria, na qual executamos as ferramentas.
- Metasploitable 2: alvo de laboratório deliberadamente vulnerável, que disponibiliza serviços inseguros para fins educativos.
- VirtualBox: software de virtualização que permite executar as duas máquinas no mesmo computador.
Como funciona a comunicação?
Cada máquina virtual precisa de uma interface de rede configurada para que a comunicação ocorra. Num laboratório isolado, uma rede Host-Only permite que as máquinas virtuais comuniquem com o anfitrião e, conforme a configuração, entre si, sem lhes proporcionar necessariamente acesso à Internet.

Uma rede NAT pode proporcionar acesso à Internet, mas a comunicação entre máquinas depende da configuração de rede escolhida.

Para confirmar os endereços de rede no Kali:
ip -br addr


Para consultar as rotas:
ip route


No Metasploitable 2, consulta também o endereço IP atribuído à interface de rede.
O que verificar antes dos testes
1. As duas máquinas estão ligadas.
2. As interfaces estão na rede pretendida.
3. O endereço IP de cada máquina está correto.
4. O laboratório não está inadvertidamente exposto à rede pública.
5. Existe um snapshot para recuperar o estado inicial.
Não deves confundir conectividade com vulnerabilidade. Conseguir comunicar com uma máquina não significa ter autorização para aceder aos seus serviços, nem prova que esses serviços estão vulneráveis.
10. Alcançando a máquina vulnerável no Metasploitable 2
Nesta fase, o objetivo é confirmar que o Kali consegue comunicar com o alvo.

Primeiro, identifica o endereço IP do Metasploitable 2. Depois, testa a conectividade usando o endereço correto:
ping -c 4 IP_DO_METASPLOITABLE


Substitui IP_DO_METASPLOITABLE pelo endereço real da máquina de laboratório.

Se não houver resposta, verifica:
- Se as máquinas estão na mesma rede virtual.
- Se o endereço IP foi atribuído corretamente.
- Se a interface de rede está ativa.
- Se existe uma rota adequada.
- Se o sistema de destino bloqueia respostas ICMP.
A ausência de resposta ao ping não prova que a máquina está desligada. O ICMP pode estar bloqueado, embora outros serviços estejam acessíveis.
Descoberta de serviços
O Nmap pode ser usado, com autorização, para identificar portas e serviços expostos no alvo de laboratório.
nmap -sV IP_DO_METASPLOITABLE


A opção -sV tenta identificar as versões dos serviços detetados.

Os resultados ajudam a construir um inventário técnico. Por exemplo, podem revelar serviços FTP, SSH ou HTTP, dependendo da configuração do sistema.

Objetivo pedagógico: aprender a relacionar uma porta, o serviço correspondente, a versão detetada e o risco potencial, sem concluir automaticamente que qualquer serviço aberto constitui uma falha.
11. Criando ficheiros de utilizadores e palavras-passe comuns
Uma wordlist é um ficheiro de texto que contém palavras ou outros valores candidatos utilizados em testes de segurança.

Uma lista de utilizadores contém identificadores de contas. Uma lista de palavras-passe contém candidatos que podem ser avaliados num laboratório.
Por que são importantes?
As listas permitem reproduzir cenários de auditoria, verificar políticas de palavras-passe e estudar o impacto de escolhas previsíveis.

Por exemplo, um laboratório pode utilizar contas fictícias como aluno01 e aluno02, com credenciais criadas exclusivamente para a demonstração.

Para criar um diretório destinado aos materiais do laboratório:
mkdir -p ~/laboratorio/wordlists


Para criar um ficheiro de teste com valores fictícios:
nano ~/laboratorio/wordlists/utilizadores.txt


Guarda apenas os utilizadores de teste nesse ficheiro.
Cuidados essenciais
- Não coloques palavras-passe pessoais ou reais em listas de demonstração.
- Não utilizes ficheiros de credenciais obtidos de terceiros sem autorização.
- Controla o número de candidatos e as condições do teste.
- Protege os resultados da auditoria, porque podem conter informações sensíveis.
A aprendizagem principal é perceber que a qualidade de um teste depende tanto dos dados utilizados como da ferramenta escolhida.
12. Ataques de força bruta em formulários de login Web
Nesta aula, estudamos como funciona a autenticação num website e quais são as falhas que podem permitir tentativas excessivas de login.

Quando um utilizador preenche um formulário, o navegador envia um pedido ao servidor. O servidor valida as credenciais e devolve uma resposta, como sucesso, falha ou pedido de verificação adicional.
O que um auditor procura avaliar?
- Se existe limitação de tentativas.
- Se o sistema aplica atrasos progressivos quando ocorrem falhas.
- Se as mensagens de erro revelam se determinado utilizador existe.
- Se a autenticação multifator está disponível.
- Se os registos permitem detetar comportamentos anormais.
Uma ferramenta de testes Web precisa de compreender como o formulário envia os dados, quais os campos utilizados e como as respostas são interpretadas. Formulários que utilizam tokens CSRF, cookies ou mecanismos adicionais de autenticação exigem cuidados específicos.

Num laboratório autorizado, podes utilizar um formulário de demonstração com contas fictícias para observar a diferença entre uma tentativa válida e uma tentativa inválida.

O ponto fundamental: não basta descobrir se uma palavra-passe funciona. É necessário avaliar se o sistema protege adequadamente o processo de autenticação.
13. Criação de wordlists
Esta aula aprofunda a construção e a utilização de listas de palavras.

Uma wordlist pode ser criada manualmente ou gerada a partir de regras e padrões definidos. A sua qualidade depende do objetivo da auditoria e das características do ambiente avaliado.
Tipos de listas
Tipo	Finalidade
Lista de utilizadores	Identificar contas fictícias do laboratório
Lista de palavras-passe de teste	Avaliar uma política de autenticação
Lista de padrões	Estudar previsibilidade e complexidade
Lista de combinações	Avaliar conjuntos de candidatos num teste controlado

Para veres o conteúdo de uma lista criada anteriormente:
cat ~/laboratorio/wordlists/utilizadores.txt


Para contar as linhas:
wc -l ~/laboratorio/wordlists/utilizadores.txt


Estes comandos ajudam a verificar se o ficheiro contém os dados esperados.
Como explicar a importância das wordlists?
Uma lista muito grande não é necessariamente uma lista melhor. Se os candidatos não forem adequados ao cenário, o aumento do volume pode apenas tornar o teste mais lento e ruidoso.

Num exercício profissional, define primeiro o objetivo, o conjunto de contas fictícias, o limite de tentativas e os critérios para interromper o teste.
14. Utilizando o Medusa para simular combinações de acesso









Medusa

O Medusa é uma ferramenta de auditoria de autenticação que suporta vários módulos de serviços de rede e permite testar credenciais em cenários autorizados.


O seu papel no curso
O Medusa permite estudar como as tentativas de autenticação se comportam em diferentes serviços suportados. É útil para compreender como os sistemas reagem a falhas repetidas e como a atividade é registada.

Para consultar as opções da versão instalada:
medusa -h


O que deves observar num laboratório?
1. A resposta do serviço perante credenciais inválidas.
2. A forma como as falhas são registadas.
3. A existência de limites de tentativas.
4. A diferença entre uma conta bloqueada e um serviço indisponível.
5. O impacto da concorrência e do volume de pedidos.
Hydra, Medusa e Ncrack: são a mesma coisa?
Não. As três ferramentas têm funcionalidades sobrepostas, mas diferem nos módulos, na sintaxe, nas opções de execução e nas características de funcionamento.

Um bom profissional não escolhe uma ferramenta apenas porque é popular. Escolhe-a conforme o protocolo, o objetivo da auditoria, a autorização concedida e os limites operacionais do teste.
15. Ataque em cadeia: enumeração SMB e Password Spraying
Esta aula combina duas etapas de uma auditoria: a identificação de informações expostas por SMB e a avaliação das políticas de autenticação.
O que é SMB?
O Server Message Block (SMB) é um protocolo utilizado, principalmente, para partilhar ficheiros, diretórios e outros recursos em redes.

Em ambientes Windows, o SMB pode permitir acesso a partilhas, desde que as permissões e a autenticação o autorizem.
O que significa enumeração SMB?
A enumeração consiste em recolher informações sobre os serviços e recursos disponibilizados por SMB. Dependendo das permissões e da configuração, podem ser identificadas partilhas, nomes de recursos e outras informações.

O problema surge quando o serviço revela mais informações do que deveria ou permite acesso desnecessário a recursos.
E o Password Spraying?
Depois de compreender o serviço e as suas políticas de acesso, um auditor pode avaliar, mediante autorização explícita, se a organização utiliza mecanismos de autenticação suficientemente resistentes.

A sequência conceptual é:
1. Identificação do serviço SMB


2. Verificação de recursos e permissões


3. Avaliação controlada da autenticação


4. Análise dos registos e recomendações


O objetivo é verificar se existem permissões excessivas, configurações inseguras ou falhas de deteção. A enumeração, por si só, não concede acesso a uma partilha protegida.

Lição defensiva: restringir o SMB às redes necessárias, desativar protocolos antigos, aplicar permissões mínimas e monitorizar autenticações suspeitas.
16. Simulando um cenário corporativo mal configurado
Aqui, o curso deixa de analisar apenas ferramentas individuais e passa a estudar um cenário completo.

Imagina uma empresa fictícia com:
- Um servidor Linux vulnerável.
- Serviços de rede desnecessariamente expostos.
- Contas de teste com palavras-passe previsíveis.
- Uma partilha SMB com permissões inadequadas.
- Monitorização de segurança insuficiente.
O objetivo do exercício é demonstrar como pequenas falhas podem combinar-se e aumentar o risco global.
Como conduzir a simulação?
Primeira etapa — Reconhecimento: identificar a máquina de laboratório e os serviços disponibilizados.

Segunda etapa — Análise: compreender quais os serviços necessários e quais estão desnecessariamente expostos.

Terceira etapa — Auditoria: verificar as configurações de autenticação e permissões, sem ultrapassar o âmbito autorizado.

Quarta etapa — Deteção: analisar os registos e procurar evidências de tentativas repetidas, acessos anormais ou enumeração.

Quinta etapa — Correção: aplicar atualizações, remover serviços desnecessários, corrigir permissões e reforçar a autenticação.
Como avaliar o resultado?
Uma auditoria bem-sucedida não é necessariamente aquela em que se obtém acesso. É aquela que consegue demonstrar os riscos de forma reproduzível, identificar as causas e propor medidas concretas de correção.

No relatório, deves distinguir claramente entre vulnerabilidade confirmada, risco potencial e hipótese ainda não validada.
17. Criando uma lista de utilizadores
Esta aula aprofunda a identificação e a organização de contas num ambiente de laboratório.

Em qualquer sistema, os utilizadores possuem identidades e permissões. Uma auditoria procura determinar se essas contas estão corretamente configuradas e se os seus privilégios correspondem às funções que desempenham.
O que deves ensinar?
- Nomes de utilizador: identificadores associados às contas.
- Privilégios: ações que cada conta pode realizar.
- Grupos: conjuntos de utilizadores com permissões semelhantes.
- Contas inativas: contas que já não deveriam ter acesso.
- Contas de serviço: identidades utilizadas por aplicações e processos.
Num laboratório, podes manter uma lista de contas fictícias e documentar os respetivos privilégios.

Por exemplo:
Utilizador fictício	Função	Permissão prevista
aluno01	Estudante	Acesso limitado
tecnico01	Técnico	Acesso aos recursos técnicos autorizados
adminlab	Administrador de laboratório	Administração do ambiente de teste

A tabela representa apenas um exemplo. As permissões reais dependem da configuração do sistema.

Lição principal: conhecer um nome de utilizador não significa ter autorização para entrar na conta. A gestão de identidades deve seguir o princípio do menor privilégio.
18. Testando o acesso utilizando SMBclient









smbclient

O smbclient é um cliente de linha de comandos que permite ligar-se a partilhas SMB, listar recursos e trabalhar com ficheiros, conforme as permissões concedidas.


Para que serve?
Imagina que um servidor disponibiliza uma partilha de ficheiros para uma equipa. O administrador precisa de confirmar se os utilizadores autorizados conseguem aceder aos recursos e se os restantes são corretamente impedidos.

O smbclient permite realizar essa verificação.

Para consultar as opções disponíveis:
smbclient --help


Para verificar a versão:
smbclient --version


O que deve ser testado?
1. Se a partilha existe.
2. Se a autenticação funciona para uma conta autorizada.
3. Se as permissões de leitura e escrita correspondem ao esperado.
4. Se os utilizadores não autorizados são impedidos de aceder.
5. Se o servidor regista as tentativas de acesso.
O acesso a uma partilha pode ser autorizado mesmo quando o utilizador não tem permissão para alterar ficheiros. Por isso, leitura e escrita devem ser verificadas separadamente.

Lição defensiva: aplicar permissões mínimas, exigir autenticação apropriada e impedir partilhas anónimas quando não são necessárias.
19. Encerramento do curso
No encerramento, o objetivo é consolidar os conceitos e verificar se os participantes conseguem relacionar ferramentas, vulnerabilidades e medidas de proteção.

Ao concluir o curso, o participante deverá compreender:
- A diferença entre força bruta, Password Spraying e Credential Stuffing.
- O funcionamento geral do Hydra, Ncrack, John the Ripper, WPScan, Patator e Medusa.
- A finalidade do Kali Linux e do Metasploitable 2 no laboratório.
- A identificação de serviços e a interpretação de portas abertas.
- A utilização de wordlists em auditorias controladas.
- O funcionamento básico de SMB e a utilização do smbclient.
- A importância dos registos de autenticação e da resposta a incidentes.
- A elaboração de recomendações de segurança fundamentadas.
Uma competência importante é saber explicar por que razão uma vulnerabilidade constitui um risco e qual é a correção mais adequada. Memorizar comandos não é suficiente para trabalhar profissionalmente em cibersegurança.
20. Aula extra: limitações do Medusa e dicas finais
O Medusa, tal como outras ferramentas de auditoria de autenticação, apresenta limitações que devem ser compreendidas antes de se interpretar um resultado.
Limitações
- Compatibilidade: nem todos os protocolos ou serviços são suportados da mesma maneira.
- Configuração do alvo: diferenças entre serviços e mecanismos de autenticação podem afetar o resultado.
- Bloqueios e limites: os sistemas podem limitar tentativas, introduzir atrasos ou bloquear contas.
- Falsos positivos e falsos negativos: uma resposta inesperada pode ser interpretada incorretamente.
- Impacto operacional: pedidos excessivos podem prejudicar o serviço.
- Qualidade dos dados: uma lista de candidatos inadequada limita a utilidade da auditoria.
Boas práticas profissionais
1. Define o âmbito e obtém autorização antes do teste.
2. Usa contas e máquinas de laboratório.
3. Estabelece limites de tentativas e condições para interromper o exercício.
4. Guarda os registos relevantes.
5. Protege os dados recolhidos.
6. Documenta as limitações da ferramenta.
7. Apresenta recomendações de correção.
A escolha da ferramenta depende do serviço, do objetivo e do âmbito da auditoria. Não existe uma única ferramenta ideal para todas as situações.
21. Entendendo o desafio final
O desafio final deve demonstrar que o participante consegue aplicar o conhecimento de forma estruturada, desde o reconhecimento até à elaboração de um relatório.
Projeto final: auditoria de autenticação
Ambiente: Kali Linux + Metasploitable 2, em rede de laboratório isolada.
1. Preparar as máquinas virtuais e confirmar a conectividade.
2. Identificar os serviços disponíveis no alvo autorizado.
3. Documentar os riscos associados aos serviços e às configurações encontradas.
4. Estudar as políticas de autenticação e as limitações das ferramentas apresentadas.
5. Verificar as permissões de acesso a recursos de laboratório.
6. Rever os registos e identificar evidências de comportamentos suspeitos.
7. Propor correções e elaborar um relatório técnico.

Estrutura do relatório final
O relatório deve conter:
- Objetivo: o que se pretende avaliar.
- Âmbito: máquinas, serviços e contas de teste autorizados.
- Metodologia: ferramentas e procedimentos utilizados.
- Resultados: observações e evidências recolhidas.
- Riscos: impacto e probabilidade de cada problema identificado.
- Recomendações: ações necessárias para corrigir as falhas.
- Conclusão: estado geral da segurança e próximos passos.
Como avaliar os participantes
Critério	Peso sugerido
Preparação e isolamento do laboratório	15%
Reconhecimento e identificação de serviços	20%
Compreensão das ferramentas e da autenticação	25%
Interpretação de resultados e registos	20%
Relatório técnico e recomendações	20%

A avaliação deve privilegiar o raciocínio, a segurança do procedimento e a capacidade de justificar as conclusões.

Resumo final das ferramentas

Hydra

Testes de autenticação em serviços suportados.




Ncrack

Auditoria de autenticação de serviços de rede.




John the Ripper

Auditoria offline da resistência de palavras-passe através de hashes.




WPScan

Análise de segurança de instalações WordPress.




Patator

Testes modulares de segurança, incluindo autenticação.




Medusa

Auditoria de mecanismos de autenticação em serviços suportados.




SMBclient

Acesso e verificação de permissões em partilhas SMB.




Nmap

Descoberta de hosts, portas e serviços de rede.
