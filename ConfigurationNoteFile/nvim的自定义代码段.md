# 自定义代码段

光标忽略字符移动参考
```
" <SPACE>   : forward to next word beginning with alphanumeric char
" <S-SPACE> : backward to prev word beginning with alphanumeric char
" <C-SPACE> : same as above (as <S-SPACE> not available in console Vim
" <BS>      : back to prev word ending with alphanumeric char
function! <SID>GotoPattern(pattern, dir) range
    let g:_saved_search_reg = @/
    let l:flags = "We"
    if a:dir == "b"
        let l:flags .= "b"
    endif
    for i in range(v:count1)
        call search(a:pattern, l:flags)
    endfor
    let @/ = g:_saved_search_reg
endfunction
nnoremap <silent> <SPACE> :<C-U>call <SID>GotoPattern('\(^\\|\<\)[A-Za-z0-9_]', 'f')<CR>
vnoremap <silent> <SPACE> :<C-U>let g:_saved_search_reg=@/<CR>gv/\(^\\|\<\)[A-Za-z0-9_]<CR>:<C-U>let @/=g:_saved_search_reg<CR>gv
nnoremap <silent> <S-SPACE> :<C-U>call <SID>GotoPattern('\(^\\|\<\)[A-Za-z0-9_]', 'b')<CR>
vnoremap <silent> <S-SPACE> :<C-U>let g:_saved_search_reg=@/<CR>gv?\(^\\|\<\)[A-Za-z0-9_]<CR>:<C-U>let @/=g:_saved_search_reg<CR>gv
nnoremap <silent> <BS> :call <SID>GotoPattern('[A-Za-z0-9_]\(\>\\|$\)', 'b')<CR>
vnoremap <silent> <BS> :<C-U>let g:_saved_search_reg=@/<CR>gv?[A-Za-z0-9_]\(\>\\|$\)<CR>:<C-U>let @/=g:_saved_search_reg<CR>gv

" Redundant mapping of <C-SPACE> to <S-SPACE> so that
" above mappings are available in console Vim.
"noremap <C-@> <C-B>
if has("gui_running")
    map <silent> <C-Space> <S-SPACE>
else
    if has("unix")
        map <Nul> <S-SPACE>
    else
        map <C-@> <S-SPACE>
    endif
endif
```
[原文链接：https://stackoverflow.com/questions/6527698/setting-to-skip-over-punctuation-when-moving-forwards-and-backwards-words](https://stackoverflow.com/questions/6527698/setting-to-skip-over-punctuation-when-moving-forwards-and-backwards-words) 

