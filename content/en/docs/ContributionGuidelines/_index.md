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

1. Install Git.
1. Install Node (and its dependencies if on Windows).
1. Download and install the extended version of Hugo (linked above). You can also use ``snap`` to install the extended version of Hugo with ``sudo snap install hugo --channel=extended``. ``snap`` works with a lot of Linux distros, and is pre-installed with some major distros such as Ubuntu 16.04+.
1. Fork the repository on GitHub.
1. Use the recursive tag when cloning your fork so that all the submodules are also downloaded: ``git clone --recursive git@github.com:your-username/ucsc-guide.git``
1. ``cd ucsc-guide`` to navigate into the project.
1. Install all the dependencies: `npm install`.
1. Use the ``hugo serve`` or ``hugo server`` command to start the server. If you would like to expose the website to your network, use ``hugo serve --bind 0.0.0.0`` or ``hugo server --bind 0.0.0.0``. This is useful for accessing the site from another machine when you are using a GUI-less OS to run the site.
1. Open a browser and go to ``https://localhost:1313/ucsc-guide``.

#### **Notes for Hugo Development**
The repository looks a bit intimidating at first but most of it is all set up from Hugo initially and I fixed it up so most of the work will be done in the [./content/en/docs](./content/en/docs/) directory to write up articles in Markdown. Also when previewing changes locally, be careful of the ``draft`` value in the top of the Markdown file you are working in. If it is set to ``true`` it will not show up in the final build, but it will show up in a preview only if you use the ``-D`` flag in when starting the local server. Every article page you want to write has to have those preamble lines (Hugo calls it "front matter") at the top for it to render correctly (or at all). You can copy and paste from another file and modify the appropriate fields.

- ``title`` is the title of the article
- ``linkTitle`` is what will show up in the left navigation bar
- ``weight`` is for ordering the pages in the directory for the left navigation bar
- ``icon`` is if you want to put an emote next to the title in the left navigation bar from [Font Awesome](https://fontawesome.com/v5.15/icons?d=gallery&p=2)
- ``draft`` is to publish the file on the site if it is in the main branch (``false`` - not a draft. ``true`` - is a draft)
- ``description`` is a quick one line summary/preview/subtitle for the article to display under the main title on the page

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
This project follows the [Contributor Covenant Code of Conduct](./CODE_OF_CONDUCT.md).

### License
By contributing, you agree that your contributions will be licensed under its GNU General Public License v3.0.