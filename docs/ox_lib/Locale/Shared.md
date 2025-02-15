Allows servers to set a preferred language and attempt to load locale files in any resources using the module.  
Locale files should use the [ISO Language Code](http://www.lingoes.net/en/translator/langcode.htm) and be saved as `./locales/langcode.json`

## Setup
To change the preferred language from English, add the convar to your server.cfg

```yaml
setr ox:locale en
```

Create a locales directory and a file for your language.

```json title="locales/en.json"
{
  "grand_theft_auto": "grand theft auto",
  "male": "male",
  "female": "female",
  "suspect_sex": "suspect is %s",
}
```

```json title="locales/fr.json"
{
  "grand_theft_auto": "vol de voiture",
  "male": "homme",
  "female": "femme",
  "suspect_sex": "le suspect est %s",
}
```

```lua title="fxmanifest.lua"
files {
  'locales/*.json'
}
```

## Usage

Initialise the locale module in your resource (once).

```lua
lib.locale()
```

Format your strings with the new locale global.  
Additional arguments can be sent to format the locale output.

```lua
locale(str, ...)
```

* str: `string`
* ...: `string` or `number`

```lua
-- Load the locale module
lib.locale()

SetInterval(function()
    print(locale('grand_theft_auto'))
    print(locale('suspect_sex', locale('male')))
end, 5000)
```

## Phrases

You can create a locale string that references other locales to construct a phrase, rather than calling locale multiple times.
```json title="locales/en.json"
{
  "hello": "hello %s",
  "my_name_is": "my name is %s",
  "hello_my_name_is": "${hello}! ${my_name_is}."
}
```
```lua
print(locale('hello_my_name_is', 'doka', 'linden'))
```
