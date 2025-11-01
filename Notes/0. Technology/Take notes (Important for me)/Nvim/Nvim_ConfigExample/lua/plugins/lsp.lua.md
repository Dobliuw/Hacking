```lua
-- plugins/lsp.lua

return {
  -- 🔧 Mason: gestor de LSPs/DAPs
  {
    "williamboman/mason.nvim",
    config = function()
      require("mason").setup()
    end,
  },

  -- 🔧 Mason-LSPConfig + LSPConfig
  {
    "williamboman/mason-lspconfig.nvim",
    dependencies = {
      "neovim/nvim-lspconfig",
      "hrsh7th/cmp-nvim-lsp",
    },
    config = function()
      local mason_lspconfig = require("mason-lspconfig")
      local lspconfig = require("lspconfig")
      local capabilities = require("cmp_nvim_lsp").default_capabilities()

      mason_lspconfig.setup({
        ensure_installed = {
          "pyright",
          "ts_ls",
          "clangd",
          "cssls",
          "html",
          "bashls",
        },
        automatic_installation = true,
      })

      -- Setup manual de cada LSP
      local servers = {
        "pyright",
        "ts_ls",
        "clangd",
        "cssls",
        "html",
        "bashls",
      }

      for _, server in ipairs(servers) do
        lspconfig[server].setup({
          capabilities = capabilities,
        })
      end
    end,
  },

  -- 🔠 Autocompletado
  {
    "hrsh7th/nvim-cmp",
    dependencies = {
      "hrsh7th/cmp-nvim-lsp",
      "L3MON4D3/LuaSnip",
    },
    config = function()
      local cmp = require("cmp")
      cmp.setup({
        snippet = {
          expand = function(args)
            require("luasnip").lsp_expand(args.body)
          end,
        },
        mapping = cmp.mapping.preset.insert({
          ['<C-Space>'] = cmp.mapping.complete(),
          ['<CR>'] = cmp.mapping.confirm({ select = true }),
        }),
        sources = {
          { name = "nvim_lsp" },
          { name = "luasnip" },
        },
      })
    end,
  },
}


```
