# Banco de Dados — Sistema de Agendamento de Clínica

Projeto da squad para organizar o agendamento de consultas em clínicas, relacionando pacientes, médicos, especialidades, unidades de atendimento e contratos. A implementação utiliza Supabase com PostgreSQL 17.

## Objetivo e regras de negócio

O sistema registra clínicas, pacientes, médicos, especialidades, consultas e contratos. A regra de agendamento impede que o mesmo médico tenha duas consultas na mesma data e horário, por meio de `UNIQUE (id_medico, data_consulta, hora_consulta)`.

O relacionamento N:N entre médicos e especialidades é resolvido pela tabela intermediária `medico_especialidade`, com duas FKs e chave primária composta. A tabela `contrato` registra os vínculos entre médicos e clínicas ao longo do tempo.

## Estrutura solicitada

- **Diagrama Conceitual/** — diagrama original exportado do BRModelo e detalhes.
- **Modelo Lógico/** — modelo relacional final, com tabelas, colunas, PKs e FKs.
- **Modelo Esquema no Supabase/** — esquema consultado no projeto Supabase.
- **Tabelas/** — script `CREATE TABLE` e constraints.
- **Testes/** — scripts `INSERT INTO` e `ALTER TABLE`; também há exemplos complementares de `UPDATE` e `SELECT`.
- **Dados/** — visualizações dos registros fictícios nas sete tabelas.

## Tabelas e registros conferidos

| Tabela | Registros | Função |
|---|---:|---|
| `clinica` | 2 | Unidades de atendimento |
| `paciente` | 3 | Pacientes (entidade chamada Cliente no DER original) |
| `medico` | 3 | Médicos |
| `especialidade` | 4 | Especialidades médicas |
| `medico_especialidade` | 4 | Associação N:N entre médicos e especialidades |
| `consulta` | 3 | Agendamentos |
| `contrato` | 3 | Vínculos contratuais entre médicos e clínicas |
| **Total** | **22** | Registros de demonstração |

Todos os dados são fictícios; os e-mails usam o domínio reservado `.invalid`.

## Constraints utilizadas

- `PRIMARY KEY` para identificar cada registro, incluindo chave composta em `medico_especialidade`.
- `FOREIGN KEY` para manter os relacionamentos entre as tabelas.
- `UNIQUE` para CPF, CNPJ, CRM, número de contrato e horário do mesmo médico.
- `NOT NULL` para campos obrigatórios.
- `DEFAULT` para valores iniciais de status.
- `CHECK` para estados permitidos, valores monetários não negativos e período de contrato válido.
- `ON DELETE RESTRICT` para proteger registros referenciados.

## Ordem de execução em um banco vazio

1. `Tabelas/01_criacao_tabelas.sql` — cria as sete tabelas e constraints.
2. `Testes/02_alter_table_motivo.sql` — acrescenta a coluna opcional `motivo VARCHAR(255)` à tabela `consulta`.
3. `Testes/03_insert_dados.sql` — insere os registros fictícios de demonstração.

Os arquivos `04_update_complementar.sql` e `05_consultas_verificacao.sql` são complementares. O banco publicado já possui os 22 registros; não execute o `CREATE TABLE` novamente nele.

## Correspondência entre o DER e a implementação

A entidade original `Cliente` foi nomeada `paciente` na implementação. O atributo `data_hora` foi separado em `data_consulta` (`DATE`) e `hora_consulta` (`TIME`). O atributo `motivo`, que aparece no diagrama original, foi acrescentado à tabela `consulta` usando `ALTER TABLE`. O relacionamento N:N entre médico e especialidade é implementado por `medico_especialidade`. A relação 1:N `trabalha_em` entre clínica e médico foi detalhada na tabela `contrato`.

## Modelo público e exportação do BRModelo

- **BRModelo Web — modelo público da squad:** https://app.brmodeloweb.com/publicview/6b06d4ef1448006b56801a47

O código SQL exportado pelo BRModelo foi usado como referência para a modelagem, mas não é o script de criação executável da entrega. A exportação apresenta problemas como múltiplas declarações de chave primária por tabela, vírgulas finais, tipos `INT` aplicados a atributos textuais, datas e valores, além de não representar separadamente as tabelas `especialidade` e `medico_especialidade`. Por isso, a implementação relacional foi ajustada e normalizada no script `Tabelas/01_criacao_tabelas.sql`, com suas chaves e constraints, e está refletida no Supabase.

## Links

- **Supabase — painel do projeto:** https://supabase.com/dashboard/project/dbdmaapvokjiewsniruq
- **Supabase — URL pública do projeto/API:** https://dbdmaapvokjiewsniruq.supabase.co
- **BRModelo Web — modelo público:** https://app.brmodeloweb.com/publicview/6b06d4ef1448006b56801a47

O painel Supabase exige autenticação e permissão no projeto. O endpoint público não significa que as tabelas estejam abertas para leitura anônima: as tabelas permanecem protegidas por RLS.

## Conteúdo do Módulo 4 aplicado

O projeto reúne os conteúdos das seis aulas: modelagem conceitual e DER; entidades, atributos, relacionamentos e cardinalidade; modelo lógico, normalização, PK e tipos de dados; FKs e integridade referencial; DDL com `CREATE TABLE`, constraints e `ALTER TABLE`; e DML com `INSERT`, `SELECT`, filtros e `UPDATE`.
