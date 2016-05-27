# awesome_bot

Verify links in [awesome](https://github.com/sindresorhus/awesome) projects

![](http://i.giphy.com/urvsFBDfR6N32.gif)

[![Build Status](https://travis-ci.org/dkhamsing/awesome_bot.svg)](https://travis-ci.org/dkhamsing/awesome_bot) [![Tests](https://img.shields.io/badge/tests-circle%20ci-brightgreen.svg)](https://circleci.com/gh/dkhamsing/awesome_bot)
[![Gem Version](https://badge.fury.io/rb/awesome_bot.svg)](https://badge.fury.io/rb/awesome_bot)
[![](https://img.shields.io/badge/awesome-status-brightgreen.svg)](status/status.md)

`awesome_bot` checks for valid URLs in a file, it can be used to [verify pull requests](#validate-pull-requests) updating a README.

## Installation

    $ gem install awesome_bot

## Usage

### Command Line

    awesome_bot <file> [--allow-dupe] [--allow-redirect] [--allow-timeout] [--set-timeout d] [--white-list item1,item2,..]
      file             Path to file, required as first argument
      --allow-dupe     Duplicate URLs are allowed
      --allow-redirect Redirected URLs are allowed
      --allow-timeout  URLs that time out are allowed
      --set-timeout    Set connection timeout (seconds)
      --white-list     Comma separated URLs/domains to white list

By default, `awesome_bot` flags duplicates and URL redirects.

- Use option `--allow-dupe` to allow duplicates.
- Use option `--allow-redirect` to all redirects.
- You can also white list specific links that will not be flagged (for dupe or redirect). `--white-list domain1.com/post/article,domain2.com` white lists `domain1.com/post/article` and all links matching `domain2.com`.

### Examples

```shell
$ awesome_bot README.md
> Checking links in README.md
Links found: 56, 37 unique
  01. https://github.com/sindresorhus/awesome
  02. http://i.giphy.com/urvsFBDfR6N32.gif
  03. https://travis-ci.org/dkhamsing/awesome_bot.svg
# ...
  37. https://github.com/dkhamsing
  Checking URLs: ✓✓✓→?✓→✓→→✓✓→✓✓✓→✓✓✓✓✓✓✓✓✓✓✓→✓✓✓✓✓→✓✓

Issues :-(
> Links
  1. [L007] 301 https://travis-ci.org/dkhamsing/awesome_bot.svg → https://api.travis-ci.org/dkhamsing/awesome_bot.svg
  2. [L008] 302 https://badge.fury.io/rb/awesome_bot → http://rubygems.org/gems/awesome_bot
# ...
> Dupes
  1. [L03] https://github.com/sindresorhus/awesome
  2. [L05] http://i.giphy.com/urvsFBDfR6N32.gif
# ...
```

```shell
$ awesome_bot README.md --allow-dupe --allow-redirect --white-list rubydoc,giphy
> Checking links in README.md
> Will allow redirects
> Will allow duplicate links
> White list links matching: rubydoc, giphy
Links to check: 41, 5 white listed, 29 unique
  01. https://github.com/sindresorhus/awesome
  02. https://travis-ci.org/dkhamsing/awesome_bot.svg
# ...
Checking URLs: ✓✓→✓✓→→→✓✓✓✓✓✓✓✓✓✓✓✓✓✓✓→✓✓✓→✓
Checking white listed URLs: ?✓

> White listed:
  1. [L005] 200 http://i.giphy.com/urvsFBDfR6N32.gif
  2. [L093] 202 http://www.rubydoc.info/gems/awesome_bot
No issues :-)
```

```shell
(master) $ git branch
* master
(master) $ git checkout -b new-branch
Switched to a new branch 'new-branch'
(new-branch) $ touch new-readme.md && echo 'https://github.com/dkhamsing' >> new-readme.md
(new-branch) $ git add new-readme.md
(new-branch) $ git commit -m 'Testing'
[new-branch ef47336] Testing
 1 file changed, 1 insertion(+)
 create mode 100644 new-readme.md
(new-branch) $ git diff master.. --name-only | grep '.md' | xargs awesome_bot
> Checking links in new-readme.md
Links to check: 1
  1. https://github.com/dkhamsing 
Checking URLs: ✓
No issues :-)

Wrote results to ab-results-new-readme.md.json
```

### Library

```ruby
irb(main):001:0> require 'awesome_bot'
=> true
irb(main):002:0> content = File.read 'README.md'
=> "..."
irb(main):003:0> result = AwesomeBot.check content
=> #<AwesomeBot::Result:0x007fdde39f4408 @links=...>
# AwesomeBot Result with success, statuses_issues, dupes and more
irb(main):004:0> puts result.success ? 'No errors' : ':-('
:-(
```

More information at [rubydoc](http://www.rubydoc.info/gems/awesome_bot).

## Validate Pull Requests

Does your GitHub README contain a lot of links? `awesome_bot` can help you validate them when a [pull request](https://github.com/dkhamsing/open-source-ios-apps/pull/159) is created (or a commit is pushed). It is used by:

- https://github.com/tiimgreen/github-cheat-sheet
- https://github.com/vinta/awesome-python
- https://github.com/enaqx/awesome-react
- https://github.com/vsouza/awesome-ios
- https://github.com/alebcay/awesome-shell
- https://github.com/matteocrippa/awesome-swift

and [more](status/status.md).

Tip: Use the keyword `[ci skip]` in your commit title/message to selectively skip verification (if you are let's say working on a bunch of changes).

### Travis CI

To use `awesome_bot` with Travis CI, [connect your repo](https://travis-ci.org/) and create a [`.travis.yml` file](https://github.com/ziadoz/awesome-php/blob/master/.travis.yml).

```yml
language: ruby
rvm: 2.2
before_script: gem install awesome_bot
script: awesome_bot README.md
```

To turn off email notifications, add the lines below

```yml
notifications:
  email: false
```

### Circle CI

If you prefer Circle CI, it'll work too. [Connect your repo](https://circleci.com/) and create a [`circle.yml` file](https://github.com/tmcw/awesome-geojson).

```yml
machine:
  ruby:
    version: 2.2.0
test:
  pre:
    - gem install awesome_bot
  override:
    - awesome_bot README.md
```

### More

Circle CI, [Codeship](https://codeship.com/), and [Semaphore CI](https://semaphoreci.com/) support running tests without adding a file to the repo (a public configuration file can however help others contribute).

```
# Codeship
Setup
rvm use 2.2.0 --install
gem install awesome_bot

Test
awesome_bot README.md
```

```
# Semaphore CI
Language: Ruby
Ruby version: 2.2
Databases for: don't generate
Setup:
gem install awesome_bot
awesome_bot README.md
```

### Status Badge

[![Build Status](https://travis-ci.org/unixorn/awesome-zsh-plugins.png)](https://travis-ci.org/unixorn/awesome-zsh-plugins)

To add the Travis CI build status badge above to your project, use the following code

```
[![Build Status](https://travis-ci.org/<username>/<project>.svg)](https://travis-ci.org/<username>/<project>)

i.e.
[![Build Status](https://travis-ci.org/dkhamsing/awesome_bot.svg?branch=master)](https://travis-ci.org/dkhamsing/awesome_bot)
```

As it happens, the default code snippet provided contain a redirect so adding a badge could fail your status :sob:.. one way to fix this is to white list `travis-ci`, i.e.

```
- awesome_bot README.md --white-list travis-ci
```

You can also add a badge for other CI tools, I recommend checking out [shields.io](http://shields.io/).

## Contact

- [github.com/dkhamsing](https://github.com/dkhamsing)
- [twitter.com/dkhamsing](https://twitter.com/dkhamsing)

## License

This project is available under the MIT license. See the [LICENSE](LICENSE) file for more info.
