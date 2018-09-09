# VimWorkspace

If you are an experienced Vim user, you might got tired of `bn/bp/ls/Ctrl-^`. If
you are new to the Vim world, then welcome, and start by learning Vim's
notions of [buffers, windows](http://vimdoc.sourceforge.net/htmldoc/windows.html)
and [tabpages](http://vimdoc.sourceforge.net/htmldoc/tabpage.html).

VimWorkspace brings the IDE-like tabs into Vim, for easy navigation, and a nice,
customizable look. It takes your buffers and tabs, and shows them combined in the
tabline. With this you always have your list of buffers visible, at the same
time not losing visibility into tabs. Moreover, VimWorkspace provides handy
commands to boost navigation as well as a list of options to customize how the
tabline appears.

## Introduction

<h3 align="center">
    <img
        src="https://raw.githubusercontent.com/bagrat/vim-workspace/60fadaeee65368f7d2d0a62b4dc452bf9ca99113/demo.jpg"i
        alt="VimWorkspace Screenshot"
    />
</h3>

Take a look at the screenshot. The blue cuties are the tabpages. The tabpage
that has the buffers list coming next, is the current tabpage. The gray items
with names are the hidden/inactive buffers, and obviously, the green one is the
current buffer. The gray items on both ends with the little arrows and numbers
are the truncation indicators. If all the buffers do not fit the screen,
VimWorkflow truncates the tabline, and shows the number of truncated buffers on
both ends.

*Note: the instance of vim in the screenshot is configured to use powerline
symbols and dev-icons. The default interface is only text and will work without
requiring any patched fonts. The default interface looks like in the screenshot
below.*

<h3 align="center">
    <img
        src="https://raw.githubusercontent.com/bagrat/vim-workspace/47741bfed48fe73b1ebcf2653e6be60379477c53/demo2.jpg"i
        alt="VimWorkspace Screenshot"
    />
</h3>

## Installation

Use your favourite plugin manager to install VimWorkspace. If you do not have any
preference or have not decided yet, I would recommend [Plug](https://github.com/junegunn/vim-plug).

```
Plug 'bagrat/vim-workspace'
```

After installation, VimWorkspace is enabled by default, so whenever you restart
Vim, you will see the new tabline!

## Commands

As already mentioned, VimWorkflow provides a set of commands to easily navigate
through your buffers. You might wonder, how would some commands replace `:bn`
and `:bp`. The answer is, that if you are using some other plugins, that add
their buffers to your buffer list, you might not want to be switched to
those, while navigating through your list. VimWorkflow does this for you, and
also provides options to extend the list of buffers to be ignored.

* `WSNext` - switch to the buffer to the right of current one.
* `WSPrev` - switch to the buffer to the left of current one.
* `WSClose[!]` -  close the current buffer. If is has unsaved changes, an error
  will be shown, and the buffer will stay open. To ignore any changes and
  forcibly close the buffer, use `WSClose!`.
* `WSTabNew` - create a new tab. This uses the current buffer to load into the
  new tab's window, to avoid having a new empty buffer created. This is
  basically an equivalent of `tabedit <current-buffer>`.
* `WSBufOnly[!]` - close all the buffers but the current. If there is any buffer
  in the list that has unsaved changes, this command stops there and shows an
  error. To ignore any changes and forcibly close all buffers (except the
  current one), use `WSBufOnly!`.

## Configuration

There are some configuration options that make it possible to customize how the
tabline works and looks like.

### Options

The following is the list of available options, that should be set in your
vimrc file, using `let <optiona-name> = <option-value>`:

* `g:workspace_hide_buffers` - a list of buffer names to ignore. The name should
  match exactly. This option does not provide much power. For a more general
  configuration see the next option.

  Default:
  ```
  let g:workspace_hide_buffers = []
  ```

* `g:workspace_hide_ft_buffers` - a list of `filetype`s to ignore.

  Default:
  ```
  let g:workspace_hide_ft_buffers = ['qf']
  ```

* `g:workspace_hide_terms` - don't show terminal windows in the tabline

  Default:
  ```
  let g:workspace_hide_terms = 0
  ```

* `g:workspace_powerline_separators` - if set to `1`, use powerline separators
  in between buffers and tabs in the tabline. This is a shortcut, so that you do
  not have to configure the separators individually.

  Default:
  ```
  let g:workspace_powerline_separators = 0
  ```

* `g:workspace_separator` - the character to be used for separating items with
  different background colors in the tabline.

  Default:
  ```
  let g:workspace_separator = ""
  ```

* `g:workspace_subseparator` - the character to be used for separating items that
  have the same background colors in the tabline.

  Default:
  ```
  let g:workspace_subseparator = "|"
  ```

* `g:workspace_use_devicons` - if set to `1` and
  [`vim-devicons`](https://github.com/ryanoasis/vim-devicons) plugin is
  installed, show file type icons for each buffer in the tabline. If the
  `vim-devicons` plugin is not present, the option will automatically be set to
  `0`.

  Default:
  ```
  let g:workspace_use_devicons = 1
  ```

* `g:workspace_tab_icon` - the character to be used as an icon for the tab items
  in the tabline.

  Default:
  ```
  let g:workspace_tab_icon = "#"
  ```

* `g:workspace_new_buffer_name` - the character to be shown as the name of a new
  buffer.

  Default:
  ```
  let g:workspace_new_buffer_name = "*"
  ```

* `g:workspace_new_buffer_name` - the character to be shown by the name of
  a modified buffer.
  Default:

  ```
  let g:workspace_modified_icon = "+"
  ```

* `g:workspace_left_trun_icon` - the character to be shown by the count of
  truncated buffers on the left.

  Default:
  ```
  let g:workspace_left_trunc_icon = "<"
  ```

* `g:workspace_right_trun_icon` - the character to be shown by the count of
  truncated buffers on the right.
  
  Default:
  ```
  let g:workspace_right_trunc_icon = ">"
  ```

### Colors

Of course, you can customize the colors of your tabline, to make it awesome and
yours. The following is the list of highlight groups, with self-explanatory
names:

* `WorkspaceBufferCurrent` - the current buffer.
* `WorkspaceBufferActive` - an active buffer (a non-current buffer visible in
  a non-current window).
* `WorkspaceBufferHidden` - a non-current buffer.
* `WorkspaceBufferTrunc` - the truncation indicators (count of truncated buffers
  from the left or right).
* `WorkspaceTabCurrent` - the current tab.
* `WorkspaceTabHidden` - a non-current tab.
* `WorkspaceFill` - the blank space left on the right of the tabline.

To get your custom colors set, define a function with name
`g:WorkspaceSetCustomColors` and place your highlight group definitions inside
the function. Make sure the function is defined before `VimWorkspace` is loaded

## Recommendations and FAQ

Here are some recommended mappings to boost your navigation experience:

```
noremap <Tab> :WSNext<CR>
noremap <S-Tab> :WSPrev<CR>
noremap <Leader><Tab> :WSClose<CR>
noremap <Leader><S-Tab> :WSClose!<CR>
noremap <C-t> :WSTabNew<CR>

cabbrev bonly WSBufOnly
```

### FAQ

#### **How do I get the look like in the screenshot?**

First you will need a patched font, extended with `powerline` and `font-awesome`
symbols. Also, you will need the
[`vim-devicons`](https://github.com/ryanoasis/vim-devicons) installed, which
also has great guides on how to patch fonts, as well as some pre-patched fonts.
As soon as you have the patched font, setting the following options, will give
you exactly the same tabline as you see in the demo gif:

```
let g:workspace_powerline_separators = 1
let g:workspace_tab_icon = "\uf00a"
let g:workspace_left_trunc_icon = "\uf0a8"
let g:workspace_right_trunc_icon = "\uf0a9"
```

## License

See
[LICENSE](https://github.com/bagrat/vim-workspace/blob/master/LICENS://github.com/bagrat/vim-workspace/blob/master/LICENSE).
