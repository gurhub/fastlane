# The fastlane Setup Steps

### Installing on your macOS

```bash
$ brew update
$ brew install rbenv
``` 

### Add the following in .bashrc file:
```bash
eval "$(rbenv init -)"
``` 

### Now, we can look at the list of ruby versions available for install
```bash
$ rbenv install -l
``` 

### Install version 2.3.8 for example
```bash
$ rbenv install 2.7.6
``` 

### Now we can use this ruby version globally
```bash
$ rbenv global 2.3.8
```

### Finally run
```bash
$ rbenv rehash
```

```bash
$ which ruby
/Users/myuser/.rbenv/shims/ruby
```

```bash
$ ruby -v
ruby 2.3.7p456 (2018-03-28 revision 63024) [x86_64-darwin17]
```

### Go for it

Now install bundler

```bash
$ gem install bundler
```

### Create a ./Gemfile in the root directory of your project with the content

```bash
source "https://rubygems.org"

gem "fastlane"
```

then

```bash
> sudo gem install fastlane -NV 
```
remember

* Run bundle update and add both the ./Gemfile and the ./Gemfile.lock to version control
* Every time you run fastlane, use 
```bash
bundle exec fastlane [lane]
```
* On your CI, add bundle install as your first build step
* To update fastlane, just run 
```bash
bundle update fastlane
```

**⚠️** Don’t use *brew* for "future issues"

```bash
> vim  ~/.zshrc
```

add this line: export PATH="$HOME/.fastlane/bin:$PATH"

```bash
> fastlane init 
```

# Run

run in your project’s root directory

```bash
> bundle exec fastlane beta --verbose
```

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

# Targeting tvOS

If you're working on a **tvOS** project then you need to use it like in example: [Fastfile_tvOS](https://github.com/gurhub/fastlane/blob/master/Fastfile_tvOS) 

**Warning:** Please don't forget that tvOS support is still experimental and platform 'appletvos' is **not officially supported**. Currently supported platforms are [:ios, :mac, :android]. But your lane will work like a charm.

## Unistalling Fastlane

```bash
> brew cask uninstall fastlane
```

# Other Useful Actions

## clear_derived_data

Deletes the Xcode Derived Data.

# Apple Versioning

### Automating Version and Build Numbers Using agvtool.

https://developer.apple.com/library/archive/qa/qa1827/_index.html

you can check if it’s enabled:

```bash
> xcrun agvtool what-version
```

**other options:**
```bash
agvtool what-marketing-version
```

# Warnings | Errors

## UTF-8 Warning

WARNING: fastlane requires your locale to be set to UTF-8. To learn more go to 
https://docs.fastlane.tools/getting-started/ios/setup/#set-up-environment-variables
How to Set up environment variables:

Set up environment variables

fastlane requires some environment variables set up to run correctly. In particular, having your locale not set to a UTF-8 locale will cause issues with building and uploading your build. Open your shell profile with:

```bash
> vim ~/.zshrc
```bash

and add the following lines:

```bash
> export LC_ALL=en_US.UTF-8

> export LANG=en_US.UTF-8
```

Note: You can find your shell profile at ~/.bashrc, ~/.bash_profile, ~/.profile or ~/.zshrc depending on your system. 

## permission denied: bundle

first check "which bundle” command, if it’s not installed on your system

```bash
> sudo gem install bundler -n /usr/local/bin
```

## cocoapods gem error

 Add 'gem "cocoapods"' to your Gemfile and restart fastlane, try this:

if you install with brew first uninstall brew version of it:

```bash
> brew cask uninstall fastlane
```

then

```bash
> sudo gem install fastlane -NV -n /usr/local/bin
```

## Sign in with the app-specific password you generated. If you forgot the app-specific password or need to create a new one, go to appleid.apple.com (-22938)

Transporter transfer failed.Sign in with the app-specific password you generated. If you forgot the app-specific password or need to create a new one, go to appleid.apple.com (-22938)Your account has 2 step verification enabled. Please go to https://appleid.apple.com/account/manage and generate an application specific password for the iTunes Transporter, which is used to upload builds. To set the application specific password on a CI machine using an environment variable, you can set the FASTLANE_APPLE_APPLICATION_SPECIFIC_PASSWORD variable.

Goto https://appleid.apple.com/, under Security find:

APP-SPECIFIC PASSWORDS

Use the "Generate Password" link to create a new password. Set the FASTLANE_APPLE_APPLICATION_SPECIFIC_PASSWORD environment variable in your .bash_profile file. This file could be different depending on your chose for the bash on your terminal. Add this line:

```bash
export FASTLANE_APPLE_APPLICATION_SPECIFIC_PASSWORD="XXX"
```

## Transporter Error Output]: Could not start delivery: all transports failed diagnostics

Ready to upload new build to TestFlight (App: 1241913459)...
[14:26:33]: Going to upload updated app to App Store Connect
Transporter Error Output]: Could not start delivery: all transports failed diagnostics
INFO: The Signiant transfer engine's status is DISCONNECTED

Solution: 
run the command line below:

```bash
> export DELIVER_ITMSTRANSPORTER_ADDITIONAL_UPLOAD_PARAMETERS="-t DAV"
```

then retry!

##  Could not find unf_ext-0.0.7.5 in any of the sources
Ignoring bigdecimal-1.3.5 because its extensions are not built. Try: gem pristine bigdecimal --version 1.3.5
Could not find unf_ext-0.0.7.5 in any of the sources
Run `bundle install` to install missing gems.

Solution: 
Run 

```bash
> bundle install --verbose
```

then retry!

## To fix Bundler errors

First unsinstall with command below:

```bash
> sudo gem uninstall -n /usr/local/bin bundler
```

will ask you "Select gem to uninstall", you can seleck All option if you have more then one gem. 

Then run:

```bash
> sudo gem install -n /usr/local/bin bundler
```

# Other Examples

* https://github.com/fastlane/examples
* https://gist.github.com/mcany/b207c18c5ea26f6d1d81d074888f2e1a

# Docs

* For list of all built-in fastlane actions and their available options, please check: https://docs.fastlane.tools/actions/
fastlane actions

Also, To get the most up-to-date information from the command line on your current version you can also run

> fastlane actions # list all available fastlane actions
> fastlane action [action_name] # more information for a specific action
