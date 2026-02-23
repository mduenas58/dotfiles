" Basic Settings
set nocompatible                " Use Vim settings, not Vi
set title                       " Set window title
set encoding=utf-8              " UTF-8 encoding

" Indentation
set expandtab                   " Use spaces instead of tabs
set tabstop=4                   " Tab width = 4 spaces
set softtabstop=4               " Soft tab width
set shiftwidth=4                " Indent width
set smartindent                 " Smart auto-indenting

" Interface
syntax on                       " Syntax highlighting
set number                      " Show line numbers
set ruler                       " Show cursor position
set hlsearch                    " Highlight search results
set incsearch                   " Incremental search
set mouse=a                     " Enable mouse support
set cursorline                  " Highlight current line
set hidden                      " Allow hidden buffers
set splitright                  " Split vertical to right
set splitbelow                  " Split horizontal below

" Disable bells
set belloff=all                 " Turn off all bells
set noerrorbells                " No error bells
set visualbell                  " Use visual bell instead of beeping

" Colors (if terminal supports)
set t_Co=256                    " 256 colors
set termguicolors               " True color support

" Auto-install vim-plug if not installed
if empty(glob('~/.vim/autoload/plug.vim'))
  silent !curl -fLo ~/.vim/autoload/plug.vim --create-dirs
    \ https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
  autocmd VimEnter * PlugInstall --sync | source $MYVIMRC
endif

" Plugin Management
call plug#begin('~/.vim/plugged')

" Plugins
Plug 'scrooloose/nerdtree'          " File explorer
Plug 'vim-airline/vim-airline'      " Status line
Plug 'vim-airline/vim-airline-themes' " Airline themes
Plug 'tpope/vim-fugitive'            " Git integration
Plug 'preservim/nerdcommenter'       " Easy commenting
Plug 'jiangmiao/auto-pairs'          " Auto close brackets
Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }  " Fuzzy finder
Plug 'junegunn/fzf.vim'              " FZF integration

call plug#end()

" Plugin Configurations

" Airline settings
let g:airline_powerline_fonts = 1
let g:airline_theme = 'dark'
let g:airline#extensions#tabline#enabled = 1

" NERDTree settings
nnoremap <C-n> :NERDTreeToggle<CR>
let g:NERDTreeWinSize = 30

" FZF settings
nnoremap <C-p> :Files<CR>
nnoremap <C-g> :GFiles<CR>
nnoremap <C-l> :Lines<CR>

" NERDCommenter settings
let g:NERDSpaceDelims = 1
let g:NERDCompactSexyComs = 1

" Auto-commands
augroup vimrc_autocmds
    autocmd!
    " Remember last cursor position
    autocmd BufReadPost *
        \ if line("'\"") > 0 && line("'\"") <= line("$") |
        \   exe "normal! g`\"" |
        \ endif
augroup END
