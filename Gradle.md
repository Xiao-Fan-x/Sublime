# Gradle

groovy高效特性

1.可选的类型定义

def version = 1

2.assert 

assert version == 2

3.括号是可选的

println version

4.字符串

def s1 = 'string1'

def s2 = "gradle version is ${version}"

def s3 = '''my

gradle is 

: )'''

println s1

println s2

println s3



5.集合api

list

```
def buildTools = ['ant','maven']
buildTools << 'gradle'
assert buildTools.getClass() == ArrayList
assert buildTools.size()==3
```

map

```
def buildYear = ['ant':2000,"maven":2004]
buildYear.gradle = 2009

println(buildYear.ant)
println buildYear["gradle"]
println buildYear.getClass()
```

6.闭包

```
def c1 = {
    v ->
        println v
}

def c2 = {
    print 'hello'
}

def  method1(Closure closure){
    closure('param')
}

def method2(Closure closure){
    closure
}

method1(c1)
method1(c2)
```

