# Logger (Fig) v0.1.0

Módulo de logging para projetos Fig, com níveis, contexto em JSON, labels, cores e **timestamps formatados com o módulo date (interno da linguagem)**.

## Instalar no projeto

No seu projeto Fig:

```bash
fig install isCarlosCoder/logger
```

## Importar

```js
import "mod:isCarlosCoder/logger" log
```

## Uso basico

```js
import "mod:isCarlosCoder/logger" log

log.info("app started", {port: 3000})
log.warn("cache miss", {key: "user:42"})
log.error("db error", {code: "ECONNRESET"})
```

## Niveis disponiveis

- `trace`
- `debug`
- `info`
- `warn`
- `error`
- `fatal` (encerra o programa com `system.exit(1)`)

## Configuracao

```js
import "mod:isCarlosCoder/logger" log

log.setLevel("debug")
log.enableTimestamp(true)
log.enableColor(true)
log.enableUppercase(true)
log.setLabel("api")
log.setTimestampFormat("YYYY-MM-DD HH:mm:ss")  

log.info("request", {path: "/health"})
```

## Formatos de Timestamp

**NOVO:** Agora com suporte a formatos personalizados usando o módulo `date` (interno da linguagem):

```js
# Formato padrão (ISO)
log.setTimestampFormat("YYYY-MM-DD HH:mm:ss")
# Saída: [2026-02-09 15:30:45] [api] INFO: message

# Formato ISO completo
log.setTimestampFormat("YYYY-MM-DDTHH:mm:ss")
# Saída: [2026-02-09T15:30:45] [api] INFO: message

# Formato curto
log.setTimestampFormat("HH:mm:ss")
# Saída: [15:30:45] [api] INFO: message

# Formato americano
log.setTimestampFormat("MM/DD/YYYY HH:mm")
# Saída: [02/09/2026 15:30] [api] INFO: message
```

**Tokens suportados:**
- `YYYY` - Ano com 4 dígitos
- `MM` - Mês (01-12)
- `DD` - Dia (01-31)
- `HH` - Hora (00-23)
- `mm` - Minuto (00-59)
- `ss` - Segundo (00-59)

## Logger com label

```js
import "mod:isCarlosCoder/logger" log

let api = log.withLabel("api")
api.info("ready")
api.warn("rate limit")
```

## Contexto em JSON

O contexto eh serializado com `json.stringify`:

```js
log.info("user", {id: 42, role: "admin"})
```

## API

- `log.trace(message, context?)`
- `log.debug(message, context?)`
- `log.info(message, context?)`
- `log.warn(message, context?)`
- `log.error(message, context?)`
- `log.fatal(message, context?)`
- `log.log(level, message, context?)`
- `log.format(level, message, context?)` -> string
- `log.formatWithLabel(level, message, context?, label)` -> string
- `log.setLevel(level)`
- `log.getLevel()`
- `log.isEnabled(level)`
- `log.enableTimestamp(true|false)`
- `log.enableColor(true|false)`
- `log.enableUppercase(true|false)`
- `log.setLabel(label)`
- `log.clearLabel()`
- `log.setTimestampFormat(format)` 
- `log.withLabel(label)` -> object com `trace/debug/info/warn/error/fatal`

## Rodar testes locais

Dentro do modulo:

```bash
FIG_LOGGER_TEST=1 fig run
```

## Demo de saida

```bash
FIG_LOGGER_DEMO=1 fig run
```

Exemplo de saida:

```
[2026-02-09 15:30:45] [auth] INFO: user login {"id":42,"role":"admin"}
[2026-02-09T15:30:45] [api] WARN: rate limit {"limit":100}
[15:30:45] [web] DEBUG: cache hit {"key":"user:42"}
```

## Características da Versão 0.1.0

### Timestamps com Módulo Date (Interno)
- Formatação flexível com tokens `YYYY-MM-DD HH:mm:ss`
- Suporte a ISO, curto, personalizado
- Usa o módulo `date` interno da linguagem (não requer dependência externa)

### API: `setTimestampFormat()`
```js
log.setTimestampFormat("YYYY-MM-DD HH:mm:ss")
log.setTimestampFormat("HH:mm:ss")
log.setTimestampFormat("MM/DD/YYYY")
```

### Exemplos Práticos
- Logs para APIs (formato ISO)
- Logs para desenvolvimento (formato curto)
- Logs para auditoria (formato completo)

### Configurações Disponíveis
- Formato padrão: `"YYYY-MM-DD HH:mm:ss"`
- Funciona com todas as outras opções (cores, labels, etc.)
