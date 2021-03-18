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
  - path: github.com/theNewDynamic/hugo-module-tnd-nav
```

## Usage

### tnd-nav/GetMenu

Context is a Map:
  - String (.menu)
  - MenuEntry (.MenuEntry)
  - Page (.Page)

#### Examples
```
  {{ range partial "tnd-menus/GetMenu" $args }}
    <a href="{{ .URL }}" class="MenuItem {{ if .Active }} MenuItem--active {{ end }}"
    {{ if .External }} target="_blank"{{ end }}>
    {{ .Name }}
    </a>
  {{ end }}
```
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
