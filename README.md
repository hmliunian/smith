# smithdata     segment
message  db 'da xie zhuan hua wei xiao xie,esc wei tui chu'
         db 0dh,0ah,'$'
data     ends
code     segment
assume   cs:code,ds:data
start:   mov ax,data
         mov ds,ax
         mov dx,offset message
         mov ah,9
         int 21h;输出提示符
again:   mov ah,1
         int 21h
         cmp al,1bh;如果为esc跳出
         je exit
         or al,00100000b;大写变小写
         mov dl,al
         mov ah,2
         int 21h
         jmp again
exit:    mov ah,4ch
         int 21h          
code     ends
         end start
