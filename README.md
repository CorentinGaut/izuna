# izuna

> Enhances Haskell code review for Github

Izuna brings a richer GitHub interface by showing type annotations directly in your browser.

![gif demo](./demo.gif)

## Requirements

As of today, the izuna plugin is only available for Chrome and your Haskell project needs to be using GHC 8.10.1.

## How do I use it?

If you only want to play with it, you need to install the izuna plugin in chrome by going to `chrome://extensions/` and clicking `load unpacked` (then select the `chrome-extension` folder). Then you can either go to one of the [izuna-example](https://github.com/matsumonkie/izuna-example/pulls) pull requests or submit one.

To use it for your own project, you'll need to enable the github action [izuna-action](https://github.com/matsumonkie/izuna-action/).

## How does it work?

Izuna makes use of [.hi extended](https://gitlab.haskell.org/ghc/ghc/-/wikis/hie-files) (AKA **hie files**) to recover information about your code. Your project information is then displayed by a plugin in your browser.

A more detailed worklow is:
1. Every time you push a commit, a GitHub Action will upload the hie files to a server
2. The server will then process the hie files
3. When you visit a pull request from your browser, information about this PR (if any available) will be fetched from the server and displayed in your browser thanks to a plugin.

## Features & Roadmap

✅: available<br/>
🔧: building<br/>


| available | feature                | description                                                |
|-----------|------------------------|------------------------------------------------------------|
| ✅        | Type annotation        | Show type annotation for your haskell code                 |
| ✅        | Unified diff view mode | Works correctly for unified diff view mode                 |
| ✅        | Chrome support         |                                                            |
| 🔧        | Firefox support        |                                                            |
| 🔧        | Split diff view mode   |                                                            |
| 🔧        | GHC 8.10.2 support     | only GHC 8.10.1 is available atm                           |
| 🔧        | Security               | Make sure private repos are only accessible by their owner |
| 🔧        | Syntax color           | Display richer Haskell syntax color                        |

## Caveats

- Izuna is as of today (December 2020) a first draft and might fail in some scenarios.
- There is no authentication/authorization present at the moment. Any individual that has the tuple **owner/repository/commitId** for your project will be able to access your code. Private repos should use Izuna at their own risks.

## How to build

### Github Action

Please go to the [izuna-action](https://github.com/matsumonkie/izuna-action/) repo for more information.

### izuna-builder/izuna-server

izuna-builder is the core of the project. Its purpose is to receive a hie files tar archive from the github action and extract it.
Then it needs to parse the hie files and recover any useful information.

Build with:
```bash
stack build izuna-builder --stack-yaml=stack-8.10.1.yaml --no-nix
```

izuna-server is a simple server that returns the processed hie files for the plugin.

Build with:
```bash
stack build izuna-server --stack-yaml=stack-8.10.1.yaml --no-nix
```

## Inspirations

Izuna was (more than) inspired by:
- [Haskell-code-explorer](https://github.com/alexwl/haskell-code-explorer) by Alexwl
- [Haddock](https://github.com/haskell/haddock/)

Many thanks to [Weeder](https://github.com/ocharles/weeder/) by Ocharles and [Stan](https://github.com/kowainik/stan) by Kowainik which helped me understand better how Hie files work.


Icons made by [Freepik](https://www.flaticon.com/authors/freepik)
