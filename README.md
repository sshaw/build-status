# build-status

Minor mode that shows a buffer's build status in the mode line.

**Currently only supports CircleCI with GitHub and maybe Bitbucket; pull requests welcome!**

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

### CircleCI

```el
(setq build-status-circle-ci-token "YOUR-TOKEN")
```

The buffer or one of its descendant directories must contain a `circle.yml` file.

## TODOs

* Status for queued state
* TravisCI (somewhat in progress)
* Other services

## See Also

* [jenkins-watch](https://github.com/ataylor284/jenkins-watch)
* [github-notifier](https://github.com/xuchunyang/github-notifier.el)
