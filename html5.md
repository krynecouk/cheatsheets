## Section elements
### `<body>`
> The body element represents the contents of the document. Only one in document.

### `<article>`
> Represents independent item of content (forum post, magazine or newspaper article, a blog entry, a user-submitted comment etc.).

```html
<article itemscope itemtype="http://schema.org/BlogPosting">
 <header>
  <h1 itemprop="headline">The Very First Rule of Life</h1>
  <p><time itemprop="datePublished" datetime="2009-10-09">3 days ago</time></p>
  <link itemprop="url" href="?comments=0">
 </header>
 <p>If there's a microphone anywhere near you, assume it's hot and
 sending whatever you're saying to the world. Seriously.</p>
 <p>...</p>
 <footer>
  <a itemprop="discussionUrl" href="?comments=1">Show comments...</a>
 </footer>
</article>
```

### `<section>`
> `<div>` with special semantic meaning. Use if block is needed (feels like) that belongs to a table of contents.

> `<article>` element instead of the `<section>` element when it would make sense to syndicate the sections of the article.

```html
<article>
 <hgroup>
  <h1>Apples</h1>
  <h2>Tasty, delicious fruit!</h2>
 </hgroup>
 <p>The apple is the pomaceous fruit of the apple tree.</p>
 <section>
  <h1>Red Delicious</h1>
  <p>These bright red apples are the most common found in many
  supermarkets.</p>
 </section>
 <section>
  <h1>Granny Smith</h1>
  <p>These juicy, green apples make a great filling for
  apple pies.</p>
 </section>
</article>
```

### `<header>` & `<footer>`
> Designed to be used within any part of your document that represents a chunk of content with a clear beginning and end. This can include things like forms, articles, sections of articles, posts on a social media site, cards, etc.

### `<main>`
> The main content area of a document includes content that is unique to that document and excludes content that is repeated across a set of documents (logo, banner, search forms etc.).

> There must not be more than one visible main element in a document. If more than one main element is present in a document, all other instances must have `hidden` attribute.

```html
<header>
  <h1>Super duper best blog ever</h1>
  ...
</header>
<main>
  <h2>Why you should buy more cheeses than you currently do</h2>
  ...
</main>
<footer>
  Contact us!
  <div class="contact-info">this.is.us@example.com</div>
</footer>
```

### `<nav>`
> Designed to clearly identify the main navigation blocks on the page.

```html
<nav>
    <a href="/">Home</a>
    <a href="/about">About</a>
    <a href="/archive">Archive</a>
</nav>
```

### `<aside>`
> Represents a section of a page that consists of content that is tangentially related to the content around the aside element, and which could be considered separate from that content.

```html
<p>He later joined a large company, continuing on the same work.</p>
<aside>
 <q> People ask me what I do for fun when I'm not at work. But I'm
 paid to do my hobby, so I never know what to answer. </q>
</aside>
...
```

### `<figure>`
> Single unit separated from main flow with `figcaption`.

### `<hgroup>`
> Group of headings.

```html
<hgroup>
 <h1>The reality dysfunction</h1>
 <h2>Space is not the only void</h2>
</hgroup>
```

### `<adress>`
> The address element represents the contact information for its nearest article or body element ancestor. If that is the body element, then the contact information applies to the document as a whole.

```html
<address>
 <a href="../People/Raggett/">Dave Raggett</a>,
 <a href="../People/Arnaud/">Arnaud Le Hors</a>,
 contact persons for the <a href="Activity">W3C HTML Activity</a>
</address>
```

## Grouping elements
### `<p>`
> Paragraph.

### `<hr>`
> Paragraph level break.

### `<pre>`
> Block of preformatted text.

### `<blockquote>`
> Section that is quoted from another source.

### `<ol>`
> Ordered list.

### `<ul>`
> Unordered list.

### `<li>`
> List item.

### `<dl>`
> Description list.

### `<dt>`
> Description term. 

### `<dd>`
> Descriptin definition.

```html
<dl>
 <dt><dfn>happiness</dfn></dt>
 <dd class="pronunciation">/'hæ p. nes/</dd>
 <dd class="part-of-speech"><i><abbr>n.</abbr></i></dd>
 <dd>The state of being happy.</dd>
 <dd>Good fortune; success. <q>Oh <b>happiness</b>! It worked!</q></dd>
 <dt><dfn>rejoice</dfn></dt>
 <dd class="pronunciation">/ri jois'/</dd>
 <dd><i class="part-of-speech"><abbr>v.intr.</abbr></i> To be delighted oneself.</dd>
 <dd><i class="part-of-speech"><abbr>v.tr.</abbr></i> To cause one to be delighted.</dd>
</dl>
```

## Text level semantics
### `<em>`
> Emphasis.

### `<strong>`
> Bold.

### `<small>`

### `<s>`
> Strikethrough.

### `<cite>`
>  Title of a work (e.g. a book, a paper, an essay, a poem, a score, a song, a script...)

### `<q>`
> Quote from another source. 

`<q cite="https://www.w3.org/Consortium/">To lead the World Wide..</q>`

### `<dfn>`
> Defining instance of a term

### `<abbr>`
> Abbreviation/acronym. 

`<abbr title="World Health Organization">WHO</abbr>`

### `<data>`
> Machine-readable form of data. `value` is mandatory attribute. 

`<data value="8">Eight</data>`

### `<time>`
> Machine-readable form of time. `datetime` is optional.

`<time class="dtstart" datetime="2005-10-05">October 5</time>`

### `<code>`
> Programming code formatting.
```html
<pre><code class="language-pascal">var i: Integer;
begin
   i := 1;
end.</code></pre>
```

### `<samp>`
> Output from different computing system.

### `<var>`
> Variable.

### `<b>`
> Bold. But not so bold like `<strong>`. 

### `<mark>`
> Mark like with marker.

### `<del>`
> Like `<s>` but for lists.

## Sources
[1]:[whatwg](https://html.spec.whatwg.org/multipage/sections.html)
[2]:[Stop-div](https://dev.to/kenbellows/stop-using-so-many-divs-an-intro-to-semantic-html-3i9i)

