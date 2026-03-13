# Mutate
Inline text replacement and generation utility for Mac (menu bar, via shortcut)



## Requirements
macOS 14+, universal .app in .dmg archive, notarized

requires: 
- accessibility permissions (to access selected text and to replace it, also accesses clipboard to bypass limitations of certain tools)
- outgoing network connection to support Monaco editor

## Features
- native
- works in any window
- completely offline
- seamless text replacement or generation without interrupting your worklfow and without switching to a differnt window
- ability to define your own transformation and generation tools with Javascript (the app comes with a few default tools)
- register as startup item to be always available
- define your own shortcut
- import/export tools to yaml

## Use cases
- Expanding abbreviations
- Conversions
- Encoding / decoding
- Sorting
- Templates
- Lorem ipsum generation
- and more

## Installation

1. Download dmg archive (from releases on the right side of this page)
2. Mount the dmg and move .app file to /Applications
3. Run the app
4. The tool comes with a few pre-installed transformations and generators. You can import more from the [transformations](https://github.com/robert-v/Mutate-public/tree/main/transformations) folder and [generators](https://github.com/robert-v/Mutate-public/tree/main/generators) folder or create your own. Contributions are welcome!

Update to a new version: simply grab the newest dmg from Releases and replace your existing .app file in /Applications folder. Your existing Transformations will be preserved.

## Usage
1. trigger Mutate with the defined shortcut (default is ```Cmd + Shift + u```)
2. popup will show Transformations or Generators depending on whether any text is selected or not
3. you can toggle between Tranformations and Generators with ```Ctrl + Tab```
4. choose a tool from the list
5. press enter
6. selected text will be replaced with the output or text will be injected at the cursor position

## Custom transformations

Custom transformation must contain function with the name ```transform``` and parameter ```text```. The function is expected to return a transformed string.

Format JSON:

```
function transform(text) {
    try {
        // 1. Sanitize the string first
        var sanitizedText = text
            .replace(/[“”]/g, '"')  // Fix macOS curly double quotes
            .replace(/[‘’]/g, "'")  // Fix macOS curly single quotes
            .replace(/'/g, '"');    // Attempt to convert JS single quotes to JSON double quotes
            
        // 2. Parse and format
        var parsed = JSON.parse(sanitizedText);
        return JSON.stringify(parsed, null, 2);
    } catch(e) {
        return "Error formatting JSON: " + e.message;
    }
}
```

See more examples under [transformations](https://github.com/robert-v/Mutate-public/tree/main/transformations) folder.

## Custom generators

Custom generators must contain function with the name ```generate``` and no parameters. The function is expected tu return generated string.

```
function generate() {
    return "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.";
}
```

See more examples under [generators](https://github.com/robert-v/Mutate-public/tree/main/generators) folder.

## Limitations
- Tools selector location - the tool tries to read selected text rectangle and change it's location accordingly, but some apps don't report this. In such case the tool falls back to mouse poiner location.
- Shortcut is intended to work only when text is selected. Some tools however report whole line selection even if nothing is selected.
- Terminals - the transformed text will not overwrite selected text but will appear at the cusor position,
- Rich text - the tool currently doesn't preserve rich text formatting and will output plain text if rich text is provided as an input.

## Explore My macOS Apps
  
[ProcessSpy - Advanced process monitor for Mac](https://process-spy.app)

[Restretto - Minimal REST client for Mac](https://restretto.app)

[Essence - Minimal and focused log viewer for Mac](https://github.com/robert-v/Essence-public)

