# Composing a PR

Nobody is perfect, and submitting perfect changes that don't need any tweaks is
quite a rare instance. After a few iterations, your PR, which is a list of
commits, could look like this:

- replace tabs with spaces (who did this?)
- add flux capacitor feature
- add missing documentation (silly me)
- add missing tests (I love TDD, but…)
- fix typo in documentation
- set default value as suggested

Ideally, we should be able to revert any commit in your PR and not have to
revert the others too. For instance, if we decide to revert your feature
because it turns out to cause more problems than it solves, we should not have
to revert the commit with the feature itself, then the commit with the
documentation, then the commit with the tests, etc…

Another thing to take into consideration is that in some hopefully rare
instances, you will need to keep some commits separate, because they do not
really relate to what you are doing, but the "other" thing you fixed, while
unrelated, somehow prevents you from doing your PR, or is a minor thing you
feel does not warrant a PR by itself, especially if this PR is conflicting with
the one you are currently trying to do. This is the case of the first commit in
the list above: you cannot really work until it is resolved and even if your
feature is messed up and we revert it, we will probably want to keep that
commit anyway.

Luckily, git allows you to rewrite your history before we merge your PR so that
it looks like you wrote perfect code from the start. Provided you are making a
PR on `origin/some_branch`, `git rebase --interactive origin/some_branch` will
present you with a list of commits prefixed with actions, just like that:

```
pick 38e1219 replace tabs with spaces (who did this?)
pick 99f65a4 add flux capacitor feature
pick 673b30f add missing documentation (silly me)
pick 0ef6ae0 add missing tests (I love TDD, but…)Add
pick 7c3f268 fix typo in documentation
pick 1175ab1 set default value as suggested
```

You can reorder this list as you see fit, you can also remove commits, or
merge them with their parent commit. On this instance you will want to merge or
"fixup" the last 4 commits into the second commit. This can simply be achieved
by replacing the action before these commits with `fixup` (or simply `f`), like
this:

```
pick 38e1219 replace tabs with spaces (who did this?)
pick 99f65a4 add flux capacitor feature
fixup 673b30f add missing documentation (silly me)
fixup 0ef6ae0 add missing tests (I love TDD, but…)Add
fixup 7c3f268 fix typo in documentation
fixup 1175ab1 set default value as suggested
```

Then simply save and quit, and your branch should look like that:

- replace tabs with spaces (who did this?)
- add flux capacitor feature

Finally, use `git push --force` to overwrite your PR with this.

Now this might seem a bit complicated, but their are some handy shortcuts you
can use in some special cases. For instance, if you want to modify the last
commit, simply use `git commit --amend`, then force-push your branch.

Also, if your end goal is to get one commit and you cannot seem to be able to
get to that, simply tell us, we will able to squash all the commits for you
using GitHub's
["squash and merge" feature](https://github.com/blog/2141-squash-your-commits).

If you want to learn more you can play
[this game](http://pcottle.github.io/learnGitBranching/)
about git branching, and of course, you may also
[RTFM](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History).
