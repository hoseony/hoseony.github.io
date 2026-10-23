---
layout: default
title: Modifying struct FILE
permalink: /notes/c/modifyStructFILE
lastmod: 2026-10-22
---
## Did you know that you can modify struct FILE?
For some reason, I never thought that this was something you could do. But since you have full access to the `struct FILE` inside your code, you can just modify its content. Why would you do that? I really don't know. BUT you CAN do it.

Let's see how to do it. Why not?

NOTE: the code I am showing only works on Linux. I am running a VM. If you are on macOS, I recommend setting up a Linux VM or figuring out the naming on macOS.

### struct _IO_FILE
First things first, let's investigate what there is to modify. From the [standard library](https://github.com/lattera/glibc/blob/master/libio/bits/types/struct_FILE.h), `struct FILE` is defined as follows.
```c
struct _IO_FILE
{
  int _flags;		/* High-order word is _IO_MAGIC; rest is flags. */

  /* The following pointers correspond to the C++ streambuf protocol. */
  char *_IO_read_ptr;	/* Current read pointer */
  char *_IO_read_end;	/* End of get area. */
  char *_IO_read_base;	/* Start of putback+get area. */
  char *_IO_write_base;	/* Start of put area. */
  char *_IO_write_ptr;	/* Current put pointer. */
  char *_IO_write_end;	/* End of put area. */
  char *_IO_buf_base;	/* Start of reserve area. */
  char *_IO_buf_end;	/* End of reserve area. */

  /* The following fields are used to support backing up and undo. */
  char *_IO_save_base; /* Pointer to start of non-current get area. */
  char *_IO_backup_base;  /* Pointer to first valid character of backup area */
  char *_IO_save_end; /* Pointer to end of non-current get area. */

  struct _IO_marker *_markers;

  struct _IO_FILE *_chain;

  int _fileno;
  int _flags2;
  __off_t _old_offset; /* This used to be _offset but it's too small.  */

  /* 1+column number of pbase(); 0 is unknown. */
  unsigned short _cur_column;
  signed char _vtable_offset;
  char _shortbuf[1];

  _IO_lock_t *_lock;
#ifdef _IO_USE_OLD_IO_FILE
};
```

### Let's have some fun!
#### Swapping `_fileno`
So, the first thing you can do is changing `_fileno`.

```c
#include <stdio.h>
#include <fcntl.h>

int main(void) {
    int fd = open("out.txt", O_WRONLY | O_CREAT | O_TRUNC, 0644);
    if (fd < 0) {
        perror("open"); 
        return 1;
    }

    printf("this goes to the terminal\n");
    fflush(stdout);

    stdout->_fileno = fd;
    printf("this goes to out.txt\n");
    return 0;
}
```

We have redirected `printf` to `out.txt` by changing `_fileno` of `stdout`! `printf` has no idea that anything happened. It still writes to `stdout`, but `stdout` is now pointing to `out.txt`. Turns out, `stdout` is not that special at all. That was surprisingly easy. Let's do something a bit more interesting.

#### Editing what you "printed"
What we are going to do here is "edit" what has already been "printed." There are some double quotes here and there because you are not actually editing, and it is not actually printed. 

```c
#include <stdio.h>

int main(void) {
    printf("hello world"); // This is not printed yet! It is in the buffer.
    stdout->_IO_write_base[0] = 'J'; // Edit the content
    printf("\n");
    fflush(stdout); // flush the buffer

    printf("fish was here");
    stdout->_IO_write_ptr = stdout->_IO_write_base; // "resetting" the buffer
    printf("good bye\n"); // oh no

    return 0;
}
```
The output of this C program is 
```
Jello world
good bye
```

What's happening is that this program is editing a buffer that hasn't been sent yet. This is possible because `printf` is actually buffered. It doesn't print every time you use `printf()`. The usual process is `printf` -> buffer -> `write()` -> terminal. The write system call happens when the buffer is full, when you print `\n`, when you call `fflush`, or when it exits (I am being very vague here on purpose… Curious readers should look into it more in their own time).

The buffer has `_IO_write_base` and `_IO_write_ptr`. `_IO_write_base` points to where the unsent text starts, and `_IO_write_ptr` points to where it ends. Everything in between these two pointers is going to be printed. So "fish was here" is basically gone by moving `_IO_write_ptr` to `_IO_write_base`. glibc thinks that there is nothing to print, and "good bye" just writes over it.


### Your turn...
Can you change "hello world" to "fish world"??
