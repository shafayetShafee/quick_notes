
## How to use different python version and use that and install packages for that specific python version ??

### A possible Solution

---

1. Open windows `cmd` or `git bash` and enter (if `virtualenv` is not installed.)

~~~
    $ pip install virtualenv
~~~

2. Download the desired python version (**DO NOT ADD TO	 PATH!**), and remember the ***path\to\new_python.exe*** of the newly installed version.

3. To create a `virtualenv`, open `cmd` or `git bash` and enter

~~~
    $ virtualenv \path\to\env -p path\to\new_python.exe
~~~


4. **Activate virtualenv**: open Command Prompt or git bash and enter

~~~
    $ path\to\env\Scripts\activate.bat (in cmd)
    $ source path\to\env\Scripts\activate (in git bash)
~~~

5. Install desired packages using pip in usual way

6. Deactivate the virtual env with 

~~~
    $ deactivate
~~~ 

---