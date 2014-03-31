Vim使用点滴


~/.vimrc
```bash
#鼠标可用
set mouse=a
```


Vim环境和Shell环境切换
1. `Ctrl-z`切换到shell，`fg`返回Vim
2. `:sh`切换到shell，`exit`返回Vim


执行外部命令`:!`
命令历史`q:`

退出所有窗口`:qa`

复制`"1y`(其中1表示剪贴板的号码，0、1、2、3、4、5、6、7、8、9、a是vim的缓存区剪贴板号，+是系统剪贴板号)
粘帖`"1p`


ctags插件
`Ctrl+]`跳到标签定义处


jumplist
`Ctrl+O`向前，`Ctrl+I`向后

##vim插件

###插件安装方式
1. myplugin.zip包解压到~/.vim目录，或者myplugin.vim文件拷贝到~/.vim/plugin/目录
```bash
~/.vim/plugin/myplugin.vim
~/.vim/doc/myplugin.txt
```
更新插件的帮助文档
```vim
:helptags ~/.vim/doc/
```
2. myplugin.vmb
```bash
vim myplugin.vmb -c "so %" -c "q"
```

###插件列表
+ [taglist-4.6](http://www.vim.org/scripts/script.php?script_id=273)
```bash
wget http://www.vim.org/scripts/download_script.php?src_id=19574 -O /tmp/taglist_46.zip && unzip /tmp/taglist_46.zip -d ~/.vim/
```

+ [cscope](http://cscope.sourceforge.net/)
```bash
wget http://cscope.sourceforge.net/cscope_maps.vim -O ~/.vim/plugin/cscope_maps.vim
```
如何[自动加载cscope.out文件](http://vim.wikia.com/wiki/Autoloading_Cscope_Database)，或者用autoload_cscope插件。

+ [autoload_cscope-0.5](http://www.vim.org/scripts/script.php?script_id=157)
```bash
wget http://www.vim.org/scripts/download_script.php?src_id=14884 -O ~/.vim/plugin/autoload_cscope.vim
```

+ [autotag-1.13](http://www.vim.org/scripts/script.php?script_id=1343)
```bash
wget http://www.vim.org/scripts/download_script.php?src_id=17415 -O ~/.vim/plugin/autotag.vim
```
+ [OmniCppComplete](http://www.vim.org/scripts/script.php?script_id=1520)

+ [clang complete](http://www.vim.org/scripts/script.php?script_id=3302)

+ [GCCSense](http://cx4a.org/software/gccsense/)

+ [supertab-2.0](http://www.vim.org/scripts/script.php?script_id=1643)
```bash
wget http://www.vim.org/scripts/download_script.php?src_id=18075 -O /tmp/supertab.vmb && vim /tmp/supertab.vmb -c "so %" -c "q"
```
[Vundle](https://github.com/gmarik/Vundle.vim#about)


[minibufexpl-6.3.2](http://www.vim.org/scripts/script.php?script_id=159)
```bash
wget http://www.vim.org/scripts/download_script.php?src_id=3640 -O ~/.vim/plugin/minibufexpl.vim
```
[ctrlp](https://github.com/kien/ctrlp.vim)
[安装](http://kien.github.io/ctrlp.vim/#installation)

[cvim-6.1](http://www.vim.org/scripts/script.php?script_id=213)
```bash
wget http://www.vim.org/scripts/download_script.php?src_id=21251 -O /tmp/cvim.zip && unzip /tmp/cvim.zip -d ~/.vim/
```







更新vim到7.4
```
7.4 已更新到 ppa 裡，Ubuntu 12.04 and 13.04 都可直接 apt 安裝
$ sudo add-apt-repository ppa:fcwu-tw/ppa
$ sudo apt-get update
$ sudo apt-get install vim
```

安装global-6.2.11
```bash
#安装依赖
sudo apt-get install gperf libncurses5-dev texinfo
#安装gnu global
cd global-6.2.11 && ./reconf.sh && ./configure && make && sudo make install

#安装vim插件
cp /usr/local/share/gtags/gtags.vim ～/.vim/plugin
cp /usr/local/share/gtags/gtags-cscope.vim ~/.vim/plugin
```
linux标准库或第三方库
```bash
cd /usr/include
sudo gtags
export GTAGSLIBPATH=/usr/include
```
    $ (cd /usr/src/sys; gtags)      # kernel source
    $ export GTAGSLIBPATH=/usr/src/lib:/usr/src/sys



```
map <C-F12> :!ctags -R --c++-kinds=+p --fields=+iaS --extra=+q .<CR>
map <F2> :TlistToggle <CR>
let Tlist_Show_One_File=1
let Tlist_Exit_OnlyWindow=1
set cscopequickfix=s-,c-,d-,i-,t-,e-
set mouse=a


nmap <C-\>g :cs find g <C-R>=expand("<cword>")<CR><CR>
nmap <C-\>c :cs find c <C-R>=expand("<cword>")<CR><CR>
nmap <C-\>d :cs find d <C-R>=expand("<cword>")<CR><CR>
nmap <C-\>t :cs find t <C-R>=expand("<cword>")<CR><CR>


let g:miniBufExplMapWindowNavVim = 1
let g:miniBufExplMapWindowNavArrows = 1
let g:miniBufExplMapCTabSwitchBufs = 1
let g:miniBufExplModSelTarget = 1
let g:miniBufExplMoreThanOne=0

let g:NERDTree_title="[NERDTree]"
let g:winManagerWindowLayout="NERDTree|TagList"

function! NERDTree_Start()
    exec 'NERDTree'
endfunction

function! NERDTree_IsValid()
    return 1
endfunction

nmap <F3> :WMToggle<CR>

"Vundle config, see https://github.com/gmarik/Vundle.vim#quick-start
set nocompatible              " be iMproved, required
filetype off                  " required

" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/vundle/
call vundle#rc()
" alternatively, pass a path where Vundle should install plugins
"let path = '~/some/path/here'
"call vundle#rc(path)

" let Vundle manage Vundle, required
Plugin 'gmarik/vundle'
Plugin 'Valloric/YouCompleteMe'

filetype plugin indent on     " required


```



参考资料
1. [将Vim改造为强大的IDE—Vim集成Ctags/Taglist/Cscope/Winmanager/NERDTree/OmniCppComplete](http://blog.csdn.net/bokee/article/details/6633193)
2. [Ubuntu下创建vim+Taglist+cscope+ctags组合编辑器](http://blog.csdn.net/longerzone/article/details/7789581)
3. [Vimball : 基于vim的插件管理器](http://blog.csdn.net/anonymalias/article/details/8656011)
4. [Vim自动补全神器–YouCompleteMe](http://marchtea.com/?p=161)