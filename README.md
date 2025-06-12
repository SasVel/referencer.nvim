# referencer.nvim

`referencer.nvim` is a lightweight, asynchronous Neovim plugin written in Lua that uses the built-in LSP to show the number of references to functions, methods, types, or other symbols directly in the buffer using virtual text.

This is especially useful for quickly understanding code usage without manually invoking LSP commands.

---

## Features

- ✨ **Asynchronous**: non-blocking usage count queries using built-in LSP.
- 👁️ Displays number of references next to functions, methods, structs, etc.
- ⚖️ Fully configurable highlight groups and colors.
- 💪 Works with any LSP that supports `textDocument/references` and `textDocument/documentSymbol`.
- ⚖️ On-demand or auto-triggered via `LspAttach` event.

---

## Installation

With [lazy.nvim](https://github.com/folke/lazy.nvim):

```lua
{
    "your-username/referencer.nvim",
    config = function()
        require("referencer").setup()
    end
}
```

With [packer.nvim](https://github.com/wbthomason/packer.nvim):

```lua
use {
    "your-username/referencer.nvim",
    config = function()
        require("referencer").setup()
    end
}
```

---

## Configuration

```lua
require("referencer").setup({
    enable = true, -- enable on startup
    format = "  %d reference(s)", -- format string for reference count
    show_no_reference = true, -- show if refs count = 0
    kinds = { 12, 6, 5, 23, 8 }, -- LSP SymbolKinds to show references for
    hl_group = "Comment", -- default highlight group
    color = "#FFA500", -- optional custom color (overrides hl_group)
    virt_text_pos = "eol", -- virtual text position (eol | overlay | right_align)
    pattern = "*.go", -- pattern for LspAttach autocmd to auto-enable
})
```

### `kinds`

A list of LSP `SymbolKind` numeric values. Some common kinds:

- `5` = Method
- `6` = Function
- `8` = Struct
- `12` = Variable
- `23` = Interface

Full list: [LSP Specification - SymbolKind](https://microsoft.github.io/language-server-protocol/specifications/specification-current/#symbolkind)

---

## Commands

| Command             | Description                         |
| ------------------- | ----------------------------------- |
| `:ReferencerToggle` | Toggle reference display on/off         |
| `:ReferencerUpdate` | Force refresh reference information in current buffer  |

---

## Notes

- ⚡ The plugin is **asynchronous**, so it won’t block your UI while fetching references.
- ✅ Compatible with most major LSPs (gopls, tsserver, etc.).
- ⚠ Only the first attached LSP client is used for requests.

