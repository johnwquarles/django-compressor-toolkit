# django-compressor-toolkit

Set of plug-ins for [django-compressor](https://github.com/django-compressor/django-compressor/).

## Installation

```sh
pip install django-compressor-toolset
```

## Tools

### SCSS pre-compiler

Custom filter for [node-sass](https://github.com/sass/node-sass)
+ [Autoprefixer](https://github.com/postcss/autoprefixer) integration.

What does it do:

- `node-sass input.scss output.css`
- `postcss --use autoprefixer -r output.css`

It also includes all the available static sources so you could import them in your SCSS code:

```css
/* home/scss/styles.scss */
@import "base/scss/variables";

.error-message {
    background-color: $primary-red-color;
}
```

… where `home` and `base` - Django apps.

#### Use it

Add it to your settings:

```py
COMPRESS_PRECOMPILERS = (
    ('text/x-scss', 'compressor_toolkit.precompilers.ScssFilter'),
)
```

And include SCSS in your template:

```html
{% compress css %}
<link type="text/x-scss" href="{% static 'home/scss/styles.scss' %}">
{% endcompress %}
```

To make it work, you need `node-sass` and `postcss` w/ `autoprefixer` to be installed.

Quick install:

```sh
npm install -g node-sass postcss-cli autoprefixer
```

Full instructions:
- [node-sass](https://github.com/sass/node-sass) docs
- [Autoprefixer](https://github.com/postcss/autoprefixer) docs
