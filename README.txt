Celiac This Is
===============

A Jekyll-based static site.

Requirements
------------
- Ruby (tested with 3.2.3)
- Jekyll gem (tested with 4.4.1)

Note: on this machine, jekyll is installed under a non-standard gem path
(VS Code's bundled Ruby gem home), not on the default PATH. This path
includes VS Code's snap revision number, which changes whenever VS Code
updates (check with `readlink /home/<user>/snap/code/current` if the
command below stops working). Before running jekyll commands, set:

    export GEM_HOME=/home/<user>/snap/code/current/.local/share/gem/ruby/3.2.0
    export PATH="$GEM_HOME/bin:$PATH"

Running locally
----------------
From the project root:

    jekyll serve --port 4001

Then open http://127.0.0.1:4001 in your browser. Auto-regeneration is
enabled, so edits to source files are picked up automatically.

If the browser shows "failed to load page" for any URL on port 4001, the
server is most likely not running (or was stopped) — start it again with
the command above.
