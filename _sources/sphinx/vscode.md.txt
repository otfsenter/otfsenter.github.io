# vscode

## start vscode on windows

```
D:\VSCode\Code.exe --disable-gpu --no-sandbox
```


## extensions: paste images

Paste Image: Path

```
${currentFileDir}/assets/${currentFileNameWithoutExt}
```

## prince xml font settings

reference url

https://github.com/shd101wyy/markdown-preview-enhanced/blob/master/docs/customize-css.md

To customize css for your markdown file, `cmd-shift-p` then run `Markdown Preview Enhanced: Customize Css` command.

The style.less file will open, and you can override existing style like this:

> `style.less` file is located at `~/.mume/style.less`

```

.markdown-preview.markdown-preview {

  // custom prince pdf export style
  &.prince {
    font-family: "Times New Roman", "PingFang SC";
  }

```
