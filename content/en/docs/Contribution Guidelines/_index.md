---
title: "Contribution Guidelines"
linkTitle: "Contribution Guidelines"
weight: 9
description: >
  How to contribute to the Unofficial UCSC Guide
---

Hello and thank you for wanting to contribute to the project! All experience levels are welcome! Please take a look at ``./HELPWANTED.md`` to see items that are outside of the current team's expertise that need help to expand the scope of the project.

The Unofficial UCSC Student Guide is an open source project and welcome to patches, contributions, and improvements!

## Contributing to The Unofficial UCSC Student Guide
The Guide lives on [GitHub](https://github.com/hamorrar/ucsc-guide). You can view all of its source code there.

### For those inexperienced with programming: Create an Issue
If there's something you'd like to see in The Guide (or if you've found something that isn't working the way you'd expect), but you're not sure how to fix it yourself, please create an [issue](https://github.com/hamorrar/ucsc-guide/issues) or contact Hilal via email (hamorrar@ucsc.edu) or Discord (hmorrar#1632).

---

### For those experienced with programming:

#### **Initial Setup**
The guide uses the [extended version of hugo](https://github.com/gohugoio/hugo/releases) with the [Docsy theme](https://www.docsy.dev/docs/getting-started/).

1. Fork the repository on GitHub.
1. Use the recursive tag when cloning your fork so that all the submodules are also downloaded: `git clone --recursive git@github.com:your-username/ucsc-guide.git`
1. ``cd ucsc-guide`` to navigate into the project.
1. Install all the dependencies: `npm install`
1. Use the `hugo serve` command to start the server.
1. Open a browser and go to ``https://localhost:1313/ucsc-guide``.

#### **Create a Pull Request and Preview Locally**
Continue with the usual GitHub workflow to edit files, commit them, push the changes up to your fork, and create a pull request. For this project, most changes will be in [./content/en/docs](./content/en/docs/). For more general information on how to contribute to open source projects, check out [Open Source Guides](https://opensource.guide/how-to-contribute/). Please follow similar writing style in new contributions.

Steps to contribute:
1. Fork the repository.
1. Clone your fork to your machine.
1. Create or checkout an/the appropriate branch.
1. Commit your changes.
1. Push to your fork of the repo.
1. Make a Pull Request for review.

### Code reviews
Submissions will be reviewed by at least one person (Hilal). We use GitHub pull requests for this purpose. Consult [GitHub Help](https://help.github.com/articles/about-pull-requests/) for more information on using pull requests.

---

### Code of Conduct
This project follows the[Contributor Covenant Code of Conduct](./CODE_OF_CONDUCT.md).

### License
By contributing, you agree that your contributions will be licensed under its GNU General Public License v3.0.