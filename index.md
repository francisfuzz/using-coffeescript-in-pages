## Using CoffeeScript in GitHub Pages 

### Setup

First, follow these instructions:
* [Create a new GitHub Pages site](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)
* [Add a theme to your GitHub Pages site with theme chooser](https://docs.github.com/en/pages/getting-started-with-github-pages/adding-a-theme-to-your-github-pages-site-with-the-theme-chooser)
* [Configure the publishing source for your site](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site) to `gh-pages`

Next, follow the instructions for [customizing your theme's HTML layout](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll#customizing-your-themes-html-layout). Be sure to use the theme you added with theme chooser; you'll create a new `_layouts/default.html` file using the same contents as the theme.

### Configuration

Follow [these instructions for testing the Pages site locally](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll). The repo include some "convenience" scripts for bootstrapping and serving up the site.

Ensure that your Gemfile is created:

```ruby
# https://bundler.io/gemfile.html

source 'https://rubygems.org'

gem 'github-pages', group: :jekyll_plugins
```

As well as your `_config.yml` being updated to use CoffeeScript:

```yaml
# I chose this theme, but yours could be completely different 😉
theme: jekyll-theme-minimal

plugins:
  - jekyll-coffeescript
```

### The CoffeeScript

Create a new file, `assets/js/index.coffee`:

```coffee
---
---

# Source: https://coffeescript.org/#introduction
# Assignment:
number   = 42
opposite = true

# Conditions:
number = -42 if opposite

# Functions:
square = (x) -> x * x

# Arrays:
list = [1, 2, 3, 4, 5]

# Objects:
math =
  root:   Math.sqrt
  square: square
  cube:   (x) -> x * square x

# Splats:
race = (winner, runners...) ->
  print winner, runners

originallyCompiledFromCoffeeScript = true 

# Existence:
console.log "This alert was originally compiled from CoffeeScript!" if originallyCompiledFromCoffeeScript?

# Array comprehensions:
cubes = (math.cube num for num in list)
```

Some important observations:

* Internally, Jekyll compiles your site and outputs the files to the `_site` directory. `_site` includes an `assets/js/` directory by default, so we can take advantage of the pipeline and include our own CoffeeScript files within `./assets/js`.
* The two `---` markers at the top of the CoffeeScript file are important for Jekyll to recognize these are assets to be compiled. Read more in [Jekyll's Docs: Content > Assets](https://jekyllrb.com/docs/assets/).

Last, incorporate the file in the `_layouts/default.html` created earlier:

```html
    <script src="{{ "/assets/js/index.js" | relative_url }}"></script>
```

Run the site -- locally or on GitHub Pages itself -- and open your browser's JavaScript Console. You should see the following message logged:

```javascript
"This alert was originally compiled from CoffeeScript!"
```

💃
