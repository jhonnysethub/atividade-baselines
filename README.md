# Aponti Academy - DevOps - Prática Baseline

Atividade prática em grupo com o objetivo de compreender o conceito de **Baseline** dentro da Gerência de Configuração, relacionando-o ao versionamento, aos itens de configuração (ICs), ao controle de mudanças e à identificação de _Configuration Drift_.

## Divisão das Tarefas

| Desafio | Responsável                                             |
| ------- | ------------------------------------------------------- |
| 1       | [Miqueias Eduardo](https://github.com/miqueias-eduardo) |
| 2       | [Nelson Henrique](https://github.com/nhsneto)           |
| 3       | [Jhonny Emmanoel](https://github.com/jhonnysethub)      |
| 4 e 5   | [Luiz Felipe Gomes](https://github.com/felipeGTBR)      |

## Histórico de Evolução da Configuração

| Etapa | Evento             | Descrição                 | Responsável       | Data       |
| ----- | ------------------ | ------------------------- | ----------------- | ---------- |
| 1     | BASELINE-v1.0      | Baseline inicial aprovada | Miqueias Eduardo  | 14/08/2026 |
| 2     | RFC-001            | Solicitação de mudança    | Jhonny Emmanoel   | 15/08/2026 |
| 3     | Alteração do MySQL | Implementação da mudança  | Nelson Henrique   | 15/08/2026 |
| 4     | Testes             | Validação da mudança      | Jhonny Emmanoel   | 16/08/2026 |
| 5     | Aprovação          | Aceite da mudança         | Miqueias Eduardo  | 16/08/2026 |
| 6     | BASELINE-v1.1      | Nova baseline             | Luiz Felipe Gomes | 16/08/2026 |

**Observação:** Ocorreu uma alteração na versão do MySQL fora do processo formal de gerência de configuração, então foi necessário a RFC-001 para formalizar, validar e aprovar essa mudança, garantindo a rastreabilidade histórica.

## Desafio 1 - Criar a Baseline

Estado oficial aprovado do sistema: [BASELINE-v1.0](BASELINE-V1.0.md)

## Desafio 2 - Mudança Não Autorizada

**Cenário:**

Um administrador percebeu que o banco MySQL 8.4 estava apresentando problemas de desempenho e decidiu atualizar diretamente o servidor de produção para MySQL 9.0. A aplicação continuou utilizando as mesmas configurações e o código não foi alterado. Após a atualização, algumas consultas começaram a apresentar erros.

**1. A baseline foi alterada?**

Sim, a baseline foi alterada, pois o banco MySQL 8.4, que era o item de configuração aprovado, foi atualizado para o MySQL 9.0 sem um processo formal de controle de mudanças, prejudicando o ambiente estável de configuração e gerando erros em algumas consultas.

**2. Qual Item de Configuração (IC) foi modificado?**

IC - Banco de Dados MySQL 8.4.

**3. Essa alteração deveria ter sido realizada diretamente em produção??**

Não, pois todas as alterações que precisam ser feitas na Baseline exigem um processo formal de controle de mudanças para garantir a estabilidade do projeto e evitar regressões.

**4. Qual processo deveria ter sido executado antes da alteração?**

O processo formal de controle de mudanças. Esse processo é feito através do RFC (Request for Change), que é uma requisição que detalha a alteração proposta, sua justificativa e o nível de urgência. Ela deve ser avaliada e compreendida por todos os envolvidos, além de ser implementada, testada e, por fim, aceita se não ocorrer regressões.

**5. O que deve acontecer com a baseline após uma mudança aprovada?**

Ela deve ser atualizada formalmente para uma nova versão, mantendo o histórico de mudanças, ou seja, uma nova baseline é criada contendo o novo estado estável aprovado do sistema.

## Desafio 3 - Criar uma RFC

Solicitação formal de mudança: [RFC-001](RFC-001-mysql.md)

## Desafio 4 - Criar uma Nova Baseline

Nova configuração implementada, testada e aprovada: [BASELINE-v1.1]() <!-- Adicionar link -->

## Desafio 5 - Configuration Drift

| Situação                                                      | Mudança controlada?                         | Está na baseline? |
| ------------------------------------------------------------- | ------------------------------------------- | ----------------- |
| Desenvolvedor altera o código e realiza um novo commit        | Não, se não passou pelo processo de mudança | Não               |
| Administrador altera manualmente uma configuração em produção | Não                                         | Não               |
| Mudança aprovada e documentada gera a baseline v1.1           | Sim                                         | Sim               |

**Explique: Se alguém alterar manualmente o servidor depois da baseline v1.1, o que aconteceu com a configuração do ambiente?**

Irá ocorrer um Configuration Drift, porque o estado real do servidor passou a ser diferente do estado oficial definido pela baseline v1.1
O configuration Drift aparece quando uma alteração não foi solicitada, avaliada, aprovada ou registrada

## Pergunta Final

**Em até 5 linhas, explique com suas próprias palavras qual é a importância de uma baseline para uma equipe DevOps e quais problemas podem surgir quando alterações são realizadas sem controle de configuração.**

### Jhonny Emmanoel

Lorem Ipsum...

### Luiz Felipe Gomes

A baseline é um documento descrito em vários frameworks de governança de ti (COBIT) para o profissional de DevOps acompanhar as configurações e mudanças do ambiente. Quando alterações são feitas sem controle, podem surgir o Configuration Drift que é quando o ambiente real é diferente do registrado oficialmente na baseline.

### Miqueias Eduardo

A baseline é importante para manter versões e configurações estáveis e compatíveis entre si para o funcionamento da aplicação. Ela também documenta as decisões de configuração utilizadas no sistema, evitando problemas causados por atualizações de dependências que podem gerar incompatibilidades com o sistema. Com mudanças e atualizações documentadas e avaliadas, a aplicação mantém seu funcionamento consistente e reduz o risco de falhas causadas por alterações na configuração. Além disso, permite consultar o histórico e entender as decisões tomadas durante as mudanças.

### Nelson Henrique

A baseline representa um estado de configuração estável de um projeto, então ela é importante para manter essa consistência e não prejudicar o andamento do desenvolvimento e da operação, além de servir de controle para as mudanças que acontecerão na configuração do software. Sem esse marco estável e o controle de cada item, podemos encontrar erros de consultas a bancos, usar novas bibliotecas que são incompatíveis com a versão estável, remover um arquivo de configuração importante e dificuldade de retornar a um estado estável, por exemplo.
