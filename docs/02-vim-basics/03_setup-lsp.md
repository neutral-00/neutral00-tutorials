# Set up Language Server Protocol

First install vim-plug. For this open `~/.vimrc` and add the following

```sh
call plug#begin('~/.vim/plugged')
Plug 'prabirshrestha/vim-lsp' " Language Server Protocol support
Plug 'mattn/vim-lsp-settings'
call plug#end()
```

Next add the following after it.
This is setting up autocomplete fuction to work with LSP.

```sh
function! s:on_lsp_buffer_enabled() abort
    setlocal omnifunc=lsp#complete
endfunction

augroup lsp_install
    au!
    autocmd User lsp_buffer_enabled call s:on_lsp_buffer_enabled()
augroup END
```

Tip: you can press `Ctrl-x o` to start the auto-complete

Now save the `.vimrc`, exit vim and relauch it.
Run :PlugInstall

Next, open a file say: vim ~/main.java
Vim will offer you to install the relevant lsp in the status line.

![jdtls](/img/eclipse_jdtls.png)

Now simply run the command `:LspInstallServer` . Doing so will ask for confirmation to install it. \
![confirmation-jdtls](/img/confirm_jdtls.png)

Press Y to confirm. It will start installing it.

![install-jdtls](/img/install_jdtls.png)

Restart vim and reopen the java file.
