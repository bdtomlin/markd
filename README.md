# markd

[![Language](https://img.shields.io/badge/language-crystal-776791.svg)](https://github.com/crystal-lang/crystal)
[![Tag](https://img.shields.io/github/tag/icyleaf/markd.svg)](https://github.com/icyleaf/markd/blob/master/CHANGELOG.md)
[![Build Status](https://img.shields.io/circleci/project/github/icyleaf/markd/master.svg?style=flat)](https://circleci.com/gh/icyleaf/markd)
G
Yet another markdown parser built for speed, written in [Crystal](https://crystal-lang.org), Compliant to [CommonMark](http://spec.commonmark.org) specification (`v0.27`). Copy from [commonmark.js](https://github.com/jgm/commonmark.js).

## Installation

Add this to your application's `shard.yml`:

```yaml
dependencies:
  markd:
    github: icyleaf/markd
```

## Quick start

```crystal
require "markd"

markdown = <<-MD
# Hello Markd

> Yet another markdown parser built for speed, written in Crystal, Compliant to CommonMark specification.
MD

html = Markd.to_html(markdown)
```

Also here is an options to configure the parse and render.

```crystal
options = Markd::Options.new(smart: true, safe: true)
Markd.to_html(markdown, options)
```

## Options

Name | Type | Default value | Description |
---|---|---|---
time | `Bool` | false | render parse cost time during read source, parse blocks, parse inline.
smart | `Bool` | false |if **true**, straight quotes will be made curly,<br />`--` will be changed to an en dash,<br />`---` will be changed to an em dash, and<br />`...` will be changed to ellipses.
source_pos | `Bool` | false | if **true**, source position information for block-level elements<br />will be rendered in the data-sourcepos attribute (for HTML)
safe | `Bool` | false | if **true**, raw HTML will not be passed through to HTML output (it will be replaced by comments)
gfm | `Bool` | false | **Not support for now**
toc | `Bool` | false | **Not support for now**

## Advanced

If you want use custom renderer, it can!

```crystal

class CustomRenderer < Markd::Renderer

  def strong(node, entering)
  end

  # more methods following in render.
end

options = Markd::Options.new(time: true)
document = Markd::Parser.parse(markdown, options)
renderer = CustomRenderer.new(options)

html = renderer.render(document)
```

## Performance

First of all, Markd is slower than [Crystal Built-in Markdown](https://crystal-lang.org/api/0.23.0/Markdown.html) which it is a lite version, only apply for generte Cystal documents ([#4496](https://github.com/crystal-lang/crystal/pull/4496), [#4613](https://github.com/crystal-lang/crystal/issues/4613)).

Here is the result of [a sample markdown file](benchmarks/source.md) parse at MacBook Pro Retina 2015 (2.2 GHz):

```
Crystal Markdown   3.28k (305.29µs) (± 0.92%)       fastest
           Markd 305.36  (  3.27ms) (± 5.52%) 10.73× slower
```

Recently, i'm working to compare the other popular commonmark parser, the code is stored in [benchmarks](/benchmarks).

## Donate

Markd is a open source, collaboratively funded project. If you run a business and are using Markd in a revenue-generating product,
it would make business sense to sponsor Markd development. Individual users are also welcome to make a one time donation
if Totem has helped you in your work or personal projects.

You can donate via [Paypal](https://www.paypal.me/icyleaf/5).

## How to Contribute

Your contributions are always welcome! Please submit a pull request or create an issue to add a new question, bug or feature to the list.

All [Contributors](https://github.com/icyleaf/markd/graphs/contributors) are on the wall.

## You may also like

- [halite](https://github.com/icyleaf/halite) - HTTP Requests Client with a chainable REST API, built-in sessions and middlewares.
- [totem](https://github.com/icyleaf/totem) - Load and parse a configuration file or string in JSON, YAML, dotenv formats.
- [poncho](https://github.com/icyleaf/poncho) - A .env parser/loader improved for performance.
- [popcorn](https://github.com/icyleaf/popcorn) - Easy and Safe casting from one type to another.
- [fast-crystal](https://github.com/icyleaf/fast-crystal) - 💨 Writing Fast Crystal 😍 -- Collect Common Crystal idioms.

## License

[MIT License](https://github.com/icyleaf/markd/blob/master/LICENSE) © icyleaf
