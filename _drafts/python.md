---
layout: post
title: Python is pseudo code
---

When I write code in my head, it's always in [Python](http://python.org/).  Because Python is basically pseudo code.

Some whiteboard code:

```
class Bean {
    bool cool = false;
    isCool() return cool;
    beCool(bool) set cool;
}

weCool(list<Bean> beans)
    for (Bean in beans)
        if !bean.isCool()
            bean.beCool(true);
    print("We cool.")
```

Curly braces are too hard to draw so forget those, semi-colons are intermittent because no one cares, iteration is implicit, etc.

## Whiteboard code to real code

### C++

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Bean
{
private:
    bool m_cool = false;

public:
    Bean()
    {
    }
    virtual ~Bean()
    {
    }

    bool isCool() const
    {
        return m_cool;
    }

    void beCool(bool cool)
    {
        m_cool = cool;
    }
};

void we_cool(vector<Bean> &beans)
{
    for (Bean &bean : beans)
    {
        if (!bean.isCool())
        {
            bean.beCool(true);
        }
    }
    cout << "We cool." << endl;
}

int main(int argc, char *argv[])
{
    vector<Bean> beans = {Bean{}, Bean{}};
    we_cool(beans);
    return 0;
}
```

### Java

```java
// NOTE: This class is in its own .java file
public class Bean {
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

/*****************************************************/

import java.util.ArrayList;

public class Main {
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

### Perl

```perl
```

### Python

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

Doesn't look too different from the pseudo code, but this is real Python code!

Python is really cool, and one of my favorite languages.  Without the constraints of minutia, programmers are free to write really cool code.

[Simplicity is empowering](http://xkcd.com/353/)
