---
title: "Bootstrap Notes"
date: 2020-06-08
categories: Bootstrap
permalink: /:categories/:title
---

## Concepts

- Linking to a HTML

```HTML
// adding Bootstrap CDN to <head> inside a <link> tag
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css" integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" crossorigin="anonymous">
```

- containers
  - rows
    - columns

```HTML
<div class="container">
  <div class="row">
    <div class="col">
      <!-- A column inside a row inside a container! -->
    </div>
  </div>
</div>
```

- .container-fluid

  - ```HTML
    <div class="container-fluid"></div>
    ```

- .col

  - <div class="col"></div>
  - <div class="col-9"></div>
  - <div class="col-auto"></div>

- breaking points

```HTML
<div class="col-sm-8">
</div>
```

```HTML
<div class="col-12 col-sm-10 col-md-8 col-lg-6 col-xl-3">
</div>
```

- bootstrap starter template
  [Bootstrap starter template](https://getbootstrap.com/docs/4.2/getting-started/introduction/#starter-template)

- color

```HTML
<p class="text-primary">.text-primary</p>
<p class="text-secondary">.text-secondary</p>
<p class="text-success">.text-success</p>
<p class="text-danger">.text-danger</p>
<p class="text-warning">.text-warning</p>
<p class="text-info">.text-info</p>
<p class="text-light bg-dark">.text-light</p>
<p class="text-dark">.text-dark</p>
<p class="text-body">.text-body</p>
<p class="text-muted">.text-muted</p>
<p class="text-white bg-dark">.text-white</p>
<p class="text-black-50">.text-black-50</p>
<p class="text-white-50 bg-dark">.text-white-50</p>
```

- text

```HTML
  <p class="text-uppercase font-italic text-right">
    First, assign a class to style this text so that it is entirely uppercased.
    After you've assigned the appropriate class to make this text uppercased, assign another class to make this text italicized.
    Finally, browse Bootstrap's documentation to right align this text.
  </p>
```

- card
- Carousel Component
- collapse

```HTML
<button class="btn btn-primary" type="button" data-toggle="collapse" data-target="#collapsePara" aria-expanded="false" aria-controls="collapsePara">
  This button toggles the visibility of the <p>.
</button>
<p class="collapse" id="collapsePara">
	This text should not be visible at first.
</p>
```
