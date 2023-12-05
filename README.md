# [![Voidr](https://img.voidr.co/voidr/compress:100/convert:webp/fetch/https://api.voidr.co/v1/images/raw/voidr/voidr-banner-en_1701195001454.png)](https://en.voidr.co/images)

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Discord](https://img.shields.io/badge/Discord-7289DA?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/Wk6dfhJu)
[![Telegram](https://img.shields.io/badge/Telegram-2CA5E0?style=flat-squeare&logo=telegram&logoColor=white)](https://t.me/comunidadevoidr/1)
[![Twitter Follow](https://img.shields.io/twitter/follow/Voidr_co?style=social)](https://twitter.com/Voidr_co)

# Voidr

Voidr is a robust and scalable platform for image optimization and resizing, specifically designed for developers. With our intuitive and flexible API, you can improve the loading performance of your applications in minutes by delivering optimized images in cutting-edge formats.

[![Voidr Code Example](https://img.voidr.co/voidr/compress:100/convert:webp/fetch/https://api.voidr.co/v1/images/raw/voidr/code-example-clean.png)](https://voidr-images-en.readme.io/reference/intro)

# 🚀 Getting started

### Configure Theme Settings

1. Log in to your Shopify account.
2. Navigate to Online Store > Themes > Click on the three dots > Edit code.
3. Go to the config section and edit the settings_schema.json file.

In the `settings_schema.json` file, you'll find an array of configurations.

4. At the end of this file, right after the last `}` character, add a comma, like this `},` and include the following code:

```json
{
  "name": "Voidr Images",
  "settings": [
    {
      "type": "paragraph",
      "content": "For more information see the [docs](https://voidr-images.readme.io/reference/intro)"
    },
    {
      "type": "checkbox",
      "id": "voidr_enable",
      "label": "Enable Voidr Images",
      "info": "Toggle the Voidr Images feature"
    },
    {
      "type": "text",
      "id": "voidr_project",
      "label": "Voidr Project Name",
      "default": "my-project-name",
      "info": "Project name that you created on your Voidr Dashboard"
    }
  ]
}
```

5. After that, in the `snippets` section, create a file called `voidr.liquid` and add the following code:

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

6. Go to your theme settings on personalization and activate the Voidr Images helper.

# Transformers

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

> `cropopts` is a optional param

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

> `resizefit` is a optional param

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

# Usage example

Now, for each image on your store, add the following code to your theme files:

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
