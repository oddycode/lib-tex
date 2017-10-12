# lib-tex

A variant of the texlive 2017 distribution, but adapted for cross-compiling and with function calls in a library. I made it so I could use pdftex and luatex on iOS, but there are other uses. 

To compile: 
```
./build_command.sh
```
This is just the "Build" command of texlive, but with most of the packages (e.g. tex, dvipdfmx...) disabled. If you are not cross-compiling for iOS, remove the "--host" and "--build" part of the command, as well as the "CFLAGS", "CXXFLAGS", "OBJCXXFLAGS". 

Once compilation is done, you may have to edit the digital libraries to change their location and the location of other dynamic libraries relative to them. Copy "fix_texlive_dynamiclibs.sh" to the directory where you will be installing the libraries, edit the two environment variables at the top, then run it:
```
./fix_texlive_dynamiclibs.sh
```

You should be all set. "texlive_ios.h" is the header file that contains the function calls you can use: 
```
extern int bibtex_main(int argc, char *argv[]);
extern int dllluatexmain(int argc, char *argv[]);
extern int dllpdftexmain(int argc, char *argv[]);
```

Each of them is equivalent to calling "main()" in the respective command. To call "lualatex myFile.tex", you call "dllluatexmain(3, "lualatex", "myFile.tex")";
