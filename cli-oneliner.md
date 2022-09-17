## Some Bash Oneliner (probably !!!) faced along the way

1. For renaming files (preappending files with sequential number)

~~~
    $ ls P* | cat -n | while read n f; do mv -n "$f" "0 (($n+3))_$f" ; done
~~~


2. For replacing space filename

~~~
    $ for f in *\ *; do mv "$f" "${f// /_}"; done
~~~

- *\ * selects files with space in names
- ${parameter/pattern/replace} is parameter syntax of bash



3. Creating multiple sequential file

~~~
    $ for i in {1..10}; do touch file$i.txt; done
~~~

- We can also do this for directory

~~~
    $ for i in {60..69}; do touch ./texts/file$i.txt; done
~~~

- or with parameter expansion

~~~
    $ touch bspl{0001..0003}.c
~~~


4. Turning a space separated file in comma separated file in bash

~~~
    $ sed -e 's/\s/,/g' text.txt > new.txt
~~~

- or in vim

~~~
    $ vim filename.txt
    : set nu 
    : %s/ /,/g
    : wq!
~~~

- `: set nu` sets the line number
- `%s/ /,/g` pattern searching and then replacing ` ` with `,` (globally)
- `:wq!` write (save) and then quit


5. How to select only two digit number and replace with commas in vim (using boundary)

~~~
    :%s/\<\d\{2\}\>/,/g
~~~

6. How to create multiple files with common name but different extensions?

~~~
    $ touch filename.{ext1,ext2}
~~~

**Be careful about not to put space between ext1 and ext2 except comma**

~~~
> touch chap01.{R,txt}
~~~


7. Copy multiple files with specific pattern

~~~
    $ cp *lang_en.srt ..
~~~

- or

~~~
    $ find -regex *lang_en.srt -exec cp {} \;
~~~