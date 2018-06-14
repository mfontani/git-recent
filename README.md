# git-recent [-s] [-A] [N]

`git-recent` Shows `N` (default to 10) "unique recent branches" the user
has moved to/from, from the most recently moved to to the least recently
moved to, in the format:

    BRANCH_NAME [whitespace] SOURCE

... whereby `SOURCE` is whence the branch came from: from the reflog, or from
the list of all local branches. Use `-S` if you don't want the `SOURCE` to be
shown.

You can use `N=0` (i.e. `git recent 0`) to not restrict the output, and have it
show all branches in order:

* Branches and SHAs from the reflog, from most recently to least recently checked out.

* All other local branches

Use the `-s` option to *skip* showing (plausible) SHAs which were checked out,
and only show actual branches.

This will *not* work the way you expect if you named a branch using the same
set of characters (hex, `a-f0-9`) and the same length (40) that a SHA has.

Use the `-A` option to NOT show branches from the local branch list, and
only show branches from the reflog.

# How to use

Useful as a Git alias in `~/.gitconfig`, used in conjunction with `fzf`.
`cor` here stands for "check out recent":

    [alias]
      cor          = !git checkout $( git recent 0 -s | fzf +s | awk '{ print $1 }' )
      corsha       = !git checkout $( git recent 0    | fzf +s | awk '{ print $1 }' )

# Author

Marco Fontani - <MFONTANI@cpan.org>

# License

Copyright 2018 Marco Fontani <MFONTANI@cpan.org>

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.

3. Neither the name of the copyright holder nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE
LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
POSSIBILITY OF SUCH DAMAGE.
