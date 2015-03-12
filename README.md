# mynt-mode
### static done even simpler

Static site generators are all about simplicity - no complicated frameworks, no overhead through dynamically generating the page every time it's requested, and being able to work in your favorite environment for creating and posting content.

So why am I forced to constantly switch between my editor and (at least one) terminal? Until now, I've always fired up two terminals, one with `mynt watch` to generate the site, another one with `mynt serve` to be able to preview my writings. Not to mention having to load the virtualenv first...

There's got to be an easier way. Enter _mynt-mode_.

_mynt-mode_ is a minor mode for everybody's (admit it) favorite editor. Edit, generate and preview without leaving Emacs. Create a new post with frontmatter with a single keybinding. Make static sites as simple as they're supposed to be.

## Dependencies

_mynt-mode_ doesn't depend on anything other than Emacs itself. But if you're using a virtualenv for mynt, you **do** need [virtualenvwrapper.el][3].

## Installation

### Manual
The usual stuff. Drop mynt-mode.el in your load path and add `(require 'mynt-mode)`

### package.el
_mynt-mode_ is (will soon be) available on [MELPA][1]. `M-x package-install<RET>mynt-mode<RET>` to enlightenment!

## Configuration

### Manual
There are four variables that you need to edit. Assuming you have a mynt site living in `~/Sites/mynt`, containing two subdirs for source and production, and using a virtualenv called "mynt" (hey, that pretty much describes me - what a coincidence!), this would look something like this:

```` lisp
(setq mynt-location    "~/Sites/mynt/"
      mynt-source      "source/"
      mynt-destination "production/"
      mynt-venv        "mynt")
````

Also, you don't care about <kbd>C-m</kbd> for newline, and want to use it for _mynt-mode_ instead:
```` lisp
(add-hook 'mynt-mode-hook
          '(lambda ()
             (local-set-key (kbd "C-m g") 'mynt-generate)
             (local-set-key (kbd "C-m w") 'mynt-watch)
             (local-set-key (kbd "C-m s") 'mynt-serve)
             (local-set-key (kbd "C-m p") 'mynt-make-post)))
````

### use-package (Recommended)

Same scenario as above. As a bonus, this also makes sure that _mynt-mode_ is installed, so you don't have to do that manually!

```` lisp
(use-package mynt-mode
  :ensure t
  :bind (("C-m g" . mynt-generate)
         ("C-m w" . mynt-watch)
         ("C-m s" . mynt-serve)
         ("C-m p" . mynt-make-post))
  :config (setq mynt-location "~/Sites/crshd.github.io/"
                mynt-source "io.source/"
                mynt-destination "io.production/"
                mynt-venv "mynt"))
````

_(Author's note: You (really, **really**) should use [use-package][2]._

## TODO

- The async process management is shit. Basically it's non-existent.
- Support switching between multiple mynt installs.
- Submit your ideas.

[1]: http://melpa.org
[2]: https://github.com/jwiegley/use-package "You really should"
[3]: https://github.com/porterjamesj/virtualenvwrapper.el
