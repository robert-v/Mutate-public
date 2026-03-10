# Mutate
Inline text transformations for Mac (menu bar, via shortcut)

<img width="655" height="415" alt="image" src="https://github.com/user-attachments/assets/185a7d9a-7c2d-448f-b0e8-f987c45adb12" />


###

<img width="213" height="64" alt="image" src="https://github.com/user-attachments/assets/01cf54b7-6065-443c-b9f9-d529aaab24c3" />


macOS 14+, universal .app in .dmg archive, notarized

requires: accessibility permissions (to access selected text and to replace it, also accesses clipboard to bypass limitations of certain tools)

## Installation

1. Download dmg archive (from releases on the right side of this page)
2. Mount the dmg and move .app file to /Applications
3. Run the app
4. The tool comes with a few pre-installed transformations. You can import more from the [transformations](https://github.com/robert-v/Mutate-public/tree/main/transformations) folder or create your own transformations. Contributions are welcome!

Update to a new version: simply grab the newest dmg from Releases and replace your existing .app file in /Applications folder. Your existing Tools will be preserved.

## Usage
1. select any text
2. trigger Mutate with the defined shortcut (default is Cmd + Shift + u)
3. choose a tool from the list
4. press enter
5. selected text will be replaced with the output

## Features
- seamless text replacement without interrupting your worklfow and without switching to a differnt window
- ability to define your own transformation tools with Javascript (the app comes with a few default tools)
- register as startup item to be always available
- define your own shortcut
- import/export transformations to yaml

## Custom transformation examples

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

See more examples under [transformations](https://github.com/robert-v/Mutate-public/tree/main/transformations) folder

## Limitations
- Tools selector location - the tool tries to read selected text rectangle and change it's location accordingly, but some apps don't report this
- Terminals - the transformed text will not overwrite selected text but will appear at the cusor position

## Explore My macOS Apps
  
[ProcessSpy - Advanced process monitor for Mac](https://process-spy.app)

[Restretto - Minimal REST client for Mac](https://restretto.app)

[Essence - Minimal and focused log viewer for Mac](https://github.com/robert-v/Essence-public)

