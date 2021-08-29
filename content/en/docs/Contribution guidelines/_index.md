---
title: "Contribution Guidelines"
linkTitle: "Contribution Guidelines"
weight: 9
description: >
  How to contribute to the Unofficial UCSC Guide
---

The Unofficial UCSC Student Guide is an open source project and welcome to patches, contributions, and improvements!

## Contributing to The Unofficial UCSC Student Guide
The Guide lives on [GitHub](https://github.com/hamorrar/ucsc-guide). You can view all of its source code there.

### For those inexperienced with programming: Create an Issue
If there's something you'd like to see in The Guide (or if you've found something that isn't working the way you'd expect), but you're not sure how to fix it yourself, please create an [issue](https://github.com/hamorrar/ucsc-guide/issues).

### For those experienced with programming: Create a Pull Request and Preview Locally
Navigate to the root of the repository in your terminal and type in ``hugo serve``. The website will be hosted locally at ``http://localhost:1313/ucsc-guide`` for you to preview your changes in the browser. Continue with the usual GitHub workflow to edit files, commit them, push the changes up to your fork, and create a pull request. For this project, most changes will be in ``./content/en/docs/``. For more information on how to contribute, check out [Open Source Guides](https://opensource.guide/how-to-contribute/). Please follow similar writing style in new posts.
Steps to contribute:
1. Fork the repository.
1. Clone your fork to your machine.
1. Create or checkout an/the appropriate branch.
1. Commit your changes.
1. Push to your fork of the repo.
1. Make a Pull Request for review.

### Initial setup
The guide uses the [extended version of hugo](https://github.com/gohugoio/hugo/releases) with the [docsy theme](https://www.docsy.dev/docs/getting-started/). The first time setup has a couple of extra steps.
1. Use the recursive tag when cloning your fork so that all the submodules are also downloaded: `git clone --recrusive git@github.com:your-username/ucsc-guide.git`
1. cd into the directory and install all the dependencies. `npm install`
1. Use the `hugo server` command to start the server.

### Code reviews
Submissions will be reviewed by at least one person (Hilal). We use GitHub pull requests for this purpose. Consult [GitHub Help](https://help.github.com/articles/about-pull-requests/) for more information on using pull requests.

### Community guidelines
This project follows [Google's Open Source Community Guidelines](https://opensource.google.com/conduct/).

### License
By contributing, you agree that your contributions will be licensed under its GNU General Public License v3.0.
