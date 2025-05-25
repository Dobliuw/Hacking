```lua
return {
  -- Colorscheme
  { "folke/tokyonight.nvim", priority = 1000, config = function() vim.cmd("colorscheme tokyonight") end },
  
  -- Lualine (status bar)
  {
    "nvim-lualine/lualine.nvim",
    dependencies = { "nvim-tree/nvim-web-devicons" },
    config = function()
      require("lualine").setup {
        options = {
          theme = "tokyonight",
          section_separators = "",
          component_separators = "",
        }
      }
    end
  },

  -- File explorer
  {
    "nvim-tree/nvim-tree.lua",
    dependencies = { "nvim-tree/nvim-web-devicons" },
    config = function()
      require("nvim-tree").setup {}
    end,
  }
}
```
