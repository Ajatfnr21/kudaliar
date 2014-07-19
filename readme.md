### Sublime Dependents

Sublime Text 3 plugin for navigating JavaScript codebases.

Features:

* Find JavaScript modules that depend on the current JavaScript module.
* Jump to a dependency

Current scope: AMD and CommonJS applications

### Motivation

When you want to find out which files `require` the module you're looking at, it's annoying as hell to
find the filename of the current file, do a Find All, then sift through the find results to see which
file you want to jump to. **This should be automated.**

### Prerequisite

You need to have Node.js installed and the node tool [dependents](https://github.com/mrjoelkemp/node-dependents).

`npm install dependents`

### Installation

Install `Dependents` via Package Control.

Don't see it? Add the repository and install it:

1. Package Control -> Add Repository
2. Enter `https://github.com/mrjoelkemp/sublime-dependents`
3. Package Control -> Install Package
4. Choose sublime-dependents

Finally, add the key binding definition below and you're all set!

#### Key binding

You need to supply the plugin with a `root` which dictates where to look for dependents.
This value is then sent to [dependents](https://github.com/mrjoelkemp/node-dependents).

Add the following to your User defined keyboard bindings: `Preferences` -> `Key Bindings - User`

```javascript
[
  {
    "keys": ["super+alt+up"],
    "command": "dependents",
    "args": {
      "root": "public/assets/js"
    }
  },
  {
    "keys": ["super+alt+right"],
    "command": "dependents",
    "args": {
      "root": "public/assets/js",
      "mode": "dependency"
    }
  }
]
```

* You won't need the opening and closing square brackets ([]) if you have pre-existing key bindings

#### Mouse Binding

1. Create a new (or modify existing if you have one) .sublime-mousemap file:

    > **Windows** - create `Default (Windows).sublime-mousemap` in `%appdata%\Sublime Text 3\Packages\User`
    >
    > **Linux** - create `Default (Linux).sublime-mousemap` in `~/.config/sublime-text-3/Packages/User`
    >
    > **Mac** - create `Default (OSX).sublime-mousemap` in `~/Library/Application Support/Sublime Text 3/Packages/User`

2. Add the following binding

    ```js
    [
      {
        "button": "button1",
        "count": 1,
        "modifiers": ["super", "alt"],
        "press_command": "drag_select",
        "command": "dependents",
        "args": {
          "root": "public/assets/js",
          "mode": "dependency"
        }
      }
    ]
    ```

    * Note: You do not need the opening/closing square brackets `[]` if you are modifying an existing `.sublime-mousemap` file.

3. Modify the `root` according to the location of JS files in your codebase

### Usage

#### Find the dependents of the current file

Use the `keys` value above, `cmd + option + up`, to trigger finding the dependents.

* If dependents are found, you'll see them in a quick panel (i.e., dropdown).
 * You can select any of the items in the panel to jump to that file
 * If there's only one dependent, you'll be taken to that dependent file directly.
* If no dependents are found a popup will be shown

#### Jump to a dependency

1. Within a JS file, place your cursor over the dependency path you want to go to
2. Press `cmd + option + right` (or the key combination you defined) to jump to that file

Or, if you defined the mousemap in the [Mouse Binding](#mouse-binding) section:

1. hold down `CMD + Option` and click on the path of a dependency to jump to that file
