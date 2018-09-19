# A Fast "fastlane" Tutorial

installing on your macOS

> sudo gem install fastlane -NV 

**Important:** Don’t use *brew* for "future issues"

> vim  ~/.zshrc

add this line: export PATH="$HOME/.fastlane/bin:$PATH"

> fastlane init 

in your project’s root directory

> bundle exec fastlane beta  

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

Check my [Fastfile](Fastfile)

### GEMFILE

Check my [Gemfile](MyGemfile). 

Note: Please rename MyGemfile to Gemfile on your local Fastlane directory.

### APPFILE

Check my [Appfile](Appfile)

**Another Example**
https://gist.github.com/mcany/b207c18c5ea26f6d1d81d074888f2e1a

## Unistalling Fastlane

> brew cask uninstall fastlane

## Apple Versioning

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
How to Set up environment variables

fastlane requires some environment variables set up to run correctly. In particular, having your locale not set to a UTF-8 locale will cause issues with building and uploading your build. In your shell profile add the following lines:

> export LC_ALL=en_US.UTF-8

> export LANG=en_US.UTF-8


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

# Docs

* For list of all built-in fastlane actions and their available options, please check: https://docs.fastlane.tools/actions/
fastlane actions

Also, To get the most up-to-date information from the command line on your current version you can also run

> fastlane actions # list all available fastlane actions
> fastlane action [action_name] # more information for a specific action


