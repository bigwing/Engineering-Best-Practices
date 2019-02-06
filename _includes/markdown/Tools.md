The following are tools we use at BigWing. This list will grow and change over time and is not meant to be comprehensive. Generally, we encourage or require these tools to be used in favor of other ones. Rules governing tools to be used and packaged with a client site will be much stricter than those used on internal projects.

<h2 id="local-development" class="anchor-heading">Local Development Environments {% include Util/top %}</h2>

At BigWing, we use [Local by Flywheel](https://local.getflywheel.com/) to build and interact with virtual environments that match production as closely as possible. Local is a Docker-based virtual environment for WordPress development that works on Mac or Windows. Local will also setup a file structure to allow easy manual theme tweaks, allow SSH keys, and support WP-CLI access for WordPress command line tinkering.

There are many setups and configurations available when you start a new local environment, but the following setup is largely preferred internally:

* PHP Version: 7.2.0
* Web Server: Apache
* MySQL Version: 5.6

Note that when opening a legacy website project in Local it should be pre-packaged with settings based upon either the versions that were current at the time of initial deployment or the settings that fit the client's needs at the time.

<h2 id="scaffolding" class="anchor-heading">Scaffolding {% include Util/top %}</h2>

[WP Rig](https://github.com/wprig/wprig/) - Our general preference for all custom theme development is to use WP Rig to quickly create themes with our recommended tools and many of our best practices already in place. It already utilizes task runners and parsers such as Gulp, Babel, and PostCSS, parses JS using ES2015, and formats all output code using ESLint.

Before utilizing WP Rig you'll need to install and configure the following dependencies:

* [Node.js](https://nodejs.org) - Installing Node via the official utility will also install NPM, but on Mac it won't necessarily include the command-line tools you'll need before running it via terminal.
* Mac OSX Command Line Tools - If this does not prompt to install along with Node (or when attempting to run a module via terminal) then you can install the necessary command-line tools by launching terminal and typing `xcode-select --install`. Note, if you still get permission errors when installing you can change the location where node modules are installed by doing the following: `mkdir ~/.npm-packages` will set node modules to install to a newly created folder which doesn't have set permissions. `npm config set prefix ~/.npm-packages` will configure Node to stash its modules in that new folder from now on.
* [Composer](#package-managers) - Covered in more detail below, but must be installed globally (run `npm install` with the `-g` handle) for WP Rig to be able to utilize it.
* Mac OSX Bash profile changes - Based on the above changes you'll need to make sure that your `.bash_profile` file contains the proper export paths by opening it in a text editor or terminal. It should always include `export PATH="usr/local/bin:$PATH"` but below that somewhere you should also make sure that `export PATH="$HOME/.composer/vendor/bin:$PATH"` is present after installing Composer and that `export PATH="/Users/YOURNAME/.npm-packages/bin:$PATH"` (where YOURNAME is your user on your machine) has been updated if you had to move where Node installs its modules via one of the steps above.

Note, even on development projects where a child theme was customized in lieu of a custom scaffolding it is likely that they were built using Node, Composer, task runners, and other utilities listed below.

<h2 id="task-runners" class="anchor-heading">Task Runners {% include Util/top %}</h2>

[Grunt](http://gruntjs.com/) - Grunt is a task runner built on Node that lets you automate tasks like Sass preprocessing and JS minification. Grunt is our default task runner and has a great community of plugins and solutions we use for on company and client projects.

[Gulp](http://gulpjs.com/) - Gulp is also a task runner build on Node that offers a similar suite of plugins and solutions to Grunt. The biggest difference is Gulp allows you direct access to the [stream](https://nodejs.org/api/stream.html) of information from your source files and allows you to modify this data directly.

[Sass](https://sass-lang.com/install) - Though Grunt and Gulp above are more commonly included as dependencies within many of our projects some legacy sites or third party themes may not already include a precompiler. In those cases it is handy to have Sass already installed globally so that it can be run as needed to aid in CSS styling.

[Webpack](https://webpack.github.io/) - Webpack is a bundler for JS/CSS. It's extremely useful when building larger JavaScript applications (i.e. React.js).

<h2 id="package-managers" class="anchor-heading">Package/Dependency Managers {% include Util/top %}</h2>

[Composer](https://getcomposer.org) - We use Composer for managing PHP dependencies. Usually everything we need is bundled with WordPress, but sometimes we need external PHP libraries like "Patchwork". Composer is a great way to manage those external libraries.

When a WordPress install is managed and maintained by an engineering team, and when the infrastructure supports it, plugins in a WordPress project can be easily managed using Composer. [WordPress Packagist](https://wpackagist.org/) provides a Composer repository that mirrors all public WordPress plugins and themes.

<h2 id="version-control" class="anchor-heading">Version Control {% include Util/top %}</h2>

[Git](https://git-scm.com) - At 10up we use Git for version control. We encourage people to use the command line for interacting with Git. GUIs are permitted but will not be supported internally.

[SVN](https://subversion.apache.org/) - We use SVN, but only in the context of WordPress.com VIP. Again, we encourage people to use the command line as we do not support GUIs internally.

<h2 id="command-line" class="anchor-heading">Command Line Tools {% include Util/top %}</h2>

[WP-CLI](https://wp-cli.org) - A command line interface for WordPress. This is an extremely powerful tool that allows us to do imports, exports, run custom scripts, and more via the command line. Often this is the only way we can affect a large database (WordPress.com VIP or WP Engine). This tool is installed by default on [WP Local Docker](https://10up.github.io/wp-local-docker-docs/).

<h2 id="a11y-testing" class="anchor-heading">Accessibility Testing {% include Util/top %}</h2>

We use a variety of tools to test our sites for accessibility issues. WebAim has some great resources on [how to evaluate sites](http://webaim.org/articles/screenreader_testing/) with a screen reader.

* [Using VoiceOver](http://webaim.org/articles/voiceover/)
* [Using NVDA](http://webaim.org/articles/nvda/)
* [Using JAWS](http://webaim.org/articles/jaws/)

We're also a fan of a few browser tools that lend us a hand when it comes to testing areas like color contrast, heading hierarchy, and ARIA application.

* [Headings Map for Chrome](https://chrome.google.com/webstore/detail/headingsmap/flbjommegcjonpdmenkdiocclhjacmbi?hl=es) or [Headings Map for Firefox](https://addons.mozilla.org/en-us/firefox/addon/headingsmap/) - A browser extension that allows you to see the heading structure of a webpage.
* [The Visual ARIA Bookmarklet](http://whatsock.com/training/matrices/visual-aria.htm) - A bookmarklet that can be run on a webpage and color codes ARIA roles.
* [WAVE](http://wave.webaim.org/) - A toolkit from WebAIM, that also has an extension for Chrome/Firefox. It evaluates a webpage and returns accessibility errors.
* [Accessibility Developer Tools](https://chrome.google.com/webstore/detail/accessibility-developer-t/fpkknkljclfencbdbgkenhalefipecmb) - A Chrome extension that adds an "Audit" tab in Chrome's developer tools that can scan a webpage for accessibility issues.
* [Tota11y](https://khan.github.io/tota11y/) - A visualization toolkit that can be used as a bookmarklet, and reveals accessibility errors on a webpage.
* [Contrast Ratio](https://leaverou.github.io/contrast-ratio/) - A color contrast tool to compare two colors against [levels of conformance](https://www.w3.org/TR/UNDERSTANDING-WCAG20/conformance.html) and see if they pass.
* [Tanagaru Contrast Finder](http://contrast-finder.tanaguru.com/?lang=en) - Another color contrast tool that tests colors against the levels of conformance, but also provides you with alternatives should your provided colors fail.