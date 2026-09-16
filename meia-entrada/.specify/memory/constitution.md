<!--
Sync Impact Report
- Version change: scaffold → 1.0.0
- Modified principles: none; established four initial project principles
- Added sections: Additional Constraints, Quality Gates
- Removed sections: unused fifth principle slot from the scaffold
- Follow-up TODOs: confirm the original ratification date
-->

# Meia-Entrada Constitution

## Core Principles

### I. Server-Side Business Rule Validation
Toda regra de negócio MUST ser validada no servidor antes de qualquer operação ser
aceita, persistida ou disponibilizada ao usuário. A validação no front-end pode
melhorar a experiência, mas nunca substitui a validação no servidor. O servidor
MUST retornar uma resposta de erro clara e consistente quando uma regra for
violada, mantendo a integridade independentemente do cliente utilizado.

### II. Complete UI State Handling
Toda tela em produção MUST representar explicitamente os estados de
carregamento e de erro, além do estado de sucesso ou conteúdo vazio quando
aplicável. Nenhum fluxo pode depender de uma tela vazia, travada ou silenciosa
enquanto aguarda uma resposta ou falha. Esses estados MUST ser verificáveis por
testes apropriados ao fluxo.

### III. Automated Coverage for Price and Limit Rules
Toda regra de preço e de limite MUST ter cobertura por teste automatizado,
incluindo casos válidos, inválidos e limites relevantes. Alterações nessas
regras MUST atualizar ou adicionar os testes correspondentes antes de serem
aceitas. A cobertura automatizada é o mecanismo mínimo para evitar regressões
em cobrança, elegibilidade, quantidade e disponibilidade comercial.

### IV. Database as Availability Source of Truth
A disponibilidade de ingressos MUST ser determinada pelo banco de dados e por
suas operações transacionais, nunca pelo estado exibido na tela ou por uma
suposição mantida no cliente. O servidor MUST consultar e validar a
disponibilidade no momento da operação de reserva ou compra, tratando
concorrência e falhas de forma consistente. O estado da interface serve apenas
para exibição e atualização, não para autorizar a venda.

## Additional Constraints

As regras devem permanecer centralizadas em serviços ou módulos do servidor
que possam ser exercitados por testes automatizados. O cliente deve tratar as
respostas do servidor como autoridade para preço, limites e disponibilidade.

## Quality Gates

Uma mudança só pode ser integrada quando houver evidência de que as regras
afetadas foram validadas no servidor, que as telas alteradas possuem estados de
carregamento e erro, e que as regras de preço e limite relacionadas estão
cobertas por testes automatizados. Mudanças que afetem concorrência ou estoque
devem incluir teste de integração ou equivalente que exercite a fonte de
verdade persistida.

## Governance

Esta constituição prevalece sobre práticas conflitantes do projeto. Qualquer
alteração deve atualizar este documento, registrar no Sync Impact Report o
impacto nos princípios e obter revisão dos responsáveis pelo projeto. A
versionagem segue SemVer: MAJOR para remoção ou redefinição incompatível de
princípios, MINOR para novos princípios ou expansão material de escopo, e PATCH
para esclarecimentos sem mudança semântica. A revisão de conformidade deve
ocorrer em toda mudança de código que afete regras de negócio, telas,
pagamentos, limites ou disponibilidade.

**Version**: 1.0.0 | **Ratified**: TODO(RATIFICATION_DATE): confirmar data original de adoção | **Last Amended**: 2026-09-12
