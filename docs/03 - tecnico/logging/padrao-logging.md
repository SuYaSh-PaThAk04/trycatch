# Documento Técnico --- Padrão de Logging (TryCatch)

Classificação: Documento Técnico\
Camada: 3 --- Técnico\
Status: Versão inicial oficial

------------------------------------------------------------------------

## 1. Objetivo

Este documento define o padrão oficial de logging do projeto TryCatch.

O objetivo é:

-   Garantir rastreabilidade de ações críticas;
-   Facilitar debug e auditoria;
-   Permitir futura integração com ferramentas de observabilidade;
-   Evitar uso inconsistente de console.log no backend.

------------------------------------------------------------------------

## 2. Princípios

O logging do TryCatch deve ser:

-   Estruturado (formato padronizado);
-   Contextual (com metadados relevantes);
-   Não verboso em produção;
-   Seguro (sem exposição de dados sensíveis);
-   Evolutivo.

------------------------------------------------------------------------

## 3. Logging Estruturado

Logging estruturado significa registrar eventos em formato organizado,
preferencialmente JSON.

Exemplo:

{ "level": "error", "timestamp": "2026-02-13T12:45:00Z", "service":
"project", "action": "create_project", "userId": "cuid123", "message":
"Validation failed", "statusCode": 400 }

------------------------------------------------------------------------

## 4. Estrutura Padrão de Log

Todo log backend deve conter:

-   level → info \| warn \| error
-   timestamp → ISO 8601
-   service → domínio afetado (project, feedback, auth, invite)
-   action → operação realizada
-   message → descrição objetiva
-   userId → quando aplicável
-   requestId → quando aplicável

------------------------------------------------------------------------

## 5. Níveis de Log

info: - Operações normais relevantes (ex: criação de projeto)

warn: - Comportamentos inesperados não críticos

error: - Falhas que impedem execução normal

------------------------------------------------------------------------

## 6. Regras de Segurança

Não registrar:

-   Senhas
-   Tokens
-   Dados sensíveis
-   Informações completas de autenticação

Logs devem respeitar LGPD.

------------------------------------------------------------------------

## 7. Implementação Recomendada

-   Criar utilitário central de logging
-   Proibir console.log solto no código
-   Centralizar logs críticos em middleware quando possível

------------------------------------------------------------------------

## 8. Evolução Futura

Logging poderá evoluir para:

-   Integração com ferramentas externas (ex: Datadog, Sentry)
-   Monitoramento de performance
-   Métricas automatizadas

Critério para evolução:

-   Aumento significativo de usuários
-   Necessidade de auditoria formal
-   Incidentes recorrentes
