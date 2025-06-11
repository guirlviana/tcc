## Relatório de Acessibilidade e Performance - Otimização do `index.html`

Este relatório detalha as otimizações implementadas no arquivo `index.html` para melhorar sua acessibilidade e performance. As mudanças foram realizadas com o objetivo de tornar o site mais utilizável para todos os usuários, incluindo aqueles com deficiências, e para garantir um carregamento mais rápido e eficiente.

### Problemas Identificados e Soluções Implementadas

Foram identificados diversos problemas de acessibilidade e performance no código original. Abaixo, detalho cada problema e as respectivas soluções aplicadas:

#### Acessibilidade

1.  **Contraste de Cores Insuficiente:**

    - **Problema:** Várias seções do site apresentavam baixo contraste entre a cor do texto e a cor de fundo, dificultando a leitura para usuários com baixa visão ou daltonismo. Exemplos incluíam `body`, `.destaque`, `.mini-menu span`, `.popup`, `.carrossel-item`, `.tab-buttons span`, `.tab-content`, `.dropdown-content div`, `.tooltip .tooltip-text`, botões com `background:#ddd; border:none; color:#999;` e tabelas.
    - **Solução:** Ajustadas as cores de fundo e texto para garantir um contraste mínimo aceitável (geralmente uma proporção de 4.5:1 para texto normal e 3:1 para texto grande, conforme WCAG 2.1 AA).

2.  **Imagens sem Atributo `alt`:**

    - **Problema:** A maioria das tags `<img>` não possuía o atributo `alt`, o que impede leitores de tela de descreverem o conteúdo da imagem para usuários com deficiência visual.
    - **Solução:** Adicionados atributos `alt` descritivos a todas as tags `<img>`. Para imagens decorativas, `alt=""` foi utilizado.

3.  **Navegação por Teclado e Foco:**

    - **Problema:** Elementos interativos como `div`s e `span`s usadas como botões ou links (`.topo div`, `.mini-menu span`, `.tab-buttons span`, `.dropdown div`, `.social-icons span`, `.modal-trigger`) não eram focáveis via teclado e não possuíam semântica apropriada para interatividade, dificultando a navegação para usuários que dependem do teclado.
    - **Solução:** Convertidos elementos interativos para `<a>` (links) ou `<button>` (botões) conforme a funcionalidade. Adicionados `tabindex="0"` a elementos que precisam ser focáveis, mas não são semanticamente links ou botões. Adicionados `role="button"` ou `role="link"` quando a semântica de `div` ou `span` foi mantida. Adicionada estilização `:focus` para todos os elementos interativos para indicar o foco do teclado.

4.  **Estrutura Semântica do HTML:**

    - **Problema:** Uso excessivo de `div`s genéricas onde elementos semânticos mais apropriados poderiam ser utilizados (ex: `nav` para navegação, `main` para conteúdo principal, `section` para blocos de conteúdo, `footer` para o rodapé).
    - **Solução:** Adicionado `<nav>` para a navegação do topo e `mini-menu`. Adicionado `<main>` para o conteúdo principal. Utilizado `<section>` para os blocos de conteúdo (`.bloco`). Adicionado `<footer>` para o rodapé.

5.  **Labels em Formulários:**

    - **Problema:** Os campos de formulário (`input`) não possuíam `<label>`s associados, o que é crucial para leitores de tela e para a usabilidade geral. O `placeholder` não substitui um `label`.
    - **Solução:** Adicionados `<label>`s explícitos para cada campo de entrada e associados via atributos `for` e `id`.

6.  **ARIA Roles e Propriedades (Onde Necessário):**

    - **Problema:** Componentes complexos como carrosséis, tabs, dropdowns e modais (mesmo que simplificados no HTML original) não possuíam os atributos ARIA necessários para comunicar seu estado e funcionalidade a tecnologias assistivas.
    - **Solução:** Adicionados atributos ARIA: `role="region"` e `aria-label` para o carrossel, `role="tablist"`, `role="tab"`, `aria-controls` e `aria-labelledby` para as tabs, `role="button"`, `aria-haspopup="true"`, `aria-expanded="false"`, `role="menu"` e `role="menuitem"` para o dropdown, `role="dialog"` e `aria-modal="true"` para o popup, `role="tooltip"` e `aria-describedby` para o tooltip. Adicionado `aria-label` para os botões de controle de vídeo e ícones sociais. Adicionado `role="table"`, `role="rowgroup"`, `role="row"`, `role="columnheader"`, `role="cell"` e `<caption>` para a tabela.

7.  **Tamanho Adequado de Elementos Clicáveis:**

    - **Problema:** Alguns elementos clicáveis, como os ícones de redes sociais e os botões de controle de vídeo, eram muito pequenos, dificultando o clique para usuários com deficiência motora ou que usam telas sensíveis ao toque.
    - **Solução:** Aumentado o `padding` ou as dimensões mínimas para esses elementos para garantir uma área de clique de pelo menos 44x44 pixels, conforme as diretrizes.

8.  **Hierarquia de Cabeçalhos:**

    - **Problema:** Embora o uso de `<h4>` fosse consistente, a falta de `<h1>`, `<h2>` ou `<h3>` no topo da página ou para seções mais importantes pode prejudicar a navegação por cabeçalhos para usuários de leitores de tela.
    - **Solução:** Adicionado um `<h1>` oculto (`.sr-only`) para o título principal do site, garantindo que a hierarquia comece corretamente.

9.  **Links e Botões:**

    - **Problema:** Muitos elementos que funcionavam como links ou botões eram `div`s ou `span`s com `onclick` JavaScript. Isso não oferece semântica adequada, não são focáveis por padrão e não são anunciados corretamente por leitores de tela.
    - **Solução:** Convertidos para `<a>` ou `<button>` tags HTML sempre que possível, e adicionado `aria-label` onde o texto visível não era suficientemente descritivo.

10. **Conteúdo dinâmico (Carrossel, Tabs, Modals, Tooltips):**

    - **Problema:** A implementação básica não fornecia feedback sobre o estado atual ou controles de navegação para tecnologias assistivas.
    - **Solução:** Atributos ARIA foram adicionados para indicar a natureza interativa dos componentes. Para uma solução completa, seria necessário JavaScript para manipular `aria-current`, `aria-selected`, `aria-expanded`, e o foco do teclado.

11. **CAPTCHA Inacessível:**
    - **Problema:** O CAPTCHA baseado em imagem não oferece alternativas para usuários que não conseguem ver a imagem (ex: cegos, baixa visão).
    - **Solução:** Adicionada uma nota indicando que, em um cenário real, um CAPTCHA acessível (como reCAPTCHA v3, ou uma alternativa de áudio/pergunta) seria essencial.

#### Performance

1.  **Imagens Não Otimizadas e Sem Dimensões:**

    - **Problema:** As imagens (`.large-image-container img`, e as imagens nos blocos) não estavam otimizadas para a web (tamanhos de arquivo potencialmente grandes) e não possuíam atributos `width` e `height` no HTML, causando Cumulative Layout Shift (CLS) e carregamento lento.
    - **Solução:** Adicionados `width` e `height` intrínsecos a todas as imagens (`<img>`) para evitar CLS.

2.  **Carregamento de Fontes Web (FOIT/FOUT):**

    - **Problema:** As fontes web eram carregadas de forma ineficiente (`font-display: block` causa FOIT - Flash of Invisible Text; `@import` ou `<link>` bloqueiam a renderização).
    - **Solução:** Removido `@font-face` e `<link href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap" rel="stylesheet">`. Recomendado o uso de `font-display: swap` para evitar FOIT, e substituído o `@import` por `<link rel="preconnect">` e `<link rel="stylesheet">` com `font-display: swap` para a fonte Roboto.

3.  **Animações que Podem Causar Problemas:**

    - **Problema:** A propriedade `will-change: transform;` foi usada desnecessariamente na classe `.animated-element`, o que pode, em alguns casos, consumir recursos e não ter o efeito de otimização desejado se não for usada criteriosamente.
    - **Solução:** Removido `will-change: transform;` da classe `.animated-element`.

4.  **Uso de GIFs em Vez de Vídeos:**

    - **Problema:** GIFs animados são geralmente maiores em tamanho de arquivo e menos eficientes que vídeos (`.mp4`, `.webm`) para conteúdo animado complexo.
    - **Solução:** Adicionada uma nota de recomendação para substituir GIFs por elementos `<video>` com atributos `autoplay`, `loop`, `muted` e `playsinline` quando a animação não tiver áudio e for apenas visual.

5.  **Recursos Não Carregados com Lazy Loading:**

    - **Problema:** Imagens e iframes que estão fora da viewport inicial (abaixo da dobra) eram carregados imediatamente, desperdiçando largura de banda e atrasando o carregamento do conteúdo visível.
    - **Solução:** Adicionado `loading="lazy"` a todas as tags `<img>` que não estão no topo da página e ao `<iframe>` do Google Maps.

6.  **JavaScript Legado/Síncrono:**
    - **Problema:** O uso de `document.write('<script src="https://example.com/legacy-script.js"><\/script>');` é uma prática antiga que pode bloquear a renderização da página.
    - **Solução:** Removido a tag `<script>` com `document.write`. Recomendado que scripts sejam carregados de forma assíncrona (`defer` ou `async`) ou ao final do `<body>`.

### Sumário das Mudanças no Código

O site otimizado incorpora as seguintes mudanças:

- **HTML Semântico:** Uso de `<nav>`, `<main>`, `<section>`, `<footer>`.
- **Acessibilidade no Conteúdo:** Atributos `alt` em todas as imagens, `label`s associados a campos de formulário, elementos interativos convertidos para `<a>` ou `<button>`, atributos ARIA adicionados a componentes complexos, aumento da área de clique, `tabindex="0"` e `role` adicionados, `<h1>` oculto para título principal, e `<caption>` na tabela com atributos `role`.


## Results

![image](https://github.com/user-attachments/assets/cf254617-3661-437f-a358-75ab8d5edfd2)

- **CSS para Acessibilidade:** Ajustes de contraste em múltiplas classes, estilos `:focus` para todos os elementos interativos, e criação da classe `sr-only`.
- **Otimização de Performance:** Atributos `width` e `height` em imagens, `loading="lazy"` para imagens e iframes, remoção de `will-change: transform;` desnecessário, remoção de script síncrono, e otimização do carregamento de fontes web.

Essas mudanças resultam em um site muito mais acessível para usuários com diversas necessidades e com um desempenho de carregamento aprimorado.
