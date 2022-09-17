## Managing tlmgr (TexLive pkg Manager)

#### Installing package (say parskip)

~~~ 
> tlmgr install parskip
~~~


#### Chekcing if already a package is installed (say checking for babel package)

- check for styles files

~~~
$ kpsewhich babel.sty
~~~

- checking multiple pkgs

~~~
$ kpsewhich babel.sty geometry.sty setspace.sty
~~~


#### Bare installing is time consuming for `tlmgr` default option so use `--no-persistent-downloads` option when installing and it will be damn faster than before.

~~~
$ tlmgr install blindtext --no-persistent-downloads
~~~

#### Getting help file for a package (say geometry)

~~~
$ texdoc geometry
~~~