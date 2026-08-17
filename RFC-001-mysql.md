# Solicitação de Mudança: RFC-001

* **IC afetado:** Banco de Dados — SGBD (MySQL)
* **Versão atual:** MySQL 8.4
* **Versão proposta:** MySQL 9.0
* **Motivo da mudança:** O banco MySQL 8.4 apresentou problemas de desempenho no ambiente de produção. A atualização para o MySQL 9.0 visa otimizar o tempo de resposta das consultas e melhorar a performance geral do sistema.
* **Riscos:**
  - Incompatibilidade de sintaxe SQL ou funções descontinuadas no MySQL 9.0.
  - Indisponibilidade do sistema durante o processo de migração.
  - Riscos de integridade dos dados caso a migração falhe.
* **Impacto na aplicação:** Falha em consultas específicas se houver incompatibilidade e indisponibilidade temporária do serviço durante a janela de manutenção.
* **Ambientes afetados:** Desenvolvimento, Homologação/Staging e Produção.
* **Testes necessários:**
  1. Execução de testes de regressão de todas as rotinas do banco de dados na versão 9.0.
  2. Testes de carga e estresse em ambiente de staging.
  3. Validação de compatibilidade com o driver do Node.js/Express.
* **Plano de implementação:**
  1. Definir e comunicar a janela de manutenção.
  2. Realizar backup completo (*dump*) do banco de dados `pedidos`.
  3. Atualizar o MySQL para 9.0 em ambiente de testes/staging e validar.
  4. Aplicar a atualização no servidor de produção.
  5. Executar scripts de validação de dados e *smoke tests* na aplicação.
* **Plano de rollback:**
  1. Em caso de falha crítica nos testes pós-implantação, parar a aplicação.
  2. Desinstalar a versão 9.0 e reinstalar o MySQL 8.4 no servidor.
  3. Restaurar o backup integral realizado antes do procedimento.
  4. Conectar a aplicação à versão 8.4 e validar o funcionamento.
* **Responsável:** Administrador de Banco de Dados (DBA) / Time de Infraestrutura
* **Aprovação:** Comitê de Controle de Mudanças (CAB) / Líder Técnico