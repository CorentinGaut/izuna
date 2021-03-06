![example workflow file path](https://github.com/matsumonkie/izuna/workflows/.github/workflows/main.yml/badge.svg)

# izuna

> Enhances Haskell code review for Github

Izuna brings a richer GitHub interface by showing type annotations directly in your browser.

![gif unified demo 1](./unified.gif)
![gif split demo 2](./split.gif)

## Requirements

As of today, the izuna plugin is only available for Chrome and your Haskell project needs to be using either GHC 8.10.1 or GHC 8.10.2

## How do I use it?

Go to the [chrome webstore](https://chrome.google.com/webstore/detail/izuna/fdddagbfkgicjkeijmbfdcmjeldegfdi) and install the izuna chrome extension.
Then you can either go to one of the [izuna-example](https://github.com/matsumonkie/izuna-example/pulls) pull requests or submit one to see izuna in action.

To use it for your own project, you'll also need to enable the github action [izuna-action](https://github.com/matsumonkie/izuna-action/).

For development purpose, you need to install the izuna plugin in chrome by going to `chrome://extensions/` and clicking `load unpacked` (then select the `chrome-extension` folder).

## How does it work?

Izuna makes use of [.hi extended](https://gitlab.haskell.org/ghc/ghc/-/wikis/hie-files) (AKA **hie files**) to recover information about your code. Your project information is then displayed by a plugin in your browser.

A more detailed worklow is:
1. Every time you push a commit, a GitHub Action will upload the hie files to a server
2. The server will then process the hie files
3. When you visit a pull request from your browser, information about this PR (if any available) will be fetched from the server and displayed in your browser thanks to a plugin.

## Features & Roadmap

✅: available<br/>
🔧: building<br/>


| available | feature                      | description                                          |
|-----------|------------------------------|------------------------------------------------------|
| ✅        | Type annotation              | Show type annotation for your haskell code           |
| ✅        | Split/Unified diff view mode | Works correctly for unified and split diff view mode |
| ✅        | Chrome support               |                                                      |
| ✅        | Security                     | Source code is no longer stored                      |
| ✅        | Syntax color                 | Display richer Haskell syntax color                  |
| 🔧        | GHC 8.10.3 support           | only GHC 8.10.1 and GHC 8.10.2 are available atm     |

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
