# vim-html-js-indent-fix

Somewhere in Vim 8.2, JS embedded in HTML stopped indenting properly.

Indentation changed from this:

```
<script>
  let x = {
  } 
</script>

```

to this:

```
<script>
  let x = {
       } 
</script>
```

To identify the issue, I did a `diff` of the `indent/html.vim` file and identified that the relevant change was that the built-in `indent/html.vim` changed this line around 589 from this:

```
  if b:hi_indent.scripttype == "javascript"
    return GetJavascriptIndent()
  else
```

to this:

```

  if b:hi_indent.scripttype == "javascript"
    return eval(b:hi_js1indent) + GetJavascriptIndent()
  else
```

This restores the original behavior by changing that line only, leaving the other changes in place.

## Install

Use your manager. I use Vundle

```
Plugin 'napcs/vim-html-js-indent-fix'
```


## License

The license VIM uses.

