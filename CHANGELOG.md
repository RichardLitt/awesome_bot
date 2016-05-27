# awesome_bot changelog

Changes by [Daniel Khamsing][] unless otherwise noted.

# 1.10.0

- add `allow-ssl` option, suggested by [Joe Block](https://github.com/unixorn)

# 1.9.1

- [fix] url redirect location encoding, reported by [@hoppfrosch](https://github.com/hoppfrosch)

# 1.9.0

- [cli] support checking multiple files (comma separated or `*` pattern  i.e. `docs/*.md`), suggested by [Sota Yamashita](https://github.com/sotayamashita)
- [cli] use `optparse`

# 1.8.5

- [fix] request errors (make `get` requests), reported by [Richard Littauer](https://github.com/RichardLitt)

# 1.8.4

- [fix] parsing links with colon
- [fix] parsing links separated by comma

# 1.8.3

- restore `head` request option
- rename `net`
- [cli] rename ab-results.json
- [status] yield `headers` (library usage)
- [gem] update `parallel` dependency to `1.8`

# 1.8.2

- [output] add link line number for dupes
- [fix] output line of link default value, reported by [Julien Bisconti][]
- write `json` results file
- isolate and cleanup

# 1.8.1

- [output] show link line number, suggested by [Daniel Gomez Rico](https://github.com/danielgomezrico)
- [output] improve enumeration with padding
- set default open link timeout to 30 seconds

# 1.8.0

- remove `faraday`
- [fix] parse links with commas (url encode), reported by [Kishan Bagaria](https://github.com/KishanBagaria)

# 1.7.1

- [fix] parse issues with links in `adoc` files, reported by [Ibragimov Ruslan](https://github.com/IRus)

# 1.7.0

- [cli] invalid options error
-	[output] improve

# 1.6.0

- [cli] improve argument error
- [output] update status using `x` for 400s error code and `?` for other
- [output] clarify white listing

# 1.5.1

- [fix] link parsing error with markdown badge
- improve code, suggested by [Colby M. White][]

# 1.5.0

- [output] display url redirect location, by [Colby M. White][]
- [output] update logic for number of unique links
- [output] standardize indent
- rename `Result` `rejected` to `links_white_listed`

# 1.4.0

- add `--allow-timeout` and `--set-timeout` options, suggested by [R.I. Pienaar][]

# 1.3.3

- [gemspec] remove uri dependency

# 1.3.2

- [fix] another error with `)` in link parsing, reported by [Julien Bisconti][]

# 1.3.1

- [fix] error with `)` in link parsing, reported by [Halim Qarroum](https://github.com/HQarroum)
- minor improvement to output

# 1.3.0

- add `--allow-redirect` option, suggested by [R.I. Pienaar][]
- output `→` as redirect status indicator
- update error logic in statuses

# 1.2.1

- correct logic for displaying white list status

# 1.2.0

- move some logic from check to cli
- output status for white listed links
- use `result`
- use `logger`

## 1.1.0

- handle bad links
- statuses yields `status`, `url`
- add head option when getting statuses
- [cli] improve output for `--allow-dupe`

## 1.0.0

- correct failure logic
- rename `run` to `check`
- isolate cli
- [cli] simply usage, output version
- [gemspec] update
- [travis] simplify

## 0.1.0

- initial version

## Contact

- [Daniel Khamsing][]

[Daniel Khamsing]:https://github.com/dkhamsing
[Colby M. White]:https://github.com/colbywhite
[Julien Bisconti]:https://github.com/veggiemonk
[R.I. Pienaar]:https://github.com/ripienaar
