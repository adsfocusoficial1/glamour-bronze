# Auditoria LP — glamour-bronze
**Auditora:** Lara | **Data:** 2026-05-04 | **Arquivo auditado:** lp-glamour-bronze.html

## Resumo Executivo
- 🚨 CRÍTICOS: 1 (pendente — ativação FormSubmit.co)
- ⚠️ IMPORTANTES: 1 restante (depoimentos fictícios — aguardando Débora)
- ✅ CORRIGIDOS: 3 IMPORTANTES + 4 SUGESTÕES (2026-05-04)
- ✅ OK: 10

---

## Problemas por categoria

### 🚨 CRÍTICOS (bloqueia entrega)

**C1 — Formulário: FormSubmit.co exige ativação por email antes de funcionar**
- **Trecho:** `fetch('https://formsubmit.co/ajax/glamourbronzeofc@gmail.com', ...)`
- **Problema:** O FormSubmit.co intercepta a PRIMEIRA submissão e envia um email de ativação para glamourbronzeofc@gmail.com. Se a Débora não clicar no link de ativação, TODOS os leads enviados antes dessa confirmação são perdidos silenciosamente — o formulário mostra o `.form-success` mas o email nunca chega.
- **Correção obrigatória antes de ir ao ar:** Fazer uma submissão de teste, acessar glamourbronzeofc@gmail.com e clicar no link "Activate Form" que o FormSubmit.co vai enviar. Só depois abrir a LP para tráfego real.

---

### ⚠️ IMPORTANTES (corrigir antes de ir ao ar)

**I1 — SEO: OG tags ausentes (preview feio no WhatsApp e Instagram)**
- **Trecho:** `<head>` — sem nenhuma `<meta property="og:...">` ou `<meta name="twitter:...">`
- **Problema:** Quando a URL for compartilhada no WhatsApp ou Instagram, vai aparecer sem imagem de preview, sem título formatado e sem descrição. O PRD previa OG tags explicitamente.
- **Correção:** Adicionar ao `<head>`:
```html
<meta property="og:title" content="Glamour Bronze — Bronzeamento Natural em Jacobina-BA" />
<meta property="og:description" content="Bronze uniforme, seguro e duradouro em Jacobina-BA. Agende com a Débora pelo WhatsApp." />
<meta property="og:image" content="img/espreguicadeiras-hero.jpeg" />
<meta property="og:type" content="website" />
```

**I2 — Dados: Depoimentos sem foto real e com nomes genéricos — REVISÃO PENDENTE**
- **Trechos:**
  - `<strong>Luana M.</strong><span>Cliente · Jacobina</span>` — avatar colorido com inicial "L"
  - `<strong>Raquel S.</strong><span>Cliente · Jacobina</span>` — avatar colorido com inicial "R"
  - `<strong>Camila A.</strong><span>Cliente · Jacobina</span>` — avatar colorido com inicial "C"
- **Problema:** Nomes genéricos (sobrenome abreviado), sem foto real (gradiente dourado no lugar da foto), sem verificação de autoria. PRD exige "depoimentos reais com foto e autorização" como dependência não resolvida.
- **Correção:** Levar à Débora para aprovação ou substituição por depoimentos reais (nome completo + foto autorizadas). Enquanto não tiver reais, deixar a seção como placeholder visível internamente — não publicar com dados fictícios.

**I3 — Copy: Formas de pagamento não confirmadas com o cliente**
- **Trecho (FAQ):** `<p>Aceitamos Pix, cartão de débito e crédito. O pagamento é feito no dia do atendimento.</p>`
- **Problema:** O PRD marcou explicitamente este item como `[A confirmar com Débora]`. O dado foi preenchido sem confirmação — se a Glamour Bronze não aceitar cartão de crédito, a LP vai gerar expectativa errada e atrito na hora do pagamento.
- **Correção:** Confirmar com Débora quais formas de pagamento são aceitas e corrigir o texto. Se não confirmar a tempo, substituir por: *"Consulte as formas de pagamento disponíveis ao agendar."*

**I4 — SEO técnico: Schema.org LocalBusiness ausente**
- **Trecho:** `<head>` — sem nenhum `<script type="application/ld+json">` com LocalBusiness
- **Problema:** O PRD previa explicitamente Schema.org LocalBusiness (name, address, telephone, openingHours, priceRange). Sem ele, o Google não gera rich snippets para a página.
- **Correção:** Adicionar antes do `</head>`:
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "Glamour Bronze",
  "telephone": "+55-74-99159-8379",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "Estrada da Maçonaria, nº 08",
    "addressLocality": "Jacobina",
    "addressRegion": "BA",
    "postalCode": "44706-685",
    "addressCountry": "BR"
  },
  "openingHoursSpecification": {
    "@type": "OpeningHoursSpecification",
    "dayOfWeek": ["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"],
    "opens": "08:00",
    "closes": "15:00"
  },
  "priceRange": "R$100-R$300",
  "url": "https://glamourbronze.vercel.app"
}
</script>
```

---

### 💡 SUGESTÕES (melhorias opcionais)

**S1 — Copy emocional: "mulher mais incrível de Jacobina" — restrição geográfica em frase emocional**
- **Trecho:** `"Mais do que um bronze bonito, quero que você saia daqui se sentindo a mulher mais incrível de Jacobina."`
- **Contexto:** O negócio É local, então Jacobina nas seções objetivas está correto. Mas essa frase é emocional e cria uma barreira psicológica para visitantes de Irecê, Senhor do Bonfim ou outras cidades alcançadas pelo Meta Ads. Se o tráfego for regional, considerar ajustar.
- **Sugestão:** *"...se sentindo a mulher mais linda e confiante do mundo."* — sem recorte geográfico.

**S2 — Imagem: card "Biquínis de tecido" usa foto errada**
- **Trecho:** `<img src="img/espreguicadeiras-mural.jpeg" alt="Biquínis de tecido" loading="lazy" />`
- **Problema:** A imagem referenciada é a do mural de coqueiros (usada também na galeria do espaço como "Cantinho dos coqueiros"). O alt text "Biquínis de tecido" não condiz com a imagem real.
- **Sugestão:** Substituir por foto real dos biquínis disponíveis para venda, ou remover o card se não tiver foto adequada.

**S3 — Identidade: Logo do cliente ausente**
- **Trecho:** `<a href="#top" class="logo">Glamour <span class="sun">Bronze</span></a>` — texto tipográfico sem imagem
- **Contexto:** Briefing menciona "Modelos de logo (Looka)" disponíveis no Drive, mas nenhuma imagem de logo foi integrada. A LP usa apenas o nome estilizado em Cormorant Garamond como logo.
- **Sugestão:** Verificar com a Débora se os logos do Drive estão aprovados. Se sim, adicionar `<img>` com o logo real no nav e footer para reforçar brand recall.

**S4 — LGPD: Cookie banner ausente**
- **Trecho:** `<body>` — sem cookie banner
- **Contexto:** PRD previa "Cookie banner simples (texto + botão aceitar)" como requisito. Ausente na versão atual.
- **Sugestão:** Adicionar banner simples no rodapé/base da tela: *"Usamos cookies para melhorar sua experiência. [Aceitar]"*

**S5 — Tipografia: Divergência de fonte em relação ao PRD**
- **Trecho CSS:** `@import` de `Cormorant Garamond` para headings
- **PRD dizia:** *"Fontes: Poppins (títulos) + Inter (corpo)"*
- **Contexto:** PRD dizia "validar com Débora" antes de desenvolver — possível que o squad tenha tomado decisão própria. A escolha Cormorant Garamond é esteticamente superior para um negócio de beleza premium.
- **Sugestão:** Confirmar com Débora se aprova a fonte atual ou prefere Poppins conforme o PRD original.

---

### ✅ OK

1. **Viewport meta tag** — `<meta name="viewport" content="width=device-width, initial-scale=1">` presente ✓
2. **WhatsApp número correto** — `5574991598379` confere com briefing (+55 74 9159-8379) em todos os CTAs ✓
3. **Endereço** — "Estrada da Maçonaria, nº 08 · Bairro Catuaba · Jacobina · Bahia · CEP 44706-685" confere com briefing ✓
4. **CNPJ** — 62.787.804/0001-30 presente no footer ✓
5. **Ordem de seções** — Hero → Espaço → Experiência → Serviços → Segurança → Depoimentos → Débora → **Formulário** → **FAQ** → **Restrições** → Footer. FAQ e Importante Saber vêm DEPOIS do formulário ✓
6. **Hamburger mobile** — implementado para ≤800px com overlay full-screen funcional ✓
7. **Media queries** — hero (900px), gallery (800px), serv-grid (1024px/420px), exp-grid (900px), form-grid (900px), footer (800px), mobile fixes (600px) ✓
8. **Alt texts** — todas as `<img>` com alt descritivo. Única exceção: imagem errada no card biquínis (ver S2) ✓
9. **Title e meta description** — preenchidos e descritivos ✓
10. **h1 único** — `<h1>Mais cor, mais confiança, <em>mais você.</em></h1>` — único na página ✓
11. **Tipografia** — 2 famílias por seção máximo: Cormorant Garamond (display/headings) + Inter (corpo/labels) ✓
12. **Nav contraste** — `.nav::before` com `rgba(0,0,0,0.55)` garante leitura do texto branco sobre hero com imagem ✓
13. **Formulário com feedback** — `.form-success` + btn ocultado após envio ✓
14. **FAB WhatsApp** — presente, fixo, funcional, com número correto ✓
15. **CSS autocontido** — estilos inline no `<style>`, sem dependência externa de `styles.css` ✓

---

## Próximos passos (em ordem de prioridade)

1. **[ANTES DE PUBLICAR]** Fazer envio de teste no formulário → acessar glamourbronzeofc@gmail.com → ativar o FormSubmit.co clicando no link de confirmação
2. **[ANTES DE PUBLICAR]** Confirmar com Débora as formas de pagamento (Pix? Cartão? Dinheiro?) e atualizar o FAQ
3. **[ANTES DE PUBLICAR]** Adicionar OG tags no `<head>` para preview correto no WhatsApp/Instagram
4. **[ANTES DE PUBLICAR]** Levar os 3 depoimentos à Débora para aprovação — substituir por reais ou obter autorização formal
5. Adicionar Schema.org LocalBusiness no `<head>`
6. Corrigir imagem do card "Biquínis de tecido" (usar foto real ou remover o card)
7. Verificar com Débora se logos do Drive estão aprovados para uso
8. Adicionar cookie banner LGPD
9. Confirmar aprovação da fonte Cormorant Garamond (vs Poppins do PRD)
10. Avaliar ajuste na deb-quote se campanhas de Meta Ads forem regionais (fora de Jacobina)
