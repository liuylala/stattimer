# stattimer - a C++ stopwatch timer library that reports statistics

This is a simple stopwatch timer library for C++ that reports statistics such as mean, standard deviation, max and min.

https://shingo-kagami.github.io/stattimer/


## Quick Start

### Q: How can I install it?

Get the file `stattimer.hpp` and put it in your include path. That's all.

### Q: How can I use it?

The following example measures the elapsed time between `st.start()` and `st.stop()` every time they are called. When the program finishes (i.e. when the object `st` is destroyed), the report is printed to the standard output. 

```c++
#include "stattimer.hpp"

STimerList st;

int
main()
{ 
    for (int i = 0; i < 1000; i++) {
        st.start("label1"); 
        /* Some codes here */
        st.stop("label1");
    } 
    return 0;
}
```

The report will look like: 

```
label1: mean = 0.306 [ms], std = 0.091, max/min = 0.783/0.239; 1000 iter.
```

You can put as many start/stop pairs as you want. They can be nested.

### Q: My program doesn't compile in Linux environment.

You may need -lrt option in the g++ command line. 

```
$ g++ -O2 main.cpp -lrt
```

### Q: How can I change the report format?

Besides the default format `STimerList::reporterDefault`, you can also use `STimerList::reporterTSV` that produces a tab separated vector (TSV) file. Specify it as an argument to the constructor of `STimerList`: 

```c++
STimerList st(STimerList::reporterTSV);
```

You can also define your own reporter function. The details will be written soon (?).

### Q: Can I put the report into a file instead of the standard output?

Yes, specify the file name as an argument to `STimerList` constructor, e.g.: 

```c++
STimerList st(STimerList::reporterDefault, "results.txt");
```
