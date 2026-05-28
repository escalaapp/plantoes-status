# Página de Status / Manutenção

Este repositório centraliza os JSON usados para controlar a página de manutenção e o banner/warning dos ambientes do sistema **Escala Plantões**.

Os arquivos são publicados via GitHub Pages e permitem alterar o comportamento sem deploy no sistema principal.

## Arquivos disponíveis

### Página de manutenção

- `maintenance-app.json`
- `maintenance-hom.json`
- `maintenance-prod.json`

### Banner / warning

- `maintenance-warning-hom.json`
- `maintenance-warning-prod.json`

## 1. Página de manutenção

Os arquivos `maintenance-[env].json` controlam a página de manutenção.

### Formato

```json
{
  "enabled": false,
  "return_time": ""
}
```

### Campos

| Campo         | Tipo    | Descrição |
| ------------- | ------- | --------- |
| `enabled`     | boolean | Ativa ou desativa a página de manutenção |
| `return_time` | string  | Horário previsto de retorno. Não aceita HTML, apenas texto simples |

### Regras

- Não há variações de cor na página de manutenção.
- O campo `return_time` deve ser preenchido com uma string simples.
- Não use tags HTML nesse arquivo.

### Exemplo

```json
{
  "enabled": true,
  "return_time": "12/05/2026 14:30"
}
```

### Efeito esperado

- Quando `enabled` for `true`, o sistema exibe a página de manutenção.
- Quando `enabled` for `false`, o sistema funciona normalmente.

## 2. Banner / warning

Os arquivos `maintenance-warning-[env].json` controlam o banner de aviso exibido antes da manutenção.

### Formato

```json
{
  "enabled": true,
  "type": "maintenance",
  "variant": "green",
  "message": ""
}
```

### Campos

| Campo      | Tipo    | Descrição |
| ---------- | ------- | --------- |
| `enabled`  | boolean | Ativa ou desativa o warning |
| `type`     | string  | Tipo do aviso. Atualmente usamos `maintenance` |
| `variant`  | string  | Cor do warning. Os valores aceitos são `green` e `orange` |
| `message`  | string  | Mensagem exibida no banner |

### Regras

- As únicas variações de cor disponíveis para o warning são `green` e `orange`.
- O ideal é definir `variant` manualmente como `orange` no dia da migração, a partir de `00:00h`.
- O campo `message` aceita HTML básico, então é possível usar tags como `<strong>` para destacar trechos da mensagem.
- Evite HTML complexo; use apenas formatação simples.

### Exemplo

```json
{
  "enabled": true,
  "type": "maintenance",
  "variant": "orange",
  "message": "O Escala Plantões entrará em manutenção preventiva em <strong>14 de maio às 21h</strong> para melhorar a estabilidade e a segurança do sistema. Voltaremos logo!"
}
```

### Efeito esperado

- O banner aparece no ambiente configurado.
- O usuário vê a mensagem com a formatação básica permitida.
