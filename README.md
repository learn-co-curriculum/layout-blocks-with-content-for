# Layout Blocks With Content For

## Objectives

1. Define named content blocks in a layout passing yield a symbol for the name.
2. Provide content for a named content block from the view template using content_for

## Outline

Our HTML needs to be logically grouped in order of the document. For example, our main layout must follow this order of HTML
```
<head>
  <meta tags>
</head>
<body>
  <nav>
    <a href="/">Flatiron Widget</a>
    <ul>
      <li>Products</li>
      <li>Your Cart</li>
    </ul>
  </nav>

  <div class="main">
    <%= yield # to view content %>
  </div>
</body>
```
which might generate something like:

```
<head>
  <meta tags>
</head>
<body>
  <nav>
    <a href="/">Flatiron Widget</a>
    <ul>
      <li>Products</li>
      <li>Your Cart</li>
    </ul>
  </nav>

  <div class="main">
    <h1>Product 1</h1>
    <h2>Product 1 Tag line</h2>
    <p>Product 1 description</p>
  </div>
</body>
```

This works fine as the content that is view specific, the information about product 1, is entirely contained within the main layout. It goes all inside the div.main.

But if we needed to put content related to product 1, view specific content that we only have access to on the view and not the layout in some other part of the layout? for example, facebook requires you to embed opengraph meta tags within the head of the document. what if we wanted to put opengraph tags about product 1? our layout would have to look like, conceptually

```
<head>
  <!-- Product Specific Information -->
  <meta property="og:type" content="product" />
  <meta property="og:url" content="/product/1" />
  <meta property="og:title" content="Product 1" />
  <meta property="og:description" content="Product 1 Description" />
  <meta property="product:price:amount" content="10" />
</head>
<body>
  <nav>
    <a href="/">Flatiron Widget</a>
    <ul>
      <li>Products</li>
      <li>Your Cart</li>
    </ul>
  </nav>

  <div class="main">
    <!-- Product Specific Information -->
    <h1>Product 1</h1>
    <h2>Product 1 Tag line</h2>
    <p>Product 1 description</p>
  </div>
</body>
```

As you can see now two entirely different parts of our final html need product information, some in the head, some in the main div. The layout never knows about which product we're dealing with, only the view can appropriately query @product.

We need to tell our layout that some of the content that belongs in the head will come from our view and we need to break our view into two parts, the main content and then the content for the meta tags.

first deal with the view and lets use content_for :opengraph_tags - include those meta tags, load /products/1, look at source, no meta tags. thats because just because the view is defining a named content block doesn't mean our layout automatically injects it

update the layout with <%= yield :opengraph_tags %> in the head. That works.

Show patterns like content_for?

explain that we do this often to get view-specific content in different parts of the layout, like sub navigations etc.

content_for :content_block gets paired with yield :content_block

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/layout-blocks-with-content-for' title='Layout Blocks With Content For'>Layout Blocks With Content For</a> on Learn.co and start learning to code for free.</p>
