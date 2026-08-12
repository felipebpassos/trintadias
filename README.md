# 30 dias para sair do fundo do poço — Landing Page

Página de vendas em HTML + Tailwind (CDN), mobile first, com espaço pronto para
Meta Pixel, Google Analytics 4, Google Ads e GTM.

Acesso local: <http://localhost/trintadias/>

## O que editar (tudo em um lugar)

Abra `index.html` e procure o bloco **`window.LP_CONFIG`** (perto do fim do arquivo):

```js
window.LP_CONFIG = {
  CHECKOUT_URL: "https://pay.hotmart.com/SEU-CODIGO-AQUI", // link do checkout
  YOUTUBE_ID: "",      // só o código do vídeo (ex.: dQw4w9WgXcQ)
  FB_PIXEL_ID: "",     // Meta Pixel — vazio = desativado
  GA4_ID: "",          // ex.: G-XXXXXXXXXX
  GOOGLE_ADS_ID: "",   // ex.: AW-123456789
  GTM_ID: "",          // ex.: GTM-XXXXXXX
};
```

O `CHECKOUT_URL` é aplicado automaticamente nos 4 botões da página
(`#pay1`, `#pay2`, `#pay3`, `#pay4`). O vídeo carrega o player do YouTube
**somente no clique** — a página abre rápido mesmo em internet ruim.

## Antes de publicar (checklist)

- [ ] Trocar `SEUDOMINIO.com.br` pelo domínio real em: `index.html` (canonical,
      Open Graph, JSON-LD), `robots.txt` e `sitemap.xml`.
- [ ] Criar a imagem de compartilhamento em `img/og-cover.jpg` (1200x630px) —
      é a imagem que aparece quando o link é enviado no WhatsApp.
- [ ] Preencher `LP_CONFIG` com o link do checkout, o ID do vídeo e os pixels.
- [ ] **Depoimentos:** o bloco "Quem já começou" está com textos de exemplo
      entre colchetes. Substitua por depoimentos reais e autorizados — ou
      apague o bloco inteiro. Depoimento inventado é propaganda enganosa
      (CDC, art. 37) e derruba conta de anúncio.
- [ ] Conferir preço e parcelamento na dobra de oferta (hoje: R$ 197 → R$ 97)
      e o mesmo valor no JSON-LD e no evento `InitiateCheckout`.
- [ ] Confirmar que a garantia de 7 dias combina com a regra do checkout.
- [ ] Criar `politica-de-privacidade.html` e `termos-de-uso.html`
      (links no rodapé) — o Google Ads exige.

## Eventos disparados

| Evento              | Quando                          | Vai para       |
| ------------------- | ------------------------------- | -------------- |
| `PageView`          | ao abrir a página               | Pixel          |
| `ViewContent`       | ao dar play no vídeo            | Pixel + GA4    |
| `InitiateCheckout`  | ao clicar em qualquer CTA       | Pixel + GA4    |

Para acompanhar a venda concluída, configure o `Purchase` na plataforma de
checkout (Hotmart/Kiwify já integram com o Pixel e o GA4 pelo painel deles).

## Estrutura da página (5 dobras)

1. **Hero** — título, vídeo e CTA
2. **Identificação** — as dores de quem usa e de quem convive
3. **Como funciona** — os 30 dias em 4 etapas + o que recebe + CTA
4. **Quem conduz** — posicionamento, aviso legal e depoimentos
5. **Oferta** — preço, garantia, FAQ e CTA final

## Observações de conformidade

A copy foi escrita **sem** prometer cura, sem citar tempo garantido de
abstinência e sem se apresentar como tratamento clínico. Os avisos de que o
programa não substitui acompanhamento médico/psicológico e o contato do
CVV (188) estão na dobra 4 e no rodapé — não remova.

## Arquivos

```
trintadias/
├── index.html      # a página inteira (HTML + CSS + JS)
├── robots.txt
├── sitemap.xml
├── .htaccess       # gzip, cache e headers
└── img/            # coloque aqui og-cover.jpg e o favicon
```

## Opcional: Tailwind compilado

A página usa o Tailwind via CDN (`cdn.tailwindcss.com`), que é ótimo para
publicar rápido, mas processa o CSS no navegador. Se quiser mais velocidade
depois, dá para gerar um `style.css` estático com o Tailwind CLI e trocar a
tag `<script src="https://cdn.tailwindcss.com">` por um `<link rel="stylesheet">`.
