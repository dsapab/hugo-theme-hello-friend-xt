# Hello Friend XT

This is my extended version (XT), forked and inspired by the [hello-friend-ng](https://github.com/rhazdon/hugo-theme-hello-friend-ng) theme. Big kudos for the amazing work and contributions! I will keep my own fork as I may add new features and capabilities in the future, but I will try to keep this project in sync with the up-stream as much as possible.


## Table of Contents

- [Features](#features)
- [How to start](#how-to-start)
- [A few extra details](#a-few-extra-details)
  - [Built in shortcodes](#built-in-shortcodes)
    - [image](#image)
  - [Code highlighting](#code-highlighting)
  - [Favicon](#favicon)
  - [Audio Support](#audio-support)
  - [Social Icons](#social-icons)
- [Known issues](#known-issues)
- [How to edit the theme](#how-to-edit-the-theme)
- [Changelog](CHANGELOG.md)
- [Licence](#licence)

---

## Features

- Theming: **dark/light mode**, depending on your system preferences or the users choice
- Great reading experience thanks to [**Inter font**](https://rsms.me/inter/), made by [Rasmus Andersson](https://rsms.me/about/)
- Nice code highlighting thanks to [**PrismJS**](https://prismjs.com)
- An easy way to modify the theme with Hugo tooling
- Fully responsive
- Support for audio in posts (thanks to [@talbotp](https://github.com/talbotp))
- Builtin (enable/disable) multi-language menu
- Support for social icons
- Support for sharing buttons
- Support for [Commento](https://commento.io)
- Support for [Plausible](https://plausible.io) (thanks to [@Joffcom](https://github.com/Joffcom))
- Support for [utterances](https://utteranc.es/) comment system

## How to start

⚠️ **The theme needs at least Hugo **Extended** v0.90.x**.

Therea are basically three main ways of installing and using themes in Hugo, being the [hugo modules](https://gohugo.io/hugo-modules/use-modules/) the most recommended approach. You can also choose **one of the 3 possibilities** to install the theme:

1. as Hugo Module (**recommended**)
2. as a standalone local directory
3. as a git submodule

### Install theme as Hugo Module

This is the most recommended way as uses Go engine for handling dependencies, which is very well integrated with GitHub. It is the most efficient and clean method for including a remote theme. If you don't intend to apply radical changes to the theme, use this approach.

```bash
# If this is the first time you're using Hugo Modules
# in your project. You have to initiate your own module before
# you fetch the theme module.
# '[your-website-git-url]' is just a placeholder for your module name.
#
hugo mod init [your-website-git-url]
```

Then you need to install the module:
```bash
hugo mod get github.com/pablods90/hugo-theme-hello-friend-xt
```

and in finally in your config file add:

```toml
[module]
  # this is needed when you fetch the theme as a submodule to your repo.
  # replacements = "github.com/pablods90/hugo-theme-hello-friend -> themes/hello-friend"
[[module.imports]]
  path = 'github.com/pablods90/hugo-theme-hello-friend'
```

If at any stage you update the theme repository, you will need to update local modules to pull the changes. You can do this as follows:

```bash
hugo mod get -u
```

Keep in mind that the theme by default won't show up in the `themes` directory. This means that you are using the theme as it was on the repository at the moment you fetched it. Your local `go.sum` file keeps all the references, so you can commit it to your repository. Read more about Hugo Modules in the [official documentation](https://gohugo.io/hugo-modules/).

⚠️ If you encounter any issues with:

```bash
Error: module "hello-friend" not found; either add it as a Hugo Module or store it in "[...your custom path]/themes".: module does not exist
```
then please try to remove `theme = "hello-friend"` from your config file.

### Install theme locally

```bash
git clone https://github.com/pablods90/hugo-theme-hello-friend-xt.git themes/hello-friend
```

This will clone the repository directly to the `themes/hello-friend` directory. This is good for local development as well as integrating the theme itself as part of your website.


### Install theme as a submodule

```bash
git submodule add -f https://github.com/pablods90/hugo-theme-hello-friend-xt.git themes/hello-friend
```

This will install the repository as a sub-module in the `themes/hello-friend` directory. I do not encourage this approach, as dealing with git sub-modules is not optimal and requires extra steps and two nested repositories. If you intend to keep the theme decoupled, my advice would be to use Hugo Modules (step 1).


## How to configure

The theme doesn't require any advanced configuration. Just copy the following config file.
To see all possible configurations, [check the docs](docs/config.md).
Note: There are more options to configure. Take a look into the `config.toml` in `exampleSite`.

``` toml
baseurl      = "localhost"
title        = "My Blog"
languageCode = "en-us"
theme        = "hello-friend-ng"
paginate     = 10

[params]
  dateform        = "Jan 2, 2006"
  dateformShort   = "Jan 2"
  dateformNum     = "2006-01-02"
  dateformNumTime = "2006-01-02 15:04"

  # Subtitle for home
  homeSubtitle = "A simple and beautiful blog"

  # Set disableReadOtherPosts to true in order to hide the links to other posts.
  disableReadOtherPosts = false

  # Enable sharing buttons, if you like
  enableSharingButtons = true
  
  # Show a global language switcher in the navigation bar
  enableGlobalLanguageMenu = true

  # Metadata mostly used in document's head
  description = "My new homepage or blog"
  keywords = "homepage, blog"
  images = [""]

[taxonomies]
    category = "blog"
    tag      = "tags"
    series   = "series"

[languages]
  [languages.en]
    title = "Hello Friend NG"
    keywords = ""
    copyright = '<a href="https://creativecommons.org/licenses/by-nc/4.0/" target="_blank" rel="noopener">CC BY-NC 4.0</a>'
    readOtherPosts = "Read other posts"

  [languages.en.params]
    subtitle  = "A simple theme for Hugo"

    [languages.en.params.logo]
      logoText = "hello friend ng"
      logoHomeLink = "/"
    # or
    #
    # path = "/img/your-example-logo.svg"
    # alt = "Your example logo alt text"

  # And you can even create generic menu
  [[menu.main]]
    identifier = "blog"
    name       = "Blog"
    url        = "/posts"
```

## A few extra details

### Built-in shortcodes

Of course you are able to use all default shortcodes from hugo (https://gohugo.io/content-management/shortcodes/).

#### image

Properties:

  - `src` (required)
  - `alt` (optional)
  - `position` (optional, default: `left`, options: [`left`, `center`, `right`])
  - `style`

Example:

``` golang
{{< image src="/img/hello.png" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}
```

### Code highlighting

By default the theme is using PrismJS to color your code syntax. All you need to do is to wrap you code like this:

<pre>
``` html
  // your code here
```
</pre>

### Favicon

Check the [docs](docs/favicons.md).

### Audio Support

You wrote an article and recorded it? Or do you have a special music that you would like to put on a certain article? Then you can do this now without further ado.

In your article add to your front matters part:

```yaml
audio: path/to/file.mp3
```

### Social Icons

A large variety of social icons are available and can be configured like this:

```toml
[[params.social]]
  name = "<site>"
  url = "<profile_URL>"
```

Take a look into this [list](docs/svgs.md) of available icon options. 

If you need another one, just open an issue or create a pull request with your wished icon. :)


## Known issues

Nothing here at the moment! 🚀


## How to edit the theme

Just edit it. You don't need any node stuff! Single branches can be created for serving different websites, in case you need to re-use this theme with small changes. Nevertheless, I encourage you to use the local directories in your site for overriding the theme default layouts.


## Licence

The theme is released under the [MIT License](./LICENSE.md). Check the [original theme license](https://github.com/rhazdon/hugo-theme-hello-friend-ng/blob/master/LICENSE.md) for additional licensing information.
