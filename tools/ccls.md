# ccls
`ccls` 是一个 c++ 的 `lsp` 实现, 需要从源码来编译，注意需要依赖 `libclang-dev`。编译后会获得一个 `ccls` 的可执行文件，放到 path 路径下即可。

# ccls in vim
推荐使用 `coc.nvim`, 装好插件以后，需要运行 `:CocConfig` 来进行配置。
## coc.nvim 配置
`coc.nvim` 支持多种语言的 `lsp`, 这里只需配置c/c++的即可：
```json
{
  "languageserver": {
    "ccls": {
      "command": "ccls",
      "filetypes": ["c", "cpp", "cuda", "objc", "objcpp"],
      "rootPatterns": [".ccls-root", "compile_commands.json"],
      "initializationOptions": {
        "cache": {
          "directory": ".ccls-cache"
        },
        "client": {
          "snippetSupport": true
        }
      }
    }
  }
}
```
在 coc.vim 的github 上提供了一个配置文件，想偷懒可以直接全用这个配置。
+ `C+p` `C+n` 可以用来上下选择补全文本，然后按 `Enter` 进行补全
+ `gd` 可以跳转到声明，`gi` 跳转到实现。跳转之后用`C+o` 来返回

# c++ 项目配置
有两种配置方式：
+ 使用 `.ccls` 文件，配置较简单，需要手写来实现
+ 使用 `compile_commands.json` 可以通过 `makefile` 或 `cmake` 文件来自动生成

在使用 cmake 来生成项目时，添加 `-DCMAKE_EXPORT_COMPILE_COMMANDS=YES` 就会自动生成 `compile_commands.json` 文件，注意要把它放到项目的根目录下。