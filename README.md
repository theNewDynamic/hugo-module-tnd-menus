This is a template repo. To start.

search `TND Nav` through the project and replace it with the module identifier (ex: `socials` for `hugo-module-tnd-socials`)

# Nav Hugo Module

(intro)

## Requirements

Requirements:
- Go 1.14
- Hugo 0.64.0


## Installation

If not already, [init](https://gohugo.io/hugo-modules/use-modules/#initialize-a-new-module) your project as Hugo Module:

```
$: hugo mod init {repo_url}
```

Configure your project's module to import this module:

```yaml
# config.yaml
module:
  imports:
  - path: github.com/theNewDynamic/hugo-module-tnd-menus
```

## Setting Menus

The menus are set following Hugo's own ways.
- Through [the content file's Front Matter](https://gohugo.io/content-management/menus/#add-content-to-menus).
- Through [the project's configuration](https://gohugo.io/content-management/menus/#add-non-content-entries-to-a-menu)

On top of that, if you're using Hugo 0.79.0 and above, it's possible to set a Page to a Menu Entry with the project's configuration method. Simple add a `page` params whose value would find a page in your content directory following the `site.GetPage` API.

Ex: 

```
# config/_default/menus.yaml
main:
- name: About
  params:
    page: /about
- name: History
  params:
    page: /posts/a-brief-history
```

## Usage

### tnd-menus/GetMenu

Anywhere in your templates you can invoke the `tnd-menus/GetMenu` partial. Its context expect either:
- A Map with:
  - `menu`* holds a string pointing to the menu key as used in your project. (Ex: "main").
  - `Page`, a Hugo Page which will set as the current page when using IsActive. If not set, we'll use the Homepage.
- A String pointing holding the pointing to the menu key as used in your project. (Ex: "main"). The Homepage will be used as `Page`.

#### Examples
```
{{ $args := dict "menu" "main" "Page" $ }}
{{ range partial "tnd-menus/GetMenu" $args }}
  <a href="{{ .URL }}" class="MenuItem {{ if .Active }} MenuItem--active {{ end }}"
  {{ if .External }} target="_blank"{{ end }}>
  {{ .Name }}
  </a>
  {{ with .Children }}
  {{/* ... */}}
  {{ end }}
{{ end }}
```

### The Module's Menu Entry object

Any given entry returned by the `tnd-menus/GetMenu` partial will hold the following keys:
Warning: Case matters.

- __Name__: Menu Entry name of the Menu Entry
- __URL__: Menu Entry URL
- __External__ (Bool): Is the MenuEntry URL external.
- __Active__ (Bool): BIs the MenuEntry considered active given the module's default or users's IsActive partial
- __Page__ (Page): The page associated with the MenuEntry if set.
- __Level__ (Int): The hierarchy Level of the Menu Entry in the given menu. Starts at 1.
- __Children__ (Slice of maps): A list of Menu Entries following hereby data structure.
- __...__ Any other lowercase key will be a key found in the Menu Entry's `params` map.


### Settings

Settings are added to the project's parameter under the `tnd_nav` map as shown below.

```yaml
# config.yaml
params:
  tnd_nav:
    [...]
```

#### Configure Key 1

#### Configure Key 2

#### Defaults

ld copy/paste the above to your settings and append with new extensions.

## theNewDynamic

This project is maintained and loved by [thenewDynamic](https://www.thenewdynamic.com).
