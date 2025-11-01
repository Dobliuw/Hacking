```lua
return {
  -- Code Intelligence
  {
    "nvim-treesitter/nvim-treesitter",
    build = ":TSUpdate",
    config = function()
      require("nvim-treesitter.configs").setup {
        ensure_installed = { "c", "lua", "bash", "python" },
        highlight = { enable = true },
        indent = { enable = true },
      }
    end
  },

  -- Autocomplete
  {
    "windwp/nvim-autopairs",
    event = "InsertEnter",
    config = function() require("nvim-autopairs").setup {} end
  }
}
```
