# Exclude files from `format on save` in vscode

### For specific file:
VS Code has a shortcut for saving a file without formatting listed under the command `workbench.action.files.saveWithoutFormatting` - Default keybinding should be

`CTRL + K CTRL + SHIFT + S` 
(simply keep CTRL pressed and then type K + SHIFT + S).

On OS X the default keybinding is

`CMD + k` then press `s`

### For entire workspace

You can use [language specific settings](https://code.visualstudio.com/docs/getstarted/settings#_language-specific-editor-settings) to _enable_ it for a specific language only, e.g. JavaScript:

<!-- language: lang-json -->

    "[javascript]": {
        "editor.formatOnSave": true
    }

To _disable_ it for a specific language, you could switch the global default to `true` and combine it with a language-specific `false`:

<!-- language: lang-json -->

    "editor.formatOnSave": true
    "[javascript]": {
        "editor.formatOnSave": false
    }

Note that language specific settings are based on [language identifiers](https://code.visualstudio.com/docs/languages/identifiers) rather than directly on file extensions. There's an open feature request to allow for [file extension specific settings](https://github.com/Microsoft/vscode/issues/35350) as well.

In cases where the language ID isn't specific enough, `"files.associations"` could be used to remap files with a specific extension and/or in a specific directory to another ID, but this will affect syntax highlighting, code completion, etc. as well. For instance, this would work to disable formatting for JavaScript files in `out` directories, but they will be treated as plaintext:

```lang-json
"[javascript]": {
	"editor.formatOnSave": true
},
"files.associations": {
	"**/out/**/*.js": "plaintext"
}
```
