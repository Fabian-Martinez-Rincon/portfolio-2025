---
title: 'Instalar NVIM'
published: 2022-10-04
description: ''
category: Linux
# url: '/posts/vim.jpg'
#https://docs.astro.build/assets/arc.webp
---

# Indice

- [Configuramos nuestro editor](#configuramos-nuestro-editor)
- [Modos de Uso]()
    - [Modo Normal](#modo-normal)
    - [Modo Insert](#modo-insert-i-a-o-insert)
    - [Modo Comandos](#modo-comandos-esc)


---

## Configuramos nuestro editor

Resultado Final

![image](https://user-images.githubusercontent.com/55964635/194474898-97cf049c-94c3-4e05-821f-11612f3da941.png)

## Pasos para la instalación

Actualizamos el apt
```powershell
sudo apt-get update
```
Ahora podemos installar neovim
```powershell
sudo apt-get -y install neovim
```
Nos metemos en config
```powershell
cd .config/
```
Chequeamos que tengamos la carpeta **nvim**
```powershell
ls -la
```
En caso de no tenerla, la creamos
```powershell
mkdir nvim
```
Accedemos a la carpeta creada
```shell
cd vim
```
Creamos el archivo init.vim que es el que contendra toda la configuración de nuestro ide
```shell
touch init.vim
```
Creamos una carpeta en donde van a estar nuestras configuraciones
```shell
mkdir general
```
Accedemos a la carpeta
```shell
cd general
```
Y creamos nuestro archivo de configuración
```shell
touch settings.vim
```

Dentro de este, pegamos lo siguiente (Ctrl + Shift + v)
```shell
synta enable
set t_Co=256
set encoding=utf-8
set hidden
set number
set title
set mouse=a
set nowrap
set cursorline
set tabstop=2
set shiftwidth=2
set softtabstop=2
set shiftround
set expandtab
set ignorecase
set smartcase
set spelllang=en,es
set termguicolors
set background=dark
set noshowmode
set clipboard=unnamed
set numberwidth=1
set showcmd
set ruler
set showmatch
" set relativenumber

" Theme Gruvbox
colorscheme gruvbox
let g:gruvbox_contrast = 'hard'
let g:gruvbox_termcolors = 256
highlight Normal ctermbg=NONE
```

Ahora nos metemos en el archivo init.vim y copiamos lo siguiente, para poder hacer referencia a nuestro archivo

```shell
source $HOME/.config/nvim/general/settings.vim
```

Instalamos vim plug

```shell
curl -fLo "${XDG_DATA_HOME:-$HOME/.config}"/nvim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

En nvim, creamos la carpeta vim-plug, dentro le metemos el archivo plugins.vim

```shell
mkdir vim-plug
cd vim-plug
touch plugins.vim
```

Dentro de este archivo, pegamos la siguiente configuración

```vim
" auto-install vim-plug
if empty(glob('~/.config/nvim/autoload/plug.vim'))
  silent !curl -fLo ~/.config/nvim/autoload/plug.vim --create-dirs
    \ https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
  "autocmd VimEnter * PlugInstall
  "autocmd VimEnter * PlugInstall | source $MYVIMRC
endif

call plug#begin('~/.config/nvim/autoload/plugged')

    " Better Syntax Support
    Plug 'sheerun/vim-polyglot'
    " File Explorer
    Plug 'scrooloose/NERDTree'
    " Auto pairs for '(' '[' '{'
    Plug 'jiangmiao/auto-pairs'
    " Gruvbox theme
    Plug 'morhetz/gruvbox'   
    Plug 'godlygeek/csapprox'

  	Plug 'powerline/powerline'    

    Plug 'easymotion/vim-easymotion'
    Plug 'christoomey/vim-tmux-navigator'
    " Airline
    Plug 'vim-airline/vim-airline'
    Plug 'vim-airline/vim-airline-themes'
    
    Plug 'mhartington/oceanic-next'
call plug#end()
```

Ahora en el archivo init.vim, pegamos lo siguiente (arriba de todo)

```shell
source $HOME/.config/nvim/vim-plug/plugins.vim
```

Ahora entramos a nvim, entramos en modo comando con escape y luego los dos puntos y escribimos lo siguiente

```
:PlugInstall
```

Salimos con **:q**


Creamos la carpetas en la que tendremos los temasd (la carpeta estara dentro de .config/nvim)

```shell
mkdir themes
cd themes
touch airline.vim
nvim airline.vim
```

Y dentro de este, pegamos lo siguiente:

```shell
" enable tabline
let g:airline#extensions#tabline#enabled = 0
" let g:airline#extensions#tabline#left_sep = ''
" let g:airline#extensions#tabline#left_alt_sep = ''
" let g:airline#extensions#tabline#right_sep = ''
" let g:airline#extensions#tabline#right_alt_sep = ''

" enable powerline fonts
let g:airline_powerline_fonts = 1
let g:powerline_pycmd = 'py3'
" let g:airline_left_sep = ''
" let g:airline_right_sep = ''

" Switch to your current theme
let g:airline_theme = 'gruvbox'

" Always show tabs
set showtabline=2
```

Ahora en init tenemos que agregar lo siguiente

```shell
source $HOME/.config/nvim/themes/airline.vim
```

Agregon algunos atajos (esto es opcional)

```shell
mkdir keys
cd keys
touch mappings.vim
nvim mappings.vim
```
Y pegamos

```vim
nnoremap <C-n> :NERDTreeToggle<CR>
nmap <Leader>s <Plug>(easymotion-s2)

nmap <C-s> :w<CR>
nmap <C-q> :q<CR>
```

Agregamos el ultimo a init.vim

```shell
source $HOME/.config/nvim/keys/mappings.vim
```

<br>

---

## Modo normal

- Por defecto no podemos escribir, solo nos permite movernos con la j/k/l/h
- `dd` corta una linea
- `d(cantidad de lineas)` corto n lineas
- `yy` copia una linea
- `y(cantidad de lineas)y` copia n lineas
-  `p` pegamos la linea
- `u` Retroseder en los cambios
- `Ctrl + r` Rehacer

<br>

## Modo Insert (entramos con la i)

- Se utiliza para modificar el codigo
-  `i, a o insert` 

<br>

## Modo visual (entramos con la v)

- Sirve para copiar y pegar de forma mas comoda (con el mause)
- `d` cortar
- `y` copiar
- `p` pegar

<br>

## Modo comandos (`esc + :`)

- `esc` Para salir del modo insertar usamos 
, Cuando salimos, podemos mandarle parametros con `:`.
- `q` para salir del archivo sin guardar
- `q!` sale del archivo directamente y no pregunta
- `w` solo guarda
- `wq!/x!` sale y guarda
- `set nu` agrega numeros en la consola
- `set background=dark `
- `Ctrl + v/d` pegar

<br>

### Links de ayuda
- [Instalar debian 11](https://www.youtube.com/watch?v=6PTjoSBdjok)
- [Copiar y Pegar entre la virtual box y nuestro Sistema Operativo](https://www.nociones.de/como-activar-el-copiar-y-pegar-en-virtual-box/#:~:text=Para%20activarlo%2C%20tenemos%20que%20ir,la%20m%C3%A1quina%20virtual%20y%20viceversa.)
- [Video de ayuda para preparar el blog](https://www.youtube.com/watch?v=6sdw6G78Jd0)
- [CheatSheet](https://vim.rtorr.com/lang/es_es)

---

### Comandos basicos

Para introducir datos presionamos `i` y para salir `esc`

- **Es equivalente al Ctrl + Z**: Alt + U
- **Eliminar Palabra** Ctrl + W
- **Borrar toda una linea** DD

Si queremos copiar y pegar muchas cosas hacemos 
- `esc` + `v` y seleccionamos,
  - Copiar `y`
  - Cortar `d`
  - Pegar `p`
- `Repetir la accion anterior`: `esc` + `.`
- Grabar accion `q` + `nombre de la accion` + d w para cortar por ejemplo ``+ `q` //no funca
- **Modo busqueda**: `esc` + `/` + `palabra a buscar`
- **Reemplazar**: `esc` + `:%s/palabra a buscar/palabra a reemplazar/g`