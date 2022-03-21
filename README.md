# History Extension

Adds History API support to nette.ajax.js addon for Nette Framework!

This repo is a fork of [vojtech-dobes/history.nette.ajax.js](https://github.com/vojtech-dobes/history.nette.ajax.js) package with additional support for Nette 3.

All credits go to Vojtěch. Thank you!

## Installation

1. Link `client-side/history.ajax.js` after `nette.ajax.js`.
2. Load PHP files with Composer: `blueweb/nette-ajax-history`
3. Register config extension in your configuration:

```
extensions:
	ajaxHistory: Blueweb\NetteAjax\HistoryExtension
```

## Usage

Write your application as normal. All redirects and forwards will be properly handled.

To correctly update UI, use snippets. If you plan to ajaxify whole application, consider adding this snippet to your `beforeRender()` method in `BasePresenter`.

```php
if ($this->isAjax()) {
	$this->invalidateControl('title');
	$this->invalidateControl('content');
}
```

And `app/@layout.latte` might be upgraded accordingly:

```html
<title n:inner-snippet="title">...</title>
```

```html
{snippet content}
	{include content}
{/snippet}
```

### Disabling

If you want specific links or forms exclude from scope of this addon (not make them update the URL), you can use `data-ajax-off` feature of *nette.ajax.js*.

```html
<a class="ajax" data-ajax-off="history">
```

## UI Caching

Extension will automatically cache your UI and restore it on *Back* and *Forward* buttons without communication with server. If you wish to call server on every *Back* and *Forward*, turn caching off.

```js
$.nette.ext('history').cache = false;
```
