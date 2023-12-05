# [![Voidr](https://img.voidr.co/voidr/compress:100/convert:webp/fetch/https://api.voidr.co/v1/images/raw/voidr/voidr-banner-en_1701195001454.png)](https://en.voidr.co/images)

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Discord](https://img.shields.io/badge/Discord-7289DA?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/Wk6dfhJu)
[![Telegram](https://img.shields.io/badge/Telegram-2CA5E0?style=flat-squeare&logo=telegram&logoColor=white)](https://t.me/comunidadevoidr/1)
[![Twitter Follow](https://img.shields.io/twitter/follow/Voidr_co?style=social)](https://twitter.com/Voidr_co)

# Voidr

O Voidr é uma plataforma robusta e escalável para otimização e redimensionamento de imagens, projetada especificamente para desenvolvedores. Com nossa API intuitiva e flexível, você pode melhorar o desempenho de carregamento de seus aplicativos em minutos, fornecendo imagens otimizadas em formatos de ponta.

[![Voidr Code Example](https://img.voidr.co/voidr/compress:100/convert:webp/fetch/https://api.voidr.co/v1/images/raw/voidr/code-example-clean.png)](https://voidr-images-en.readme.io/reference/intro)

# 🚀 Início rápido

### Configurações do tema

1. Faça login na sua conta do Shopify.
2. Navegue até Loja Online > Temas > Clique nos três pontos > Editar código.
3. Vá para a seção config e edite o arquivo settings_schema.json.

No arquivo `settings_schema.json`, você encontrará uma matriz de configurações.

4. No final deste arquivo, logo após o último caractere `}`, adicione uma vírgula, como este `{`, e inclua o seguinte código:

```json
{
  "name": "Voidr Images",
  "settings": [
    {
      "type": "paragraph",
      "content": "Para mais informações [docs](https://voidr-images.readme.io/reference/intro)"
    },
    {
      "type": "checkbox",
      "id": "voidr_enable",
      "label": "Ativar Voidr Images",
      "info": "Ativar a funcionalidade Voidr Images"
    },
    {
      "type": "text",
      "id": "voidr_project",
      "label": "Voidr Project Name",
      "default": "nome-do-projeto",
      "info": "Nome do projeto que você criou no seu Dashboard"
    }
  ]
}
```

5. Depois disso, no arquivo `snippets`, crie um arquivo chamado `voidr.liquid` e adicione o código abaixo:

```liquid
{% capture image_url %}
    {% if settings.voidr_enable %}
      {% assign voidr_api_url = "https://img.voidr.co" %}
      {% assign src_without_domain = src | split: '//' %}
      {% assign base_url = voidr_api_url | append: '/' | append: settings.voidr_project %}
      {% assign params = '' %}

      {% if compress %}
        {% assign params = params | append: 'compress:' | append: compress %}

        {% assign params = params | append: '/' %}
      {% endif %}

      {% if convert %}
        {% assign params = params | append: 'convert:' | append: convert %}

        {% assign params = params | append: '/' %}
      {% endif %}

      {% if radius %}
        {% assign params = params | append: 'radius:' | append: radius %}

        {% assign params = params | append: '/' %}
      {% endif %}

      {% if blur %}
        {% assign params = params | append: 'blur:' | append: blur %}

        {% assign params = params | append: '/' %}
      {% endif %}

      {% if rotate %}
        {% assign params = params | append: 'rotate:' | append: rotate %}

        {% assign params = params | append: '/' %}
      {% endif %}

      {% if resize %}
        {% assign params = params | append: 'resize:' | append: resize %}

        {% if resizefit %}
          {% assign params = params | append: ',fit:' | append: resizefit %}
        {% endif %}

        {% assign params = params | append: '/' %}
      {% endif %}

      {% if crop %}
        {% assign params = params | append: 'crop:' | append: crop %}
        {% if cropopts %}
          {% assign params = params | append: ',position:' | append: cropopts %}
        {% endif %}

        {% assign params = params | append: '/' %}
      {% endif %}

      {% if params != '' %}
        {{ base_url }}/{{ params }}fetch/https://{{ src_without_domain }}
      {% else %}
        {{ base_url }}/fetch/https://{{ src_without_domain }}
      {% endif %}
    {% else %}
      {{ src }}
    {% endif %}
{% endcapture -%}
{{- image_url | strip }}
```

6. Ative a funcionalidade do Voidr Images no seu Dashnoard nas configurações do seu tema

# Transformadores

### Blur

```liquid
{% assign  product_url = image | img_url: 'master' %}

{%- capture voidr_image_url %}{% render 'voidr', src: product_url, blur: '20'  -%}{%- endcapture -%}

<img
  class="header__logo-image"
  src="{{ voidr_image_url | strip }}"
/>
```

### Compress

```liquid
{% assign  product_url = image | img_url: 'master' %}

{%- capture voidr_image_url %}{% render 'voidr', src: product_url, compress: '20'  -%}{%- endcapture -%}

<img
  class="header__logo-image"
  src="{{ voidr_image_url | strip }}"
/>
```

### Convert

```liquid
{% assign  product_url = image | img_url: 'master' %}

{%- capture voidr_image_url %}{% render 'voidr', src: product_url, convert: 'webp'  -%}{%- endcapture -%}

<img
  class="header__logo-image"
  src="{{ voidr_image_url | strip }}"
/>
```

### Crop

> `cropopts` é um parâmetro opcional

```liquid
{% assign  product_url = image | img_url: 'master' %}

{%- capture voidr_image_url %}{% render 'voidr', src: product_url, crop: '20x20', cropopts: 'south'  -%}{%- endcapture -%}

<img
  class="header__logo-image"
  src="{{ voidr_image_url | strip }}"
/>
```

### Radius

```liquid
{% assign  product_url = image | img_url: 'master' %}

{%- capture voidr_image_url %}{% render 'voidr', src: product_url, radius: '50'  -%}{%- endcapture -%}

<img
  class="header__logo-image"
  src="{{ voidr_image_url | strip }}"
/>
```

### Resize

> `resizefit` é um parâmetro opcional

```liquid
{% assign  product_url = image | img_url: 'master' %}

{%- capture voidr_image_url %}{% render 'voidr', src: product_url, resize: '20x20', resizefit: 'cover'  -%}{%- endcapture -%}

<img
  class="header__logo-image"
  src="{{ voidr_image_url | strip }}"
/>
```

### Rotate

```liquid
{% assign  product_url = image | img_url: 'master' %}

{%- capture voidr_image_url %}{% render 'voidr', src: product_url, rotate: '90'  -%}{%- endcapture -%}

<img
  class="header__logo-image"
  src="{{ voidr_image_url | strip }}"
/>
```

# Exemplo de uso

Agora, para cada imagem da sua loja Shopify, personalize a imagem com o código abaixo:

```liquid
{% assign  product_url = section.settings.logo | img_url: 'master' %}

{%- capture voidr_image_url %}{% render 'voidr', src: product_url, compress: '20' -%}{%- endcapture -%}

<img
  class="header__logo-image"
  src="{{ voidr_image_url | strip }}"
  width="{{ section.settings.logo.width }}"
  height="{{ section.settings.logo.height }}"
  alt="{{ section.settings.logo.alt | default: shop.name | escape }}"
/>
```
