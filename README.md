# Why the fork?

Hello there! You might like to consider [something apart from Nuts](https://github.com/electron/electron/blob/main/docs/tutorial/updates.md#deploying-an-update-server).

*For example, this code was never deployed into any production environment I am aware of. In fact, it's almost certain to be superseded by any cloud storage backend, e.g. with https://www.electron.build/auto-update.html*

As [maintainer burnout is a thing](https://www.jeffgeerling.com/blog/2020/saying-no-burnout-open-source-maintainer), and the [original Nuts](https://github.com/GitbookIO/nuts) appears [to be abandoned](https://github.com/GitbookIO/nuts/issues/170) (thanks for all the great work!), this is a fork focused on upgrades as needed for general maintenance, reliability, security and on keeping the ability to download automatic updates by channel working when started locally (or deployed on a cloud provider, though I have not tested and have no intention to test Heroku) via the command line:

    # OWNER is a GitHub account, like pzrq
    # PRIVATE_REPO is any private repository with releases that need to be served publicly
    # TOKEN is most likely to be a GitHub server-to-server token, though other tokens might also work:
    #     https://github.blog/2021-04-05-behind-githubs-new-authentication-token-formats/
    GITHUB_ENDPOINT=https://api.github.com GITHUB_REPO=$OWNER/$PRIVATE_REPO GITHUB_TOKEN=$TOKEN PORT=1031 npm start 

Then visiting in a browser to retrieve JSON and following any links to get a working direct download link:

    http://localhost:1031/update/channel/stable/windows/1.0.0

Other bits simply aren't mission critical to my use case so may be working, or may have broken - PRs are welcome to fix any regressions, though no new features will be added.

More details can be found in the [CHANGELOG.md](./CHANGELOG.md)

---

# Nuts

Nuts is a simple (and smart) application to serve desktop-application releases.

![Schema](./docs/schema.png)

It uses GitHub as a backend to store assets, and it can easily be deployed to Heroku as a stateless service. It supports GitHub private repositories (useful to store releases of a closed-source application available on GitHub).

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)

#### Features

- :sparkles: Store assets on GitHub releases
- :sparkles: Proxy releases from private repositories to your users
- :sparkles: Simple but powerful download urls
    - `/download/latest`
    - `/download/latest/:os`
    - `/download/:version`
    - `/download/:version/:os`
    - `/download/channel/:channel`
    - `/download/channel/:channel/:os`
- :sparkles: Support pre-release channels (`beta`, `alpha`, ...)
- :sparkles: Auto-updates with [Squirrel](https://github.com/Squirrel)
    - For Mac using `/update?version=<x.x.x>&platform=osx`
    - For Windows using Squirrel.Windows and Nugets packages
- :sparkles: Private API
- :sparkles: Use it as a middleware: add custom analytics, authentication
- :sparkles: Serve the perfect type of assets: `.zip` for Squirrel.Mac, `.nupkg` for Squirrel.Windows, `.dmg` for Mac users, ...
- :sparkles: Release notes endpoint
    - `/notes/:version`
- :sparkles: Up-to-date releases (GitHub webhooks)
- :sparkles: Atom/RSS feeds for versions/channels

#### Deploy it / Start it

[Follow our guide to deploy Nuts](https://nuts.gitbook.com/deploy.html).


#### Auto-updater / Squirrel

This server provides an endpoint for [Squirrel auto-updater](https://github.com/atom/electron/blob/master/docs/api/auto-updater.md), it supports both [OS X](https://nuts.gitbook.com/update-osx.html) and [Windows](https://nuts.gitbook.com/update-windows.html).

#### Documentation

[Check out the documentation](https://nuts.gitbook.com) for more details.
