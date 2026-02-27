# Prompt Inicial para Claude Code

Copie e cole a mensagem abaixo no Claude Code para iniciar a geração da landing page:

---

## Mensagem para colar no Claude Code:

```
Preciso que você crie uma landing page completa de masterclass seguindo a skill `masterclass-lp-skill/SKILL.md` que está neste projeto.

ANTES DE COMEÇAR: Leia TODOS os arquivos de referência da skill na ordem:
1. `masterclass-lp-skill/SKILL.md` (instruções principais)
2. `masterclass-lp-skill/references/copy-masterclass.md` (texto EXATO da página)
3. `masterclass-lp-skill/references/page-structure.md` (arquitetura detalhada das páginas)
4. `masterclass-lp-skill/references/animations.md` (catálogo de efeitos CSS/JS)
5. `masterclass-lp-skill/references/design-system.md` (variáveis CSS, componentes)
6. `masterclass-lp-skill/references/tracking-gtm.md` (padrão obrigatório de campos dataLayer)

DADOS DO EVENTO:
- Nome: "A Morte da Consultoria Artesanal"
- Data: 10 de março de 2026 às 18h (Brasília)
- Duração: 1h30
- Formato: Ao vivo, sem replay, gratuita
- Webhook Make: [COLE_SEU_WEBHOOK_AQUI]
- WhatsApp Group: [COLE_SEU_LINK_AQUI]

IMAGENS DISPONÍVEIS (pasta img/):
- img/Imagem.jpg.jpeg → Lápide "Consultoria Presencial" com cruz "2026" — usar como background do hero
- img/WhatsApp Image 2026-02-27 at 17.47.41.jpeg → Ampulheta + contrato queimando
- img/evolutto masterclass .webp → Cemitério de consultores devorados por IA — usar na seção de tensão
- img/evolutto masterclass.webp → Split: cemitério P&B | consultor tech — usar na seção de solução

ENTREGÁVEIS:
1. `index.html` — Landing page principal com:
   - Banner sticky com countdown no topo
   - Hero split (texto esquerda + formulário direita)
   - Seção de tensão/problema com imagem de cemitério
   - Seção de solução com o que vai aprender
   - CTA final com urgência máxima
   - TODOS os efeitos do catálogo de animações (fade-in scroll, glow, shimmer, spinning border, partículas, 3D tilt, confete no submit)
   - Formulário envia para webhook Make + faz dataLayer.push no padrão GTM
   - Animação de confete/fogos após submit → redirect para obrigado.html

2. `obrigado.html` — Página de obrigado com:
   - Barra de progresso 3 etapas (inscrição → WhatsApp → agenda)
   - Card para entrar no grupo do WhatsApp
   - Card para salvar na agenda (Google Calendar + arquivo .ics para Outlook)
   - Estado persistido em localStorage
   - Countdown para o evento

IMPORTANTE:
- Tema DARK agressivo — a LP precisa transmitir DESESPERO para consultores
- Cor accent: vermelho #DC2626 (não verde)
- Todas as animações do catálogo devem ser implementadas
- dataLayer.push OBRIGATÓRIO seguindo references/tracking-gtm.md (chaves: email, phoneNumber, nome, sobrenome, apex_session_id, time_on_page_at_submit)
- Evento no dataLayer: 'form_submit_success'
- Responsivo: breakpoints 768px, 600px, 414px, 360px
- Desabilitar 3D tilt e partículas canvas em mobile
- Imagens com caminhos relativos (img/nome-do-arquivo.ext)
```

---

## Notas

- Substitua `[COLE_SEU_WEBHOOK_AQUI]` pelo URL real do webhook do Make
- Substitua `[COLE_SEU_LINK_AQUI]` pelo link real do grupo do WhatsApp
- A skill e todos os references já estão na pasta `masterclass-lp-skill/` dentro do projeto
- O Claude Code vai ler os references e seguir todas as especificações
