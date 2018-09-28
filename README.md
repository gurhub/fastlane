**Warning: This document is still work in progress**

# A Fast "fastlane" Setup Tutorial

installing on your macOS

> sudo gem install fastlane -NV 

**Important:** Don’t use *brew* for "future issues"

> vim  ~/.zshrc

add this line: export PATH="$HOME/.fastlane/bin:$PATH"

> fastlane init 

in your project’s root directory

> bundle exec fastlane beta --verbose

**beta** is the name of your Fastlane file's **lane** section.

**Fastlane Summary**

| Step | Action | Time (in s) |
|--|--|--|
| 1 | opt_out_usage | 0 |
| 2 | default_platform | 0 |
| 3 | cocoapods | 11 |
| 4 | gym | 132 |
| 5 | pilot | 94 |
| 6 | upload_symbols_to_crashlytics | 4 |

*fastlane.tools finished successfully* 🎉

### FASTFILE

Check my [Fastfile](https://github.com/gurhub/fastlane/blob/master/Fastfile)

### GEMFILE

Check my [Gemfile](https://github.com/gurhub/fastlane/blob/master/MyGemfile). 

Note: Please rename MyGemfile to Gemfile on your local Fastlane directory.

### APPFILE

Check my [Appfile](https://github.com/gurhub/fastlane/blob/master/Appfile)

## Unistalling Fastlane

> brew cask uninstall fastlane

# Other Useful Actions

## clear_derived_data

Deletes the Xcode Derived Data.

# Apple Versioning

Automating Version and Build Numbers Using agvtool.

https://developer.apple.com/library/archive/qa/qa1827/_index.html

you can check if it’s enabled:

> xcrun agvtool what-version

**other options:**
agvtool what-marketing-version

# Warnings | Errors

## UTF-8 Warning

WARNING: fastlane requires your locale to be set to UTF-8. To learn more go to 
https://docs.fastlane.tools/getting-started/ios/setup/#set-up-environment-variables
How to Set up environment variables:

Set up environment variables

fastlane requires some environment variables set up to run correctly. In particular, having your locale not set to a UTF-8 locale will cause issues with building and uploading your build. Open your shell profile with:

> vim ~/.zshrc

and add the following lines:

> export LC_ALL=en_US.UTF-8

> export LANG=en_US.UTF-8

Note: You can find your shell profile at ~/.bashrc, ~/.bash_profile, ~/.profile or ~/.zshrc depending on your system. 

## permission denied: bundle

first check "which bundle” command, if it’s not installed on your system

> sudo gem install bundler -n /usr/local/bin

## cocoapods gem error

 Add 'gem "cocoapods"' to your Gemfile and restart fastlane, try this:

if you install with brew first uninstall brew version of it:

> brew cask uninstall fastlane

then
> sudo gem install fastlane -NV -n /usr/local/bin


## Transporter Error Output]: Could not start delivery: all transports failed diagnostics

Ready to upload new build to TestFlight (App: 1241913459)...
[14:26:33]: Going to upload updated app to App Store Connect
Transporter Error Output]: Could not start delivery: all transports failed diagnostics
INFO: The Signiant transfer engine's status is DISCONNECTED

Solution: 
run the command line below:

> export DELIVER_ITMSTRANSPORTER_ADDITIONAL_UPLOAD_PARAMETERS="-t DAV"

then retry!

##  Could not find unf_ext-0.0.7.5 in any of the sources
Ignoring bigdecimal-1.3.5 because its extensions are not built. Try: gem pristine bigdecimal --version 1.3.5
Could not find unf_ext-0.0.7.5 in any of the sources
Run `bundle install` to install missing gems.

Solution: 
Run 

> bundle install --verbose

then retry!

## To fix Bundler errors

First unsinstall with command below:

> sudo gem uninstall -n /usr/local/bin bundler

will ask you "Select gem to uninstall", you can seleck All option if you have more then one gem. 

Then run:

> sudo gem install -n /usr/local/bin bundler

# Other Examples

* https://github.com/fastlane/examples
* https://gist.github.com/mcany/b207c18c5ea26f6d1d81d074888f2e1a


# Docs

* For list of all built-in fastlane actions and their available options, please check: https://docs.fastlane.tools/actions/
fastlane actions

Also, To get the most up-to-date information from the command line on your current version you can also run

> fastlane actions # list all available fastlane actions
> fastlane action [action_name] # more information for a specific action


