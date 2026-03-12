# Estrutura Completa das Páginas — Masterclass LP

## Visão Geral

Duas páginas HTML independentes, single-file (CSS + JS inline), dark theme.

---

## PÁGINA 1: index.html (Landing Page)

### Configuração Global

No topo do `<script>`, centralizar variáveis:

```javascript
const CONFIG = {
  eventName: 'A Morte da Consultoria Artesanal',
  eventDate: '2026-03-17T18:00:00-03:00',
  eventDuration: 90,
  webhookUrl: 'https://hook.us2.make.com/WEBHOOK_ID',
  whatsappGroupUrl: 'https://chat.whatsapp.com/GRUPO_ID',
  accentColor: '#DC2626',
  accentColorRgb: '220, 38, 38',
  maxSlots: 200,
};
```

### Seção 0: Banner Sticky (Topo)

Fixo no topo da página, z-index 9999.

```
[🔴 AO VIVO] Masterclass Gratuita — 10 de Março às 18h | ⏰ Faltam Xd Xh Xm Xs
```

- Background: gradient vermelho escuro → preto
- Countdown JS atualizando a cada segundo
- Quando o countdown zera: trocar para "🔴 ESTAMOS AO VIVO!"
- Height: ~48px desktop, ~40px mobile
- Font size: 13-14px
- Fechar (X) no canto direito para quem quiser dispensar

### Seção 1: Hero (Layout Split)

**Layout desktop:** Flex row, gap 48px
- Coluna esquerda (55-60%): Texto + CTA
- Coluna direita (40-45%): Formulário

**Coluna Esquerda — Copy:**

```
[Badge pulsante] 🔴 VAGAS LIMITADAS — MASTERCLASS GRATUITA

[H1 - texto gradiente branco→cinza]
Sua consultoria está crescendo…
ou só adiando a própria morte?

[Subtítulo - cor secundária]
Escala e recorrência não é ambição.
É sobrevivência.

[Info do evento]
📅 17 de março às 18h | Ao vivo e sem replay
```

**Coluna Direita — Formulário:**

Card com:
- backdrop-filter: blur(20px)
- background: rgba(255,255,255,0.05)
- border: 1px solid rgba(255,255,255,0.1)
- border-radius: 20px
- padding: 40px 32px

Conteúdo:
```
[Título] Garanta sua vaga gratuita
[Subtítulo] Ao vivo. Sem replay. Sem gravação.

[Campo] Nome completo
[Campo] Seu melhor e-mail
[Campo] WhatsApp (com máscara)

[Botão CTA] QUERO PARTICIPAR AO VIVO →
  - Background: var(--accent) vermelho
  - Box-shadow glow pulsante
  - Full width

[Texto escassez] 🔥 Apenas {X} vagas restantes
```

### Seção 2: Bloco de Tensão / Problema

**Background:** Imagem do cemitério com overlay escuro (gradient de cima para baixo)

**Layout:** Duas colunas
- Esquerda (55%): Copy de tensão
- Direita (45%): Imagem do consultor no cemitério (evolutto masterclass .webp)

**Copy da esquerda:**

```
[H2]
Se o seu faturamento depende de você,
seu crescimento já tem um teto.

[Cards de dor - com borda rotativa vermelha]
Se:
• Cada cliente novo aumenta sua operação
• Sua agenda define seu faturamento
• Você ainda vende hora
• Vive de indicação
• Precisa estar presente em tudo

[H3 - destaque vermelho]
Você não tem escala.
Você tem dependência.

[Texto impacto]
E dependência não cresce.
Ela estica… até romper.

[CTA Button]
QUERO PARTICIPAR AO VIVO →

[Subtexto]
Ao vivo e sem replay
```

**Efeitos nesta seção:**
- Partículas Canvas vermelhas/laranja
- Cards com borda rotativa (spinning gradient border) vermelha
- Fade-in escalonado nos bullet points
- Imagem com parallax sutil no scroll

### Seção 3: Solução / O que vai aprender

**Background:** Dark sólido, sem imagem

**Layout:** Duas colunas
- Esquerda (55%): Copy
- Direita (45%): Segunda imagem (evolutto masterclass.webp — split cemitério/futuro tech)

**Copy:**

```
[Eyebrow] O QUE VOCÊ VAI DESCOBRIR

[H2]
Consultorias não morrem por falta de clientes.
Morrem por modelo.

[Subtítulo]
Mais vendas não resolvem estrutura errada.

[Cards de aprendizado — com hover 3D tilt + shimmer]
Na aula você vai entender:
1. O erro que trava consultorias lucrativas
2. A diferença entre expandir e escalar
3. Onde está o gargalo invisível
4. O que precisa existir antes da próxima venda
5. Como transformar expertise em ativo

[Bloco de diferenciação]
Sem motivação. Sem fórmula. Sem atalhos.
Apenas estrutura.

[Destaque]
Ao vivo. Sem replay.
Quem estiver presente receberá as próximas instruções estratégicas.

[CTA]
QUERO GARANTIR MINHA VAGA →
```

### Seção 4: CTA Final

- Background com glow vermelho intenso
- Repetição do formulário OU botão que faz smooth scroll até o hero
- Contador animado: "+2.700 consultores já garantiram vaga"
- Countdown compacto
- Máxima urgência visual

### Seção 5: Footer

Mínimo:
```
© 2026 [Nome da empresa]. Todos os direitos reservados.
Ao se inscrever, você concorda com nossa Política de Privacidade.
```

---

## PÁGINA 2: obrigado.html (Thank You Page)

### Header
- Logo/nome do evento
- Background dark consistente com a LP

### Confirmação
- Ícone de check animado (SVG com stroke-dashoffset animation)
- H1: "Inscrição Confirmada! 🎉"
- Texto: "Sua vaga está garantida para a masterclass [NOME] no dia [DATA]"

### Barra de Progresso (3 Etapas)

```
[✅ Inscrição] ———————— [⬜ WhatsApp] ———————— [⬜ Agenda]
|========                                                  |
         33%
```

Implementação:
- 3 círculos conectados por linha
- Círculo ativo: preenchido com accent color
- Círculo pendente: borda, fundo transparente
- Linha entre etapas: preenche gradualmente com accent color
- Width da barra animada via CSS transition

Estado persistido em localStorage:
```javascript
const progress = JSON.parse(localStorage.getItem('mc_progress') || '{"step1":true,"step2":false,"step3":false}');
```

### Card: Grupo do WhatsApp

```
[Ícone WhatsApp SVG verde]

Entre no grupo exclusivo
Receba materiais, links e atualizações antes do evento.

[Botão verde] ENTRAR NO GRUPO DO WHATSAPP →
```

Ao clicar:
1. `window.open(whatsappUrl, '_blank')`
2. Marcar step2 = true no localStorage
3. Atualizar visual da barra para 66%
4. Mudar botão para "✅ Você já está no grupo"

### Card: Salvar na Agenda

```
[Ícone Calendário SVG]

Salve na sua agenda
Não perca a data — adicione agora ao seu calendário.

[Botão] 📅 Google Calendar    [Botão] 📅 Outlook/Apple
```

**Google Calendar:** Gerar URL com parâmetros:
```
https://calendar.google.com/calendar/render?action=TEMPLATE
  &text=A Morte da Consultoria Artesanal
  &dates=20260317T210000Z/20260317T223000Z
  &details=Masterclass gratuita ao vivo...
  &location=Online
```

**Outlook/ICS:** Gerar Blob .ics e disparar download:
```
BEGIN:VCALENDAR
VERSION:2.0
PRODID:-//Masterclass//LP//PT
BEGIN:VEVENT
DTSTART:20260317T210000Z
DTEND:20260317T223000Z
SUMMARY:A Morte da Consultoria Artesanal
DESCRIPTION:Masterclass gratuita ao vivo
LOCATION:Online
END:VEVENT
END:VCALENDAR
```

Ao clicar em qualquer um:
1. Abrir link/download
2. Marcar step3 = true no localStorage
3. Atualizar barra para 100%
4. Mostrar mensagem de parabéns

### Countdown para o Evento
- Abaixo dos cards
- Mesmo formato do banner da LP
- "Faltam X dias, X horas, X minutos para a masterclass"

### Estado 100% Completo
Quando todas etapas concluídas:
- Barra 100% preenchida
- Confete sutil (menos intenso que o do form)
- Mensagem: "Perfeito! Você está 100% preparado. Nos vemos ao vivo! 🚀"

---

## Mapeamento de Imagens

| Arquivo | Uso na LP |
|---------|-----------|
| `img/Imagem.jpg.jpeg` | Background do hero ou seção de problema — lápide "Consultoria Presencial 2026" |
| `img/WhatsApp Image 2026-02-27 at 17.47.41.jpeg` | Seção de problema ou complemento — ampulheta + contrato queimando |
| `img/evolutto masterclass .webp` | Seção de tensão coluna direita — cemitério de consultores |
| `img/evolutto masterclass.webp` | Seção de solução coluna direita — split cemitério (P&B) vs. consultor tech |
