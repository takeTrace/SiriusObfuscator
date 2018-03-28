# Obfuscation tool

## Overview

This is the umbrella tool that exposes the unified command line interface to perform the obfuscation of Xcode project.

## Usage

```bash
$ obfuscator -projectrootpath <path-to-xcode-project> -obfuscatedproject `<path-for-obfuscated-project>` [-namemappingstrategy <name-mapping-strategy>] [-keepintermediates] [-verbose]
```

where

`<path-to-xcode-project>` is a path to Xcode project root folder. It\'s the folder that contains both the Xcode project file (.xcodeproj or .xcworkspace) and the source files. It is passed to _FileExtractor_ tool.

`<path-for-obfuscated-project>` is the path to the directory that the newly generated obfuscated Swift source code files will be written to, as well as the new project. Is is passed to _Renamer_ tool.

In case when project should be obfuscated in place (without making a copy), `-inplace` argument can be used instead of `-obfuscatedproject`.

`<name-mapping-strategy>` is the optional parameter of type enum string. Is is passed to _NameMapper_ tool. Is determines, which of the following strategies is used when generating the obfuscated symbol names:

- `random` strategy generates random alphanumeric strings of length 32, e.g. `gnxWyHU0uN3bXejy8bVAoNbyfg4gRuN8`.
- `deterministic` strategy generates deterministic renames based on symbol's original name, e.g. `T1_RootViewController`.
- `minifying` strategy generates strings as short as possible, e.g. `a`.

When the `-namemappingstrategy` parameter is not provided, the default `random` strategy is used.

`-keepintermediates` is the optional flag. When present, the interemediate files used to pass the necessary info between the tools invoked by _ObfuscatorTool_ (`files.json`, `symbols.json`, `renames.json`) will not be removed after successful obfuscation process.

`-verbose` is the optional flag. When present, the flag is passed to each tool invoked by _ObfuscatorTool_ and all debug info messages from each tool are printed to standard output.


## Build notes for developers

1. Clone the source  
   `git clone ssh://git@gitlab2.polidea.com:23/SwiftObfuscator/ObfuscatorTool.git`

2. Add git-subtrees remotes
   `bash Scripts/git_remotes.sh`

3. (optional, do it if there's a need for updating the dependencies) Update dependecies
   `bash Scripts/git_update.sh`

4. Build all the dependent projects and the main project
   `bash Scripts/build.sh`

## Further read

Please consult the [Documentation](Documentation/) folder for the further explanations.

## Licence

TBA

## Contributors

In the alphabetical order:

* [Jerzy Kleszcz](jerzy.kleszcz@polidea.com)
* [Krzysztof Siejkowski](krzysztof.siejkowski@polidea.com)
