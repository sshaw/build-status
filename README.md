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

To open the CI service's web page click on the mode's lighter or
run `M-x build-status-open`.

### Status Text Properties

Each status has associated text properties. These are configured
via `build-status-color-alist`. By default it contains:

```el
'(("passed"
   ((background-color . "green")))
  ("failed"
   ((background-color . "red")))
  ("running"
   ((background-color . "yellow"))))
```

Each value is a list of text (`face`) properties. Set them as you see fit.

### Supported Services

#### CircleCI

```el
(setq build-status-circle-ci-token "YOUR-TOKEN")
```

The buffer or one of its descendant directories must contain a `circle.yml` file.

#### Travis CI

Pro and Enterprise not supported. Pull requests welcome!

```el
(setq build-status-travis-ci-token "YOUR-TOKEN")
```

The buffer or one of its descendant directories must contain a `.travis.yml` file.

## TODOs

* Status for queued state (maybe)
* Pro and Enterprise TravisCI
* Support for AppVeyor

## See Also

* [jenkins-watch](https://github.com/ataylor284/jenkins-watch)
* [github-notifier](https://github.com/xuchunyang/github-notifier.el)
