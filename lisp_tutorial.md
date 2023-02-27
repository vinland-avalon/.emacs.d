<h1>Getting Started</h1>
<p>
Environment and Configs
<br>
On MacOS, reference:https://lisp-lang.org/learn/getting-started/
<br>
SBCL + QuickLisp + SLIME
</p>
<h2>Install SBCL</h2>
<p>the Common Lisp implementation<br>
<code>$ brew install sbcl</code></p>
<h2>Install QuickLisp</h2>
<p>the package manager<br>
<code>  

    $ curl -o /tmp/ql.lisp http://beta.quicklisp.org/quicklisp.lisp 
    $ sbcl --no-sysinit --no-userinit --load /tmp/ql.lisp \
       --eval '(quicklisp-quickstart:install :path "~/.quicklisp")' \
       --eval '(ql:add-to-init-file)' \
       --quit
</code>
<h2>Install SLIME with Emacs</h2>
<p>a CommonLisp IDE built on Emacs<br>
<code>$ sbcl --eval '(ql:quickload :quicklisp-slime-helper)' --quit</code><br>
then add it to the init file of Emacs<br>
<code>(load (expand-file-name "~/.quicklisp/slime-helper.el"))<br>
(setq inferior-lisp-program "/opt/homebrew/bin/sbcl")</code>
</p>
<h2>Now Running SMILE</h2>
To start slime: On Emacs: M+x smile<br>
<code>
    CL-USER> (format t "Hello, world!")<br>Hello, world!<br>NIL
</code>
To exit slime: comma(,) + sayoonara
</p>
