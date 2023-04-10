---
title: "My Neovim configuration"

description: "How I like my code editing experience"
featured_image: "/nvim.jpg"
---

Plugins
-------

First, get pathogen, the vim plugin manager by Tpope.

```bash
mkdir -p ~/.config/nvim/autoload ~/.config/nvim/bundle && \
curl -LSso ~/.config/nvim/autoload/pathogen.vim https://tpo.pe/pathogen.vim
```

Clone all the plugins into the bundle folder: (WIP)
[plugins.sh](/plugins.sh)


init.vim
---------

Yes, this file is quite a mess.

```vim
let mapleader =" "

"Use 24-bit (true-color) mode in Vim/Neovim when outside tmux.
"If you're using tmux version 2.2 or later, you can remove the outermost $TMUX check and use tmux's 24-bit color support
"(see < http://sunaku.github.io/tmux-24bit-color.html#usage > for more information.)
  if (has("nvim"))
    "For Neovim 0.1.3 and 0.1.4 < https://github.com/neovim/neovim/pull/2198 >
    let $NVIM_TUI_ENABLE_TRUE_COLOR=1
  endif
  "For Neovim > 0.1.5 and Vim > patch 7.4.1799 < https://github.com/vim/vim/commit/61be73bb0f965a895bfb064ea3e55476ac175162 >
  "Based on Vim patch 7.4.1770 (`guicolors` option) < https://github.com/vim/vim/commit/8a633e3427b47286869aa4b96f2bfc1fe65b25cd >
  " < https://github.com/neovim/neovim/wiki/Following-HEAD#20160511 >
  if (has("termguicolors"))
    set termguicolors
  endif


execute pathogen#infect()
syntax on
filetype plugin indent on


set tabstop=8 softtabstop=0 expandtab shiftwidth=2 smarttab

filetype plugin on
set number relativenumber

set guifont=Source\ Code\ Pro:h11

augroup filetype_javascript
  autocmd!
  autocmd FileType javascript imap ;l console.log("");<Esc>hhi
  autocmd FileType javascript vmap ;l yoconsole.log();<Esc>hhp
augroup END

let g:gitgutter_map_keys = 0

let g:neovide_transparency=0.95
let g:transparency = 0.95
let g:neovide_refresh_rate= 120
let g:neovide_scroll_animation_length = 0.3
let g:neovide_background_color = '#05112e'.printf('%x', float2nr(255 * g:transparency))
let g:neovide_cursor_trail_size = 0
let g:neovide_cursor_vfx_mode = "pixiedust"
let g:neovide_hide_mouse_when_typing = v:true
let g:neovide_cursor_antialiasing = v:true
let g:neovide_cursor_animate_in_insert_mode = v:true

set background=dark


nmap <C-p> :Files<CR>
nmap <leader>p :Ag<CR>

nmap ghs <Plug>(GitGutterStageHunk)
nmap ghu <Plug>(GitGutterUndoHunk)
nmap gh? <Plug>(GitGutterPreviewHunk)

nmap ghn <Plug>(GitGutterNextHunk)
nmap ghp <Plug>(GitGutterPrevHunk)

map <leader><leader> <Esc>/<?><Enter>d3l
map <leader>/ i<?><Esc>

map <silent> e <Plug>CamelCaseMotion_w

map <leader>t :!ctags -R<CR><CR>

" latex stuf
let g:livepreview_previewer = 'zathura'
" map <leader>8 0y$i\begin{<Esc>A}<Enter><Esc>p0i\end{<Esc>A}<Esc>kA<Enter>

nmap <silent> gd <Plug>(coc-definition)
nmap <silent> gs :call CocAction('jumpDefinition', 'vsplit')<CR>
nmap <silent> gt :call CocAction('jumpDefinition', 'tabe')<CR>
nmap <silent> gy <Plug>(coc-type-definition)
nmap <silent> gi <Plug>(coc-implementation)
nmap <silent> gr <Plug>(coc-references)

map <C-f> :NERDTreeToggle<CR>
map <C-k> :wincmd k<CR>
map <C-j> :wincmd j<CR>
map <C-h> :wincmd h<CR>
map <C-l> :wincmd l<CR>
map <C-x> :wincmd x<CR>
map <leader>h :tabp<CR>
map <leader>l :tabn<CR>
map L $
map H 0

" Some servers have issues with backup files, see #649.
set nobackup
set nowritebackup

" Having longer updatetime (default is 4000 ms = 4 s) leads to noticeable
" delays and poor user experience.
set updatetime=300

" Always show the signcolumn, otherwise it would shift the text each time
" diagnostics appear/become resolved.
set signcolumn=yes

" Use tab for trigger completion with characters ahead and navigate.
" NOTE: There's always complete item selected by default, you may want to enable
" no select by `"suggest.noselect": true` in your configuration file.
" NOTE: Use command ':verbose imap <tab>' to make sure tab is not mapped by
" other plugin before putting this into your config.
inoremap <silent><expr> <TAB>
      \ coc#pum#visible() ? coc#pum#next(1) :
      \ CheckBackspace() ? "\<Tab>" :
      \ coc#refresh()
inoremap <expr><S-TAB> coc#pum#visible() ? coc#pum#prev(1) : "\<C-h>"

" Make <CR> to accept selected completion item or notify coc.nvim to format
" <C-g>u breaks current undo, please make your own choice.
inoremap <silent><expr> <CR> coc#pum#visible() ? coc#pum#confirm()
                              \: "\<C-g>u\<CR>\<c-r>=coc#on_enter()\<CR>"

function! CheckBackspace() abort
  let col = col('.') - 1
  return !col || getline('.')[col - 1]  =~# '\s'
endfunction


:lua << EOF
require'nvim-treesitter.configs'.setup {
  -- A list of parser names, or "all" (the five listed parsers should always be installed)
  ensure_installed = { "c", "lua", "vim", "vimdoc", "query", "javascript", "typescript", "rust" },

  -- Install parsers synchronously (only applied to `ensure_installed`)
  sync_install = false,

  -- Automatically install missing parsers when entering buffer
  -- Recommendation: set to false if you don't have `tree-sitter` CLI installed locally
  auto_install = true,

  highlight = {
    enable = true,

    disable = {"markdown"},

    -- Setting this to true will run `:h syntax` and tree-sitter at the same time.
    -- Set this to `true` if you depend on 'syntax' being enabled (like for indentation).
    -- Using this option may slow down your editor, and you may see some duplicate highlights.
    -- Instead of true it can also be a list of languages
    additional_vim_regex_highlighting = false,
  },
}
EOF


:lua << EOF
require('rose-pine').setup({
	--- @usage 'auto'|'main'|'moon'|'dawn'
	variant = 'auto',
	--- @usage 'main'|'moon'|'dawn'
	dark_variant = 'main',
	bold_vert_split = false,
	dim_nc_background = false,
	disable_background = false,
	disable_float_background = false,
	disable_italics = false,

	--- @usage string hex value or named color from rosepinetheme.com/palette
	groups = {
		background = 'base',
		background_nc = '_experimental_nc',
		panel = 'surface',
		panel_nc = 'base',
		border = 'highlight_med',
		comment = 'muted',
		link = 'iris',
		punctuation = 'subtle',

		error = 'love',
		hint = 'iris',
		info = 'foam',
		warn = 'gold',

		headings = {
			h1 = 'iris',
			h2 = 'foam',
			h3 = 'rose',
			h4 = 'gold',
			h5 = 'pine',
			h6 = 'foam',
		}
		-- or set all headings at once
		-- headings = 'subtle'
	},

	-- Change specific vim highlight groups
	-- https://github.com/rose-pine/neovim/wiki/Recipes
	highlight_groups = {
		ColorColumn = { bg = 'rose' },

		-- Blend colours against the "base" background
		CursorLine = { bg = 'foam', blend = 10 },
		StatusLine = { fg = 'love', bg = 'love', blend = 10 },
	}
})
EOF

syntax enable
colorscheme rose-pine
hi Normal     ctermbg=NONE guibg=NONE
hi LineNr     ctermbg=NONE guibg=NONE
hi SignColumn ctermbg=NONE guibg=NONE
" hi StatusLine ctermbg=0F202C guibg=#0F202C
" hi StatusLineNC ctermbg=NONE guibg=NONE
hi ErrorMsg ctermbg=NONE guibg=NONE
hi TabLine ctermbg=NONE guibg=NONE
hi TabLineSel ctermbg=NONE guibg=NONE
hi TabLineFill ctermbg=NONE guibg=NONE

" let g:solarized_visibility="high"
" let g:solarized_diffmode="high"
set background=dark
```
