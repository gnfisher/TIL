# Delete open buffers

You can list your open buffers with `:buffers`.

You can close a buffer by passing a string to the `:bd` (buffer delete) command
that matches part of the file path for the open buffer or you can pass the
number assigned to the buffer that is visible in the quickfix window that
`:buffers` opens.

So `:bd 1` closes the buffer assigned the number 1 and `:bd readme` would close
the buffer for `./project/README.md`.

If the buffer has been modified and not saved you need to add a `:bd!` bang (it
will close and you'll lose changes, too).

If you want to go nuclear, you can call `:bufo bd` and close all open buffers without exiting vim.
