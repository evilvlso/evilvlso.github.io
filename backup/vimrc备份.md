> 万古长青的编辑器 **vim**
> 
> 而且X格满满

### vimrc
```
set nocompatible  
set hlsearch
set number  
set history=1000
set background=dark 
syntax on  
set autoindent 
set tabstop=4
set expandtab
set shiftwidth=4

let mapleader=","

" colors
set background=dark
colorscheme hybrid

" jklh
map <C-j> <C-W>j
map <C-k> <C-W>k
map <C-h> <C-W>h
map <C-l> <C-W>l

" vim-plug
call plug#begin('~/.vim/plugged')
Plug 'scrooloose/nerdtree', { 'on':  'NERDTreeToggle' }
Plug 'yggdroot/indentline'
Plug 'python-mode/python-mode', { 'for': 'python', 'branch': 'develop' }
Plug 'majutsushi/tagbar'
Plug 'tpope/vim-commentary'

call plug#end()
" NERDTree
let NERDTreeWinSize=25
map <F9> :NERDTreeToggle<CR>

" indentline
let g:indentline_char = '¦'


" Tagbar
nmap <F8> :TagbarToggle<CR>
let g:tagbar_ctags_bin = "/usr/local/bin/ctags"
let g:tagbar_width=28


" python-mode
let g:pymode_rope = 1
let g:pymode_rope_completion = 1
let g:pymode_rope_complete_on_dot = 1
set completeopt=menuone,noinsert

" let g:pymode_rope_completion_bind = ''
" Documentation
let g:pymode_doc = 0
let g:pymode_doc_key = 'K'
"Linting
let g:pymode_lint = 1
let g:pymode_lint_checker = "pyflakes,pep8"
" let g:pymode_lint_on_write = 1
" Support virtualenv
let g:pymode_virtualenv = 1
" Enable breakpoints plugin
let g:pymode_breakpoint = 1
let g:pymode_breakpoint_bind = '<leader>b'
" syntax highlighting
let g:pymode_syntax = 1
let g:pymode_syntax_all = 1
let g:pymode_syntax_indent_errors = g:pymode_syntax_all
let g:pymode_syntax_space_errors = g:pymode_syntax_all
" Don't autofold code
let g:pymode_folding = 0
let g:pymode_run = 1
let g:pymode_run_bind = '<leader>r'
" find definition
let g:pymode_rope_goto_definition_bind = '<C-c>g'
let g:pymode_rope_goto_definition_cmd = 'new'

```