
> pbl-docs@1.0.0 markdownlint /Users/yusukehirono/Documents/code/PBL-docs
> markdownlint README

Usage: markdownlint [options] [files|directories|globs...]

MarkdownLint Command Line Interface

Arguments:
  files|directories|globs                    files, directories, and/or globs to lint

Options:
  -V, --version                              output the version number
  -c, --config <configFile>                  configuration file (JSON, JSONC, JS, YAML, or TOML)
  --configPointer <pointer>                  JSON Pointer to object within configuration file (default: "")
  -d, --dot                                  include files/folders with a dot (for example `.github`)
  -f, --fix                                  fix basic errors (does not work with STDIN)
  -i, --ignore <file|directory|glob>         file(s) to ignore/exclude (default: [])
  -j, --json                                 write issues in json format
  -o, --output <outputFile>                  write issues to file (no console)
  -p, --ignore-path <file>                   path to file with ignore pattern(s)
  -q, --quiet                                do not write issues to STDOUT
  -r, --rules <file|directory|glob|package>  include custom rule files (default: [])
  -s, --stdin                                read from STDIN (does not work with files)
  --enable <rules...>                        Enable certain rules, e.g. --enable MD013 MD041 --
  --disable <rules...>                       Disable certain rules, e.g. --disable MD013 MD041 --
  -h, --help                                 display help for command
