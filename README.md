# Logger (Fig)

Modulo de logging para projetos Fig, com niveis, contexto em JSON, labels e cores opcionais.

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

log.info("request", {path: "/health"})
```

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
[1700000000000] [auth] INFO: user login {"id":42,"role":"admin"}
```
