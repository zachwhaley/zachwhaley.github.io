---
layout: post
title: Python is pseudo code
---

When I write code in my head, it's always in [Python](http://python.org/).  Because Python is basically pseudo code.

Some whiteboard code:

```
class Bean {
    bool cool;
    isCool() return cool;
    beCool(bool) set cool;
}

weCool(list<Bean> beans)
    for (Bean in beans)
        if !bean.isCool()
            print "Not cool."
            bean.beCool(true);
    print "We cool."

beans = [Bean(true), Bean(false)]
weCool(beans)
```

Curly braces are too hard to draw so forget those, semi-colons are intermittent because no one cares, iteration is implicit, etc.

## Whiteboard code to real code

Below is the code required to create this program in different languages, including the shell commands to actually run each program.

### Java

Bean.java

```java
package coolbeans;

public class Bean {
    private boolean mCool;

    public Bean(boolean cool) {
        mCool = cool;
    }

    public boolean isCool() {
        return mCool;
    }

    public void beCool(boolean cool) {
        mCool = cool;
    }
}
```

CoolBeans.java

```java
package coolbeans;

import java.util.ArrayList;

import coolbeans.Bean;

public class CoolBeans {
    public static void weCool(ArrayList<Bean> beans) {
        for (Bean bean : beans) {
            if (!bean.isCool()) {
                System.out.println("Not cool.");
                bean.beCool(true);
            }
        }
        System.out.println("We cool.");
    }

    public static void main(String[] args) {
        ArrayList<Bean> beans = new ArrayList<>();
        beans.add(new Bean(true));
        beans.add(new Bean(false));
        weCool(beans);
    }
}
```

```bash
$ javac -d . -cp . CoolBeans.java Bean.java
$ java coolbeans.CoolBeans
Not cool.
We cool.
```

### C++

coolbeans.cpp

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Bean
{
private:
    bool m_cool;

public:
    Bean(bool cool) :
        m_cool(cool)
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
            cout << "Not cool." << endl;
            bean.beCool(true);
        }
    }
    cout << "We cool." << endl;
}

int main(int argc, char *argv[])
{
    vector<Bean> beans = {Bean{true}, Bean{false}};
    we_cool(beans);
    return 0;
}
```

```bash
$ g++ -std=c++11 -o coolbeans coolbeans.cpp
$ ./coolbeans
Not cool.
We cool.
```

### Ruby

coolbeans.rb

```ruby
class Bean
  def initialize(cool)
    @cool = cool
  end

  def is_cool
    return @cool
  end

  def be_cool=(cool)
    @cool = cool
  end
end

def we_cool(beans)
  beans.each do |bean|
    if not bean.is_cool()
      puts "Not cool."
      bean.be_cool = true
    end
  end
  puts "We cool."
end

beans = [Bean.new(true), Bean.new(false)]
we_cool beans
```

```bash
$ ruby coolbeans.rb
Not cool.
We cool.
```

### Python

coolbeans.py

```python
class Bean:
    def __init__(self, cool):
        self.cool = cool

    def is_cool(self):
        return self.cool

    def be_cool(self, cool):
        self.cool = cool


def we_cool(beans):
    for bean in beans:
        if not bean.is_cool():
            print 'Not cool.'
            bean.be_cool(True)
    print 'We cool.'


beans = [Bean(True), Bean(False)]
we_cool(beans)
```

```bash
$ python coolbeans.py
Not cool.
We cool.
```

Doesn't look too different from the pseudo code, but this is real Python code!

Python is really cool, and one of my favorite languages.  Without the constraints of minutia, programmers are free to write [really cool code.](http://xkcd.com/353/)
