# Overview

Acknowledge is a simple bash script that will easily generate a rtf that contains all the acknowledgments for libraries, frameworks and other code you've used in your iOS or OSX project.

It's made to work very well with [DCOAboutWindow](https://github.com/DangerCove/DCOAboutWindow) and [Cocoapods](http://www.cocoapods.org). Acknowledge relies on [MultiMarkdown by Fletcher Penny](http://fletcherpenney.net/multimarkdown).

![Acknowledgments generated by Acknowledge](https://raw.github.com/DangerCove/Acknowledge/master/screenshots/acknowledgments.png)

# Setup

## Clone

Clone this repo, preferably into the root of your Xcode project:

    $ git clone git@github.com:DangerCove/Acknowledge.git

Or if your project is a repo already, add it as a submodule:

    $ git submodule add git@github.com:DangerCove/Acknowledge.git

## Install multimarkdown

Follow [the guide](http://fletcherpenney.net/multimarkdown/install) on Fletcher's website, or if you're using homebrew:

    $ brew install multimarkdown

## Configure

Copy acknowledge.cfg.default to acknowledge.cfg:

    $ cd Acknowledge
    $ cp acknowledge.cfg.default acknowledge.cfg

Customize the paths to multimarkdown and your Pods folder if necessary.

## Add acknowledgments

### Cocoapods

If you use Cocoapods and have your Pods directory setup, you are ready to go. Just run `acknowledge`.

    $ ./acknowledge

### Other acknowledgments

Just add a markdown file to the `sources` directory and Acknowledge will handle the rest. Make sure the extension is `.md`.

### Order

You might've notice the `10_` and `20_` prefixes in front of the files in the `sources` folder. Acknowledge will concatenate the files in order, so just add files and change to number to change the order.

The acknowledgments generated by Cocoapods will always be prepended with `10_`.

## Potential directory layout

    .
    |- Acknowledge/
    |   |- acknowledge
    |   |- ...
    |   |- source/
    |   |   |- 11_Vendor.md
    |   |   |- 20_Acknowledge.md
    |- Pods/
    |   |- Pods-acknowledgements.markdown
    |-  |- ...
    |- Podfile
    |- Coolproject.xcodeproj
    |- Coolproject.xcworkspace
    |- ...

## Test it

Don't skip this step, you'll need to output in the next one.

Open a terminal window and run `acknowledge` once to see if it works, and to generate the initial `Acknowledgments.rtf`.

    $ ./acknowledge

Fix any errors and proceed.

## Add it to Xcode

### Add the acknowledgments to your project

You'll probably want to show the acknowledgments somewhere in your app (have a look at [DCOAboutWindow](https://github.com/DangerCove/DCOAboutWindow) if you're working on a Mac app, btw).

Simply add the generated `Acknowledgments.rtf` file to your project and display it somewhere.

### Generate the acknowledgments on each build

Keeping your acknowledgments up to date is easy if you add Acknowledge as a build phase. Here's how that works:

1. Open Xcode;
1. Select your project and open the `Build Phases` tab;
1. Click `Editor → Add Build Phase → Add Run Script Build Phase`;
1. Name your script something like "Update Acknowledgments" and position it so that it's above `Copy Bundle Resources`;
1. Now add the following code:

`cd Acknowledge && ./acknowledge`

(Make sure to adapt the paths if the script isn't located in the default folder.)

It should look something like this:

![Acknowledge Build Phase](https://raw.github.com/DangerCove/Acknowledge/master/screenshots/build-phase.jpg)

That's it! Just build your project and you're set.

# Contributions and things to add

Be creative. Acknowledge should be a flexible, easy to use way to generate acknowledgments. Make sure your changes don't break existing functionality without good reason.

# License

MIT License, see `LICENSE` for details.
