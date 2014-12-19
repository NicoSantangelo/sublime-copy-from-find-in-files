Sublime Copy from find in files
===============================

[![Build Status](https://travis-ci.org/NicoSantangelo/sublime-copy-from-find-in-files.svg?branch=master)](https://travis-ci.org/NicoSantangelo/sublime-copy-from-find-in-files)

Little package to remove the line number when copying from the find in files panel

## Use

The command is designed to only work on the `Find Results` tab and default to a normal copy otherwise.

It will transform this:

````
6  class CopyFromFindInFilesCommand(sublime_plugin.TextCommand):
7:     def run(self, edit):
8          self.view.run_command('copy')
````

to this:

````
class CopyFromFindInFilesCommand(sublime_plugin.TextCommand):
    def run(self, edit):
        self.view.run_command('copy')

````

## KeyBindings

There is no default shortcut, to add it open your User Keybindings file and add something like the following:

````javascript
// Linux or Windows
{ "keys": ["ctrl+c"], "command": "copy_from_find_in_files", 
    "context": [{ "key": "selector", "operator": "equal", "operand": "text.find-in-files" }]
}

// MacOS
{ "keys": ["super+c"], "command": "copy_from_find_in_files", 
    "context": [{ "key": "selector", "operator": "equal", "operand": "text.find-in-files" }]
}
````

using `"context": [{ "key": "selector", "operator": "equal", "operand": "text.find-in-files" }]` it's being extra careful, you can leave that out and the package will check for `Find Results` for you.

### Outside Find in Files

If you want to use the package outside `Find Results` you can add a the `force` argument, like this:

````javascript
// Linux or Windows
{ "keys": ["ctrl+alt+c"], "command": "copy_from_find_in_files",
    "args": { "force": true }
}

// MacOS
{ "keys": ["super+alt+c"], "command": "copy_from_find_in_files", 
    "args": { "force": true }
}
````

## Settings

````javascript
{
    // If set to false, it removes the dots added by sublime to mark the separation between matches in the same file.
    "keep_intermediate_dots": true
}
````