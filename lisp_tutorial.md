# Lisp Learning Begins Now!

- [Lisp Learning Begins Now!](#lisp-learning-begins-now)
- [Getting Started](#getting-started)
  - [Install SBCL](#install-sbcl)
  - [Install QuickLisp](#install-quicklisp)
  - [Install SLIME with Emacs](#install-slime-with-emacs)
  - [Now Running SMILE](#now-running-smile)
- [Syntax](#syntax)
  - [S-expression](#s-expression)
  - [functions](#functions)
    - [In a functional language, they are the first class](#in-a-functional-language-they-are-the-first-class)
      - [generic functions and methods](#generic-functions-and-methods)
  - [local variables](#local-variables)
  - [dynamic variables](#dynamic-variables)
  - [list](#list)
    - [basic usage](#basic-usage)
    - [higer-order functions](#higer-order-functions)
      - [map](#map)
      - [reduce](#reduce)
      - [sort](#sort)
  - [Input / Output](#input--output)
    - [Format](#format)
    - [File I/O ...](#file-io-)


# Getting Started
- Environment and Configs
- On MacOS, reference: https://lisp-lang.org/learn/getting-started/
- SBCL + QuickLisp + SLIME
## Install SBCL
the Common Lisp implementation
```
$ brew install sbcl
```
## Install QuickLisp
the package manager
```
    $ curl -o /tmp/ql.lisp http://beta.quicklisp.org/quicklisp.lisp 
    $ sbcl --no-sysinit --no-userinit --load /tmp/ql.lisp \
       --eval '(quicklisp-quickstart:install :path "~/.quicklisp")' \
       --eval '(ql:add-to-init-file)' \
       --quit
```
## Install SLIME with Emacs
a CommonLisp IDE built on Emacs
```
$ sbcl --eval '(ql:quickload :quicklisp-slime-helper)' --quit
```
then add it to the init file of Emacs
```
(load (expand-file-name "~/.quicklisp/slime-helper.el"))
(setq inferior-lisp-program "/opt/homebrew/bin/sbcl")
```
## Now Running SMILE
To start slime: On Emacs: ``M+x smile``
```
CL-USER> (format t "Hello, world!")<br>Hello, world!<br>NIL
```
To exit slime: ``comma(,) + sayoonara``

# Syntax

## S-expression 
_atom_ and _list_, where _atom_ refers to numbers, variables, keywords and so on.

## functions 
### In a functional language, they are the first class
```
(defun fib (n)
  "Return the nth Fibonacci number."
  (if (< n 2)
      n
      (+ (fib (- n 1))
         (fib (- n 2)))))
```
Then we can use above function with ``(fib 3)``  
functions can also return multiple values
#### generic functions and methods
```
(defgeneric description (object)
  (:documentation "Return a description of an object."))
```
```
(defmethod description ((object integer))
  (format nil "The integer ~D" object))

(defmethod description ((object float))
  (format nil "The float ~3,3f" object))
```
```
CL-USER> (description 10)
"The integer 10"

CL-USER> (description 3.14)
"The float 3.140"
```
## local variables
There is no difference with other programming lanuages.  
Use ``let`` to define:  
```
(let ((str "Hello, world!"))
  (string-upcase str))

;; => "HELLO, WORLD!"
```
To define variables whose initial values depend on previous variables in the same form, use ``let*``:
```
(let* ((x 1)
       (y (+ x 1)))
  y)

;; => 2
```
## dynamic variables
The __scope__ of variable is dynamic -- could be used as global cariable, but even more powerful  
There are two ways to define: ``defparameter`` and ``defvar``

## list
### basic usage
``(list 1 2 3)``  
``fisrt``...``tenth`` -> ``nth``  
``defpatameter``,``setf``  
for exampe:  
```
CL-USER> (defparameter my-list (list 1 2 3))
MY-LIST

CL-USER> (setf (nth 1 my-list) 65)
65

CL-USER> my-list
(1 65 3)
```
### higer-order functions  
#### map
The ``map`` function takes a functions and a list as input, then apply the function to each element and return the result list. They keyword for ``map`` is ``mapcar``, and we can implement our own ``mapcar``:
```
CL-USER> (defun my-map (function list)
           (if list
               (cons (funcall function (first list))
                     (my-map function  (rest list)))
               nil))
MY-MAP

CL-USER> (my-map #'string-upcase (list "a" "b" "c"))
("A" "B" "C")
```
#### reduce
Used to turn a list into a scala.
```
CL-USER> (reduce #'+ (list 1 2 3))
6
```
If we want a UDF, we can turn to ``lambda`` for help:
```
CL-USER> (reduce #'(lambda (a b)
                     (* a b))
                 (list 10 20 30))
6000
```
#### sort
```
CL-USER> (sort (list 9 2 4 7 3 0 8) #'<)
(0 2 3 4 7 8 9)
```
## Input / Output
### Format
Like ``printf`` in C, we use ``format`` in Lisp to print output to screen and terminal:
```
(format t "Hello, World")
```




