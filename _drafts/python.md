---
layout: post
title: Python is pseudo code
---

When I think of code in my head, it's always in [Python](http://python.org/).  Because Python is basically pseudo code.

When I write code on a whiteboard, this is what it usually looks like:

```
weCool(list<Bean> beans)
    for (Bean bean in beans)
        if !bean.isCool()
            bean.beCool(true);
    print("We cool.")
```

Curly braces are too hard to draw so forget those, semi-colons are intermittent because no one cares, etc.

Now, the same whiteboard but with real Python:

```python
def we_cool(beans):
    for bean in beans:
        if not bean.is_cool():
            bean.be_cool(True)
    print("We cool.")
```

Doesn't look too different from the pseudo code, but this is real Python code!


To really compare, here is the same code written in compilable Java.

```java
import java.util.ArrayList;

class Bean {
    private boolean mCool = false;

    public Bean() {
    }
    public boolean isCool() {
        return mCool;
    }
    public void beCool(boolean cool) {
        mCool = cool;
    }
}

class Main {
    public static void weCool(ArrayList<Bean> beans) {
        for (Bean bean : beans) {
            if (!bean.isCool()) {
                bean.beCool(true);
            }
        }
        System.out.println("We cool.");
    }

    public static void main(String[] args) {
        ArrayList<Bean> beans = new ArrayList<>();
        beans.add(new Bean());
        beans.add(new Bean());
        weCool(beans);
    }
}
```

And "compilable" Python

```python
class Bean:
    def __init__(self):
        self.cool = False
    def is_cool(self):
        return self.cool
    def be_cool(self, cool):
        self.cool = cool

def we_cool(beans):
    for bean in beans:
        if not bean.is_cool():
            bean.be_cool(True)
    print("We cool.")

beans = [Bean(), Bean()]
we_cool(beans)
```

That Java code had a lot of extra crap!  While the Python code has roughly 10 more lines than the pseudo code.

I know that Python is considered by many a scripting language and that is why it has so many fewer lines, but other scripting languages don't have the magical mixture of brevity and verbosity that Python has achieved.  It seems like most scripting languages are just too sparse, making them hard to read at a glance.

Simplicity is empowering.  Without the constraints of minutia, programmers can write really cool code.
