# Documento Técnico --- Arquitetura Geral (TryCatch)

Classificação: Documento Técnico\
Camada: 3 --- Técnico\
Status: Implementado (versão consolidada)

------------------------------------------------------------------------

## 1. Identificação

-   Nome do documento: Arquitetura Geral do Sistema
-   Domínio técnico: Arquitetura
-   Documento(s) relacionado(s): Modelagem de Dados; Padrão de Logging;
    Documentos de Produto
-   Data de criação: 2026-02-13
-   Última atualização: 2026-02-13

------------------------------------------------------------------------

## 2. Contexto Técnico

O TryCatch foi concebido como um produto educacional real, com
arquitetura suficientemente madura para refletir práticas profissionais,
mas proporcional ao estágio atual do projeto.

Problema tratado:

-   Definir modelo arquitetural claro;
-   Garantir separação de domínios;
-   Formalizar critérios de evolução futura;
-   Evitar crescimento desorganizado.

------------------------------------------------------------------------

## 3. Objetivo Técnico

Este documento especifica:

-   Modelo arquitetural adotado;
-   Separação de domínios;
-   Padrões técnicos essenciais;
-   Critérios de evolução.

Não cobre:

-   Implementação detalhada de cada módulo;
-   Infraestrutura de produção específica.

------------------------------------------------------------------------

## 4. Descrição Técnica da Solução

### 4.1 Stack Principal

-   Next.js (App Router)
-   TypeScript
-   Prisma ORM
-   PostgreSQL
-   NextAuth

### 4.2 Modelo Arquitetural

Monólito modular evolutivo.

Características:

-   Backend e frontend integrados via App Router;
-   Separação lógica por domínio;
-   Prisma como camada única de acesso a dados;
-   Autenticação centralizada.

### 4.3 Separação de Domínios

Domínios principais:

-   Produto
-   Autenticação
-   Feedback
-   Convites
-   Projetos

Cada domínio possui:

-   Documento de produto correspondente;
-   Entidades próprias no schema;
-   Responsabilidades claras.

------------------------------------------------------------------------

## 5. Tratamento de Erros

O sistema adota padrão consistente de tratamento de erros.

Regras:

-   Uso correto de códigos HTTP;
-   Erros de validação retornam status 400;
-   Erros de autenticação retornam 401/403;
-   Erros inesperados retornam 500;
-   Mensagens devem ser claras, mas não expor detalhes internos.

Integração com logging:

-   Todo erro relevante deve gerar log estruturado;
-   Logs devem conter service e action.

------------------------------------------------------------------------

## 6. Padrão de Validação

Validação ocorre no backend utilizando Zod.

Princípios:

-   Toda entrada externa deve ser validada;
-   Schemas devem refletir regras de negócio;
-   Erros de validação não devem vazar stack trace;
-   Resposta deve seguir padrão JSON consistente.

------------------------------------------------------------------------

## 7. Logging e Observabilidade

O projeto adota logging estruturado conforme definido no:

-   Documento Técnico --- Padrão de Logging

Regras:

-   Logs seguem estrutura JSON padronizada;
-   Não é permitido uso de console.log solto;
-   Dados sensíveis não devem ser registrados;
-   Logs críticos permitem rastreabilidade por usuário e ação.

------------------------------------------------------------------------

## 8. Escalabilidade e Evolução Arquitetural

Critérios objetivos para futura extração de serviços:

-   Crescimento significativo de carga;
-   Necessidade de integração externa;
-   Gargalos persistentes identificados por métricas;
-   Equipe ampliada atuando simultaneamente no mesmo domínio.

A decisão de extração deve ser formalizada via ADR.

------------------------------------------------------------------------

## 9. Alternativas Avaliadas

### Microservices desde o início

Vantagens: - Escalabilidade independente;

Desvantagens: - Complexidade desnecessária; - Overengineering; - Aumento
de custo cognitivo.

Motivo da não adoção: - Projeto ainda não demanda tal nível de
separação.

------------------------------------------------------------------------

## 10. Impacto Arquitetural

-   Performance: adequada ao estágio atual.
-   Escalabilidade: preparada para evolução futura.
-   Manutenibilidade: favorecida pela separação de domínios.
-   Acoplamento: controlado dentro do monólito modular.
-   Observabilidade: ampliada com logging estruturado.

------------------------------------------------------------------------

## 11. Impacto em Segurança

-   Autenticação centralizada via NextAuth;
-   Validação obrigatória com Zod;
-   Logs sem dados sensíveis;
-   Separação clara entre dados públicos e privados.

------------------------------------------------------------------------

## 12. Impacto em Dados

-   Prisma como camada única de acesso;
-   Integridade referencial mantida no schema;
-   Alterações estruturais exigem migração formal.

------------------------------------------------------------------------

## 13. Dependências Técnicas

-   Node.js
-   PostgreSQL
-   Prisma
-   NextAuth
-   Zod

------------------------------------------------------------------------

## 14. Riscos Técnicos Identificados

-   Crescimento descontrolado do monólito;
-   Falta de disciplina na separação de domínios;
-   Uso excessivo de logs impactando performance.

Mitigações:

-   Revisão arquitetural periódica;
-   ADR para decisões estruturais;
-   Centralização de logging.

------------------------------------------------------------------------

## 15. Critérios de Validação

-   Estrutura modular mantida;
-   Separação de domínios respeitada;
-   Logs estruturados funcionando;
-   Validações aplicadas em todas as rotas;
-   Testes cobrindo fluxos críticos.

------------------------------------------------------------------------

## 16. Relação com Documentos de Produto

Suporta todos os documentos de produto da Camada 2, fornecendo base
técnica para implementação.

------------------------------------------------------------------------

## 17. Histórico de Decisões Técnicas

-   Adoção de monólito modular;
-   Formalização de logging estruturado;
-   Definição de critérios objetivos para extração futura de serviços.

------------------------------------------------------------------------

## 18. Status e Próximos Passos

-   Status atual: Implementado
-   Pendências técnicas: Revisão periódica da separação de domínios
-   Melhorias futuras identificadas:
    -   Monitoramento de performance
    -   Eventual extração de serviços se critérios forem atingidos

------------------------------------------------------------------------

Observação: Este documento garante coerência arquitetural sem
fragmentação excessiva de documentação.
