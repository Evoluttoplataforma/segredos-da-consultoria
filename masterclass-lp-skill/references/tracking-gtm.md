# Padrão de Tracking GTM — Campos Obrigatórios

## Regra de Ouro

Todo formulário DEVE usar estas chaves EXATAS no `dataLayer.push`. Não inventar nomes alternativos.

## Campos Obrigatórios no dataLayer

| Chave | Tipo | Descrição |
|-------|------|-----------|
| `email` | string | E-mail do lead (usuario@dominio.com) |
| `phoneNumber` | string | Telefone SEM máscara — apenas dígitos (ex: 71999998888) |
| `nome` | string | Primeiro nome |
| `sobrenome` | string | Sobrenome (pode ser string vazia '', NUNCA omitir) |
| `apex_session_id` | string | Session ID do script de tracking |
| `time_on_page_at_submit` | number | Segundos na página até o submit |

## Nome do Evento

Para LPs HTML customizadas (não Tally):
```javascript
event: 'form_submit_success'
```

Trigger GTM: `form_submit_success [118]` — já dispara GA4, Meta CAPI (2 contas), TikTok e Bing.

## Implementação Completa para HTML Customizado

```javascript
// === No load da página ===
var pageStart = Date.now();

// Session ID
var sessionId = (function() {
  try {
    var key = 'apex_session_id';  // ← ESTA chave, não 'lp_session_id'
    var s = sessionStorage.getItem(key);
    if (!s) {
      s = Date.now() + '_' + Math.random().toString(36).substr(2, 9);
      sessionStorage.setItem(key, s);
    }
    return s;
  } catch(e) {
    return Date.now() + '_' + Math.random().toString(36).substr(2, 9);
  }
})();

// === No submit do form ===
document.getElementById('form-lead').addEventListener('submit', function(e) {
  e.preventDefault();

  var fullName = document.getElementById('nome').value.trim();
  var parts = fullName.split(' ');
  var firstName = parts[0];
  var lastName = parts.slice(1).join(' ');

  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    event: 'form_submit_success',
    email: document.getElementById('email').value.trim(),
    phoneNumber: document.getElementById('telefone').value.replace(/\D/g, ''),
    nome: firstName,
    sobrenome: lastName,
    apex_session_id: sessionId,
    time_on_page_at_submit: Math.round((Date.now() - pageStart) / 1000)
  });

  // Depois do push: enviar para webhook e redirecionar
});
```

## Erros Fatais a Evitar

| ERRADO | CORRETO |
|--------|---------|
| `lead_email` | `email` |
| `lead_phone` | `phoneNumber` |
| `lead_first_name` | `nome` |
| `lead_last_name` | `sobrenome` |
| `lp_session_id` | `apex_session_id` |
| Omitir `sobrenome` | Enviar `sobrenome: ''` (vazio) |
| Telefone com máscara `(71) 99999-8888` | Apenas dígitos `71999998888` |

## Checklist de Validação

1. Evento chega no GTM Preview com nome `form_submit_success`
2. DLV `email` populada (não undefined/null)
3. DLV `phoneNumber` — apenas dígitos, sem máscara
4. DLV `nome` e `sobrenome` populadas
5. `apex_session_id` presente no evento
6. Meta CAPI match quality >= 7
