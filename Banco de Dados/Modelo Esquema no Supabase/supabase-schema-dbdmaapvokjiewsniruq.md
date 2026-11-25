# Esquema do banco de dados — Supabase

**Projeto:** `dbdmaapvokjiewsniruq`  
**Origem:** exportação do esquema diretamente do Supabase, em 25/11/2026.

## Table `clinica`

### Columns

| Name | Type | Constraints |
|------|------|-------------|
| `id_clinica` | `int4` | Primary Identity |
| `cnpj` | `varchar` |  Unique |
| `razao_social` | `varchar` |  |
| `nome_fantasia` | `varchar` |  Nullable |
| `cnes` | `varchar` |  Nullable Unique |
| `telefone` | `varchar` |  Nullable |
| `email` | `varchar` |  Nullable |
| `endereco` | `varchar` |  Nullable |

## Table `paciente`

### Columns

| Name | Type | Constraints |
|------|------|-------------|
| `id_paciente` | `int4` | Primary Identity |
| `cpf` | `varchar` |  Unique |
| `nome` | `varchar` |  |
| `dt_nascimento` | `date` |  Nullable |
| `telefone` | `varchar` |  Nullable |
| `email` | `varchar` |  Nullable |
| `endereco` | `varchar` |  Nullable |
| `sexo` | `varchar` |  Nullable |

## Table `medico`

### Columns

| Name | Type | Constraints |
|------|------|-------------|
| `id_medico` | `int4` | Primary Identity |
| `cpf` | `varchar` |  Unique |
| `crm` | `varchar` |  Unique |
| `nome` | `varchar` |  |
| `telefone` | `varchar` |  Nullable |
| `email` | `varchar` |  Nullable |
| `dt_nascimento` | `date` |  Nullable |

## Table `especialidade`

### Columns

| Name | Type | Constraints |
|------|------|-------------|
| `id_especialidade` | `int4` | Primary Identity |
| `nome` | `varchar` |  Unique |
| `descricao` | `varchar` |  Nullable |

## Table `medico_especialidade`

### Columns

| Name | Type | Constraints |
|------|------|-------------|
| `id_medico` | `int4` | Primary |
| `id_especialidade` | `int4` | Primary |

## Table `consulta`

### Columns

| Name | Type | Constraints |
|------|------|-------------|
| `id_consulta` | `int4` | Primary Identity |
| `id_clinica` | `int4` |  |
| `id_paciente` | `int4` |  |
| `id_medico` | `int4` |  |
| `data_consulta` | `date` |  |
| `hora_consulta` | `time` |  |
| `status` | `varchar` |  |
| `observacoes` | `text` |  Nullable |
| `valor` | `numeric` |  Nullable |
| `motivo` | `varchar` |  Nullable |

## Table `contrato`

### Columns

| Name | Type | Constraints |
|------|------|-------------|
| `id_contrato` | `int4` | Primary Identity |
| `id_medico` | `int4` |  |
| `id_clinica` | `int4` |  |
| `numero_contrato` | `varchar` |  Unique |
| `data_inicio` | `date` |  |
| `data_fim` | `date` |  Nullable |
| `valor` | `numeric` |  Nullable |
| `tipo_contrato` | `varchar` |  Nullable |
| `status` | `varchar` |  |
| `observacoes` | `text` |  Nullable |

## RLS Policies

### `consulta`

| Policy | Command | Roles | Action | USING | WITH CHECK |
|--------|---------|-------|--------|-------|------------|
| `authenticated users can manage consulta` | ALL | authenticated | PERMISSIVE | `true` | `true` |

### `clinica`

| Policy | Command | Roles | Action | USING | WITH CHECK |
|--------|---------|-------|--------|-------|------------|
| `authenticated users can manage clinica` | ALL | authenticated | PERMISSIVE | `true` | `true` |

### `paciente`

| Policy | Command | Roles | Action | USING | WITH CHECK |
|--------|---------|-------|--------|-------|------------|
| `authenticated users can manage paciente` | ALL | authenticated | PERMISSIVE | `true` | `true` |

### `medico`

| Policy | Command | Roles | Action | USING | WITH CHECK |
|--------|---------|-------|--------|-------|------------|
| `authenticated users can manage medico` | ALL | authenticated | PERMISSIVE | `true` | `true` |

### `especialidade`

| Policy | Command | Roles | Action | USING | WITH CHECK |
|--------|---------|-------|--------|-------|------------|
| `authenticated users can manage especialidade` | ALL | authenticated | PERMISSIVE | `true` | `true` |

### `medico_especialidade`

| Policy | Command | Roles | Action | USING | WITH CHECK |
|--------|---------|-------|--------|-------|------------|
| `authenticated users can manage medico_especialidade` | ALL | authenticated | PERMISSIVE | `true` | `true` |

### `contrato`

| Policy | Command | Roles | Action | USING | WITH CHECK |
|--------|---------|-------|--------|-------|------------|
| `authenticated users can manage contrato` | ALL | authenticated | PERMISSIVE | `true` | `true` |