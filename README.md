# build-status

Emacs minor mode that shows a buffer's build status in the mode line.

![build-status example passing](example1.png)

![build-status example failing](example2.png)

## Usage

`M-x build-status-mode` in a buffer that's part of a CI project.

By default the build status will be checked every 5 minutes. To change this
set `build-status-check-interval` to the desired interval, in seconds.

API tokens can be set via the service-specific variable (see below) or via `git config`:

```
git config --add build-status.api-token TOKEN
```

To open the CI service's web page for buffer's build click on the mode's lighter or
run `M-x build-status-open`.

## Status Mapping

`build-status` will try to convert the CI service's status to one of the following:

* failed
* passed
* queued
* running

This is done via the service's status mapping alist.

If the status is not mapped it's treated as unknown (lighter is `"?"` and mouseover shows
the status as is). You can ignore a status by mapping it to the symbol `ignored`.

See the [Supported Services section](#supported-services) below for more information.

## Status Mode Line Faces

Each status indicator has an associated face. They're are listed below.

If you'd like to change the color and/or style of an indicator just
[update the appropriate face](https://www.gnu.org/software/emacs/manual/html_node/elisp/Attribute-Functions.html#Attribute-Functions).

### `build-status-face`

All faces inherit from this face.

Attributes: none

### `build-status-failed-face`

Attributes: `:background "red"`

### `build-status-passed-face`

Attributes: `:background "green"`

### `build-status-queued-face`

Attributes: `:background "yellow"`

### `build-status-running-face`

Attributes: `:background "yellow"`

### `build-status-unknown-face`

Used when the build status returns an unknown value. For more info see [status mapping](#status-mapping).

Attributes: none

## Supported Services

### CircleCI

The buffer's directory or one of its ancestors must contain a `circle.yml` file.

To set a token (but also see [`git config` tokens](#usage)):

```el
(setq build-status-circle-ci-token "YOUR-TOKEN")
```

Status mapping is controlled via `build-status-circle-ci-status-mapping-alist`. It
defaults to:

```el
'(("infrastructure_fail" . "failed")
  ("not_running" . "queued")
  ("success" . "passed")
  ("scheduled" . "queued")
  ("timedout" . "failed"))
```

### Travis CI

**Pro and Enterprise not supported. Pull requests welcome!**

The buffer's directory or one of its ancestors must contain a `.travis.yml` file.

To set a token (but also see [`git config` tokens](#usage)):

```el
(setq build-status-travis-ci-token "YOUR-TOKEN")
```

Status mapping is controlled via `build-status-travis-ci-status-mapping-alist`. It
defaults to:

```el
'(("errored" . "failed")
  ("started" . "running")
  ("created" . "queued"))
```

## TODOs

* Support for Enterprise GitHub
* Support for TravisCI Pro and Enterprise
* Support for VCS mode hooks
* Support for AppVeyor

## See Also

* [jenkins-watch](https://github.com/ataylor284/jenkins-watch)
* [github-notifier](https://github.com/xuchunyang/github-notifier.el)

## Author

Skye Shaw [skye.shaw AT gmail.com]
