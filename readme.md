# Foam

👋 Welcome to your new Foam Workspace!

## New features

This template supports rendering LaTeX with KaTeX! See here: [[math]].

The caveat is: we can no longer use GitHub Pages' default solution to build and deploy our Jekyll site. Because we are using a separate Jekyll plugin which is [linjer/jekyll-katex](https://github.com/linjer/jekyll-katex), and GitHub Pages' Jekyll build environment doesn't allow all third party plugins, which means we will run into issues like [The tag katex is not a recognized Liquid tag](https://github.com/linjer/jekyll-katex/issues/33).

So, we will be deploying this to Vercel or Netlify instead!

## Getting started

This documentation assumes that you have a GitHub account and have [Visual Studio Code](https://code.visualstudio.com/) installed on your Linux/MacOS/Windows machine.

1. If you haven't yet, browse over to the main [Foam documentation workspace](https://foambubble.github.io/foam) to get an idea of what Foam is and how to use it.
2. Press "Use this template" button at [foam-template](https://github.com/foambubble/foam-template/generate) (that's this repository!) to fork it to your own GitHub account. If you want to keep your thoughts to yourself, remember to set the repository private.
3. [Clone the repository to your local machine](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository) and open it in VS Code.

    *Open the repository as a folder using the `File > Open...` menu item. In VS Code, "open workspace" refers to [multi-root workspaces](https://code.visualstudio.com/docs/editor/multi-root-workspaces).*

4. When prompted to install recommended extensions, click **Install all** (or **Show Recommendations** if you want to review and install them one by one)

After setting up the repository, open [.vscode/settings.json](.vscode/settings.json) and edit, add or remove any settings you'd like for your Foam workspace.

To learn more about how to use **Foam**, read the [Recipes](https://foambubble.github.io/foam/recipes) bubbles of the Foam documentation workspace.


## Using Foam

We've created a few Bubbles (markdown documents) to get you started.

- [[inbox]] - a place to write down quick notes to be categorised later
- [[foam-tips]] - tips to get the most out of your Foam workspace
- [[todo]] - a place to keep track of things to do

## Note on `[[wiki-links]]`

⚠️ Until [foambubble/foam#16](https://github.com/foambubble/foam/issues/16) is resolved, `[[wiki-links]]` links (like the links above) won't work in the GitHub Markdown preview (i.e. this Readme on github.com).

They should work as expected in VS Code, and in rendered GitHub Pages.

If GitHub preview (or general 100% support with all Markdown tools) is a requirement, for the time being you can use the standard `[description](page.md)` syntax.



[//begin]: # "Autogenerated link references for markdown compatibility"
[math]: math.md "Math"
[inbox]: inbox.md "Inbox"
[foam-tips]: foam-tips.md "Foam tips"
[todo]: todo.md "Todo"
[//end]: # "Autogenerated link references"
