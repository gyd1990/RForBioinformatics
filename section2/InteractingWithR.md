# Interacting with R

The command line is the way to interact with R. That is, R requires
typing commands into the console. There is no built-in point-and-click 
approach to using R. Such typed commands come in only two flavors:

* Expressions
* Assignments

## Expressions


```r
1 + pi + sin(3.7)
```

```
## [1] 3.611757
```

Expressions are evaluated by R immediately after hitting `Enter` on the keyboard. The result is printed directly to the screen, but R does not 
"remember" the result. If, later in an R session, the result is needed, the calculation must be performed again.

## Assignments
        

```r
x = 1
y <- 2
```

The `<-` and `=` are both assignment `operators`. In this case, R did not print out the result. Instead, the result was *assigned* to a name, referred to as a *variable*. This variable can be used later to retrieve the value without having to recompute anything. 

The standard R prompt is a `>` sign. If a line is not a complete R command, R will typically continue the next line with a `+`. Try repeating the expression from above putting in the extra line as noted below.


```r
1 + pi + 
sin(3.7)
```

# Names in R

Functions, variables, methods, etc. in R all have names. There are some rules about what constitutes a valid name in R. Valid names in R:

* may contain any combination of letters, numbers, underscore, and "."
* may not start with numbers, underscore.


```r
pi
x
camelCaps
my_stuff
MY_Stuff
this.is.the.name.of.the.man
ABC123
abc1234asdf
.hi
```

![tip](../images/tips.ico) R is case-sensitive, so `Abc` is different than `abc`, for example.
