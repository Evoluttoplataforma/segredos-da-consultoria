---
name: masterclass-lp
description: |
  Gera landing pages completas estilo masterclass/webinar com tema dark agressivo, formulário de captura, página de obrigado com barra de progresso, animações avançadas (confete, scroll reveal, glow, partículas), banner de countdown, e integração com webhook (Make/n8n). Use esta skill sempre que o usuário pedir para criar uma landing page de evento, masterclass, webinar, aula ao vivo, workshop online, ou qualquer página de captura com countdown e página de obrigado. Também acione quando o usuário mencionar: LP de evento, página de inscrição, landing page dark, página com countdown, formulário com confete, página de obrigado com checklist/progresso.
---

# Masterclass LP Builder

Skill para gerar landing pages de masterclass/webinar com alta conversão. Produz um arquivo HTML único (single-file) com CSS e JS embutidos, pronto para deploy.

## Antes de Começar

Leia os arquivos de referência conforme necessário:
- `references/page-structure.md` — Arquitetura completa das páginas (LP + Obrigado)
- `references/animations.md` — Catálogo de efeitos CSS/JS (scroll reveal, glow, shimmer, 3D tilt, partículas)
- `references/design-system.md` — Variáveis CSS, tipografia, botões, componentes base
- `references/tracking-gtm.md` — Padrão obrigatório de campos dataLayer para GTM/Meta CAPI/Google Ads

## Arquitetura Geral

A skill gera **2 arquivos HTML** independentes:

1. **`index.html`** — Landing page principal de captura
2. **`obrigado.html`** — Página de obrigado com barra de progresso

Ambos são single-file (CSS + JS inline), dark theme, responsivos, e seguem o design system e catálogo de animações dos references.

## Fluxo do Usuário

```
[Usuário chega na LP]
  → Vê banner de countdown no topo
  → Sente urgência/desespero com o tema visual
  → Scroll com animações reveal
  → Preenche formulário (nome, email, telefone)
  → dataLayer.push com campos padrão GTM
  → POST para webhook Make/n8n
  → Animação de confete/fogos explode na tela
  → Redirect para obrigado.html

[Página de Obrigado]
  → Barra de progresso (3 etapas)
  → Etapa 1: ✅ Inscrição confirmada (já completa)
  → Etapa 2: Entrar no grupo do WhatsApp (link)
  → Etapa 3: Salvar na agenda (Google Calendar + Microsoft/Outlook)
  → Conforme completa etapas, barra avança
```

## Coleta de Informações

Antes de gerar o código, pergunte ao usuário (se ainda não informou):

1. **Nome da masterclass** (ex: "Os Segredos que Vão Matar a Consultoria em 2026")
2. **Data e horário do evento** (ex: "18 de Março, 2026 às 20h")
3. **URL do webhook Make** para receber os leads
4. **Link do grupo do WhatsApp**
5. **Cor de destaque** (accent color) — se não informar, usar vermelho `#DC2626` para reforçar urgência
6. **Imagens disponíveis** — verificar a pasta `img/` do projeto

## Tom e Atmosfera Visual

A LP é voltada para **consultores** e precisa transmitir **desespero e urgência**. O usuário deve sentir que sua carreira está em risco se não participar.

### Estratégia de Impacto Emocional

- **Background:** Imagem escura de cemitério/lápide com overlay gradient escuro (70-85% opacidade)
- **Paleta:** Preto profundo (#0a0a0f) + vermelho urgente (#DC2626) + branco para texto
- **Tipografia:** Títulos agressivos com gradient branco→cinza, texto impactante
- **Palavras-chave visuais:** "vai morrer", "cemitério", "fim", "última chance", "destruição"
- **Partículas Canvas:** Vermelho/laranja flutuando = sensação de fogo/caos
- **Glows:** Vermelho pulsante em vez do verde padrão
- **Animações:** Mais rápidas e "cortantes" que o padrão — transition 0.6s em vez de 0.8s

### Hierarquia de Emoções por Seção

1. **Banner topo:** URGÊNCIA (countdown ticking)
2. **Hero:** CHOQUE ("A consultoria vai morrer em 2026")
3. **Problema:** MEDO (dados de mercado, tendências)
4. **Solução:** ESPERANÇA (a masterclass como saída)
5. **CTA/Form:** AÇÃO IMEDIATA (vagas limitadas, inscreva-se agora)

## Estrutura da LP (index.html)

### 1. Banner Sticky no Topo
```
[🔴 LIVE] Masterclass Gratuita — {DATA} às {HORA} | ⏰ Faltam X dias, X horas
```
- Fixo no topo (sticky), z-index alto
- Background: gradiente vermelho escuro → preto
- Countdown em JS atualizando a cada segundo
- Em mobile: versão compacta

### 2. Hero Section (Layout Split)
- **Esquerda (60%):** Texto principal
  - Badge pulsante: "🔴 VAGAS LIMITADAS" com borda pulse animation
  - H1 agressivo com texto gradiente
  - Subtítulo com a promessa/dor
  - Bullet points com ícones de benefícios
  - Data e hora do evento
- **Direita (40%):** Formulário de captura
  - Card com backdrop-filter blur
  - Título do form: "Garanta sua vaga gratuita"
  - Campos: Nome, E-mail, Telefone (com máscara)
  - Botão CTA vermelho com glow pulsante
  - Texto de escassez abaixo: "Apenas XX vagas restantes"

### 3. Seção de Problema/Dor
- Background com imagem de cemitério de consultores (overlay escuro)
- Cards de "dor" com borda rotativa (spinning gradient border) em vermelho
- Cada card = um motivo pelo qual consultorias vão morrer
- Partículas canvas vermelhas/laranja flutuando
- Contador animado: "+73% das consultorias vão fechar até 2027"

### 4. Seção de Solução
- Transição visual: do vermelho/caos para um tom mais esperançoso
- "O que você vai aprender na masterclass"
- Cards com hover 3D tilt
- Steps/pilares numerados
- Shimmer effect nos cards de destaque

### 5. Sobre o Apresentador (opcional)
- Foto + bio curta
- Credenciais / prova social

### 6. CTA Final
- Repetição do formulário ou botão que scrolla até o hero
- Urgência máxima: countdown + vagas restantes

### 7. Footer Mínimo
- Copyright + política de privacidade

## Formulário — Especificações Técnicas

### Campos
```html
<input name="nome" placeholder="Seu nome completo" required>
<input name="email" type="email" placeholder="Seu melhor e-mail" required>
<input name="telefone" type="tel" placeholder="(00) 00000-0000" required>
```

### Máscara de Telefone
Aplicar formatação automática `(XX) XXXXX-XXXX` no campo de telefone via JS.

### Validação
- Email: regex básico + verificar se tem @ e domínio
- Telefone: mínimo 10 dígitos após remover máscara
- Nome: mínimo 2 caracteres

### Submit — Ordem de Execução
1. `e.preventDefault()`
2. Validar campos
3. Montar payload
4. `dataLayer.push()` com campos padrão GTM (ler `references/tracking-gtm.md`)
5. `fetch()` POST para webhook Make
6. Disparar animação de confete/fogos
7. Após 2.5s de animação → redirect para `obrigado.html`

### dataLayer.push — Padrão Obrigatório
```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event: 'form_submit_success',
  email: emailValue,
  phoneNumber: phoneDigitsOnly,      // APENAS dígitos, sem máscara
  nome: firstName,
  sobrenome: lastName || '',          // string vazia se não tiver
  apex_session_id: sessionId,
  time_on_page_at_submit: Math.round((Date.now() - pageStart) / 1000)
});
```

As chaves DEVEM ser exatamente essas — não usar `lead_email`, `lead_phone`, etc. Ler `references/tracking-gtm.md` para detalhes completos.

### Webhook Make
```javascript
fetch(WEBHOOK_URL, {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    nome: fullName,
    email: emailValue,
    telefone: phoneDigitsOnly,
    source: 'masterclass-lp',
    timestamp: new Date().toISOString()
  })
});
```

## Animação de Confete/Fogos

Após submit com sucesso, disparar animação fullscreen de confete + fogos de artifício usando Canvas. A animação deve:

- Durar ~2.5 segundos
- Cobrir toda a tela com z-index máximo
- Ter partículas coloridas caindo (confete) + explosões radiais (fogos)
- Usar requestAnimationFrame para performance
- Após finalizar, fazer redirect suave para obrigado.html

Implementar com Canvas 2D puro — sem bibliotecas externas.

### Confete — Parâmetros
- 150-200 partículas
- Cores: vermelho, laranja, amarelo, branco, dourado
- Tamanho: retângulos 8-15px com rotação
- Gravidade + resistência do ar
- Spawnam do topo da tela

### Fogos — Parâmetros
- 3-5 explosões em posições aleatórias
- Cada explosão: 30-50 partículas radiais
- Cores brilhantes com fade out
- Trail effect (rastro)

## Página de Obrigado (obrigado.html)

### Estrutura
1. **Header** com logo/nome do evento
2. **Mensagem de confirmação** com ícone de check animado
3. **Barra de progresso** (3 etapas)
4. **Cards de ação** para cada etapa
5. **Countdown** para o evento

### Barra de Progresso

```
[✅ Inscrição] ———— [⬜ WhatsApp] ———— [⬜ Agenda]
     33%
```

Comportamento:
- Inicia em 33% (etapa 1 já completa)
- Quando clica em "Entrar no grupo" → marca etapa 2, avança para 66%
- Quando clica em "Salvar na agenda" → marca etapa 3, avança para 100%
- Salvar estado no localStorage para persistir se recarregar
- Animação suave na barra (transition width 0.5s)

### Card: Entrar no Grupo do WhatsApp
- Ícone do WhatsApp (SVG inline)
- Texto: "Entre no grupo exclusivo para receber materiais e atualizações"
- Botão verde: "Entrar no Grupo" → abre link em nova aba
- Ao clicar: marcar etapa como completa

### Card: Salvar na Agenda
- Dois botões lado a lado:
  - **Google Calendar**: gera link `calendar.google.com/calendar/render?action=TEMPLATE&...`
  - **Microsoft/Outlook**: gera arquivo `.ics` para download
- Parâmetros do evento:
  - Título: nome da masterclass
  - Data/hora: conforme informado
  - Duração: 1h30 (padrão)
  - Descrição: "Masterclass gratuita — link de acesso será enviado por email e WhatsApp"

### Google Calendar Link
```javascript
const gcalUrl = `https://calendar.google.com/calendar/render?action=TEMPLATE` +
  `&text=${encodeURIComponent(eventTitle)}` +
  `&dates=${startISO}/${endISO}` +  // formato: 20260318T200000/20260318T213000
  `&details=${encodeURIComponent(eventDescription)}` +
  `&location=Online`;
```

### Arquivo .ics (Outlook/Microsoft)
```
BEGIN:VCALENDAR
VERSION:2.0
BEGIN:VEVENT
DTSTART:20260318T230000Z
DTEND:20260319T003000Z
SUMMARY:Nome da Masterclass
DESCRIPTION:Masterclass gratuita
LOCATION:Online
END:VEVENT
END:VCALENDAR
```
Gerar como Blob e disparar download.

## Efeitos e Animações — Checklist Obrigatório

Implementar TODOS os efeitos abaixo (detalhes em `references/animations.md`):

### Obrigatórios
- [ ] Background grid sutil (`.bg-grid`)
- [ ] Glow radial no hero e rodapé (`.bg-glow`) — cor VERMELHA
- [ ] Fade-in com slide up em TODOS os elementos no scroll
- [ ] Delays escalonados nos cards
- [ ] CTA com glow vermelho + hover lift
- [ ] Texto gradiente no H1 (branco → cinza)
- [ ] Focus glow nos inputs do form
- [ ] Máscara de telefone
- [ ] Badge pulsante "VAGAS LIMITADAS"
- [ ] Countdown no banner em tempo real

### Recomendados
- [ ] Borda rotativa (spinning gradient) nos cards de dor — cor VERMELHA
- [ ] Shimmer/brilho deslizante nos destaques
- [ ] Contador animado nos números de impacto
- [ ] Partículas Canvas vermelhas/laranja na seção de problema

### Diferenciais
- [ ] 3D tilt nos cards (desabilitar em mobile)
- [ ] SVG ring progress nos ícones
- [ ] Confete + fogos no submit do form

## Responsividade

Breakpoints obrigatórios:
- **768px:** Hero passa de split para stacked (texto em cima, form embaixo)
- **600px:** Ajustar tamanhos de fonte, padding
- **414px:** iPhone Plus / Android — margens mínimas
- **360px:** iPhone SE / Android compacto

Em mobile:
- Desabilitar 3D tilt e partículas canvas (performance)
- Banner compacto (sem countdown detalhado se não couber)
- Form full-width
- Cards empilhados

## Performance

- Imagens: usar formato WebP quando disponível, JPEG como fallback
- Lazy loading em imagens abaixo do fold
- Minificar CSS/JS inline (não precisa ser perfeito, mas remover comentários dev)
- Canvas animations: usar requestAnimationFrame, não setInterval
- Debounce no resize listener do countdown

## Variáveis de Configuração

No topo do `<script>`, centralizar todas as variáveis editáveis:

```javascript
// ========== CONFIGURAÇÃO ==========
const CONFIG = {
  eventName: 'Nome da Masterclass',
  eventDate: '2026-03-18T20:00:00-03:00',  // ISO com timezone
  eventDuration: 90,  // minutos
  webhookUrl: 'https://hook.us2.make.com/SEU_WEBHOOK_ID',
  whatsappGroupUrl: 'https://chat.whatsapp.com/SEU_GRUPO',
  accentColor: '#DC2626',
  accentColorRgb: '220, 38, 38',
  maxSlots: 200,  // número de vagas (cosmético)
};
```

## Entrega Final

1. Gerar `index.html` e `obrigado.html` na pasta do projeto
2. Garantir que as imagens da pasta `img/` são referenciadas com caminhos relativos (`img/nome-do-arquivo.ext`)
3. Testar responsividade nos breakpoints
4. Validar que o dataLayer.push segue o padrão GTM (ler `references/tracking-gtm.md`)
5. Verificar que o countdown funciona corretamente com a data informada
