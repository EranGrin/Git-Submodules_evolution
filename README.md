# Git-Submodules_evolution
A summary of Git release note with respect of submodules


GIT First Submodules Release - 2008
========================
v1.5.3
* The submodule support has Porcelain layer.
  Note that the current submodule support is minimal and this is
  deliberately so.  A design decision we made is that operations
  at the supermodule level do not recurse into submodules by
  default.  The expectation is that later we would add a
  mechanism to tell git which submodules the user is interested
  in, and this information might be used to determine the
  recursive behaviour of certain commands (e.g. "git checkout"
  and "git diff"), but currently we haven't agreed on what that
  mechanism should look like.  Therefore, if you use submodules,
  you would probably need "git submodule update" on the
  submodules you care about after running a "git checkout" at
  the supermodule level.


1.5.6.5
  * Addition of "git update-index --ignore-submodules" that happened during
  1.5.6 cycle broke "git update-index --ignore-missing".


1.6.1 
* "git submodule foreach" subcommand allows you to iterate over checked
  out submodules.


1.6.4
* "git submodule update" learned --rebase option to update checked
   out submodules by rebasing the local changes.


1.7.1
 * "git status" notices and describes dirty submodules.


1.7.3
 * diff.ignoresubmodules configuration variable can be used to squelch the
   differences in submodules reported when running commands (e.g. "diff",
   "status", etc.) at the superproject level.


1.7.4
* "git fetch" learned the "--recurse-submodules" option.


1.7.5
* "git fetch" can be told to recursively fetch submodules on-demand.


1.7.6
* "git submodule update" learned "--force" option to get rid of local
   changes in submodules and replace them with the up-to-date version.


1.7.6.1
* "git fetch" did not recurse into submodules in subdirectories.


1.7.6.3
* "git fetch" had a major performance regression, wasting many
   needless cycles in a repository where there is no submodules
   present. This was especially bad, when there were many refs.


1.7.7
* "git submodule update" used to stop at the first error updating a
   submodule; it now goes on to update other submodules that can be
   updated, and reports the ones with errors at the end.


* "git push" can be told with the "--recurse-submodules=check" option to
   refuse pushing of the supermodule, if any of its submodules'
   commits hasn't been pushed out to their remotes.


1.7.7.1
* The code to check for updated submodules during a "git fetch" of the
   superproject had an unnecessary quadratic loop.


1.7.8
* The recursive merge backend no longer looks for meaningless
   existing merges in submodules unless in the outermost merge.


1.7.8.1
* "git check-attr" learned "--cached" option to look at .gitattributes
   files from the index, not from the working tree.


1.7.10.1
* "git fetch" that recurses into submodules on demand did not check
   if it needs to go into submodules when non branches (most notably,
   tags) are fetched.
* Giving "--continue" to a conflicted "rebase -i" session skipped a
   commit that only results in changes to submodules.


1.7.11
* "git push --recurse-submodules" learned to optionally look into the
   histories of submodules bound to the superproject and push them
   out.
* "git submodule init" used to report "registered for path ..."
   even for submodules that were registered earlier.
   (cherry-pick c1c259e jl/submodule-report-new-path-once later to maint).


1.8.2.1
* "git submodule update", when recursed into sub-submodules, did not
   accumulate the prefix paths.


1.8.3
* "git submodule update", when recursed into sub-submodules, did not
   accumulate the prefix paths.


1.8.4
* In addition to the choice from "rebase, merge, or checkout-detach",
   "submodule update" can allow a custom command to be used in to
   update the working tree of submodules via the "submodule.*.update"
   configuration variable.


1.8.5
* "git status" no longer prints the dirty status information of
   submodules for which submodule.$name.ignore is set to "all".


1.9.2
* "git mv" that moves a submodule forgot to adjust the array that
   uses to keep track of which submodules were to be moved to update
   its configuration.


2.0.0
* "git mv" that moves a submodule forgot to adjust the array that
   uses to keep track of which submodules were to be moved to update
   its configuration.
   (merge fb8a4e8 jk/mv-submodules-fix later to maint).


2.3.10
* Some protocols (like git-remote-ext) can execute arbitrary code
   found in the URL.  The URLs that submodules use may come from
   arbitrary sources (e.g., .gitmodules files in a remote
   repository), and can hurt those who blindly enable recursive
   fetch.  Restrict the allowed protocols to well known and safe
   ones.


2.7.0
* "git push" learned new configuration for doing "--recurse-submodules"
   on each push.


2.8.0
* Add a framework to spawn a group of processes in parallel, and use
   it to run "git fetch --recurse-submodules" in parallel.


2.8.3
* A partial rewrite of "git submodule" in the 2.7 timeframe changed
   the way the gitdir: pointer in the submodules point at the real
   repository location to use absolute paths by accident.  This has
   been corrected.
* "git submodule" reports the paths of submodules the command
   recurses into, but this was incorrect when the command was not run
   from the root level of the superproject.


2.8.4
* When de-initialising all submodules, "git submodule deinit" gave a
   faulty recommendation to use "git submodule deinit .", which would
   result in a strange error message in a pathological corner case.
   This has been corrected to suggest "submodule deinit --all" instead.


2.9.0
* "git -c credential.<var>=<value> submodule" can now be used to
   propagate configuration variables related to credential helper
   down to the submodules.
* "git clone" learned the "--shallow-submodules" option.
* "git submodule" reports the paths of submodules the command
   recurses into, but these paths were incorrectly reported when
   the command was not run from the root level of the superproject.
 * Correct faulty recommendation to use "git submodule deinit ." when
   de-initialising all submodules, which would result in a strange
   error message in a pathological corner case.


2.9.1
* Fix an unintended regression in v2.9 that breaks "clone --depth"
   that recurses down to submodules by forcing the submodules to also
   be cloned shallowly, which many server instances that host upstream
   of the submodules are not prepared for.


2.10.0
* An upstream project can make a recommendation to shallowly clone
   some submodules in the .gitmodules file it ships.
* "git submodule update" that drives many "git clone" could
   eventually hit flaky servers/network conditions on one of the
   submodules; the command learned to retry the attempt.


2.10.1
* Having a submodule whose ".git" repository is somehow corrupt
   caused a few commands that recurse into submodules loop forever.


2.11.0
* "git clone --recurse-submodules --reference $path $URL" is a way to
   reduce network transfer cost by borrowing objects in an existing
   $path repository when cloning the superproject from $URL; it
   learned to also peek into $path for presence of corresponding
   repositories of submodules and borrow objects from there when able.
* "git ls-files" learned the "--recurse-submodules" option
   to get a listing of tracked files across submodules (i.e. this
   only works with the "--cached" option, not for listing untracked or
   ignored files).  This would be a useful tool to sit on the upstream
   side of a pipe that is read with xargs to work on all working tree
   files from the top-level superproject.
* "git clone --recurse-submodules" lost the progress eye-candy in
   a recent update, which has been corrected.


2.11.1
* "git push --dry-run --recurse-submodule=on-demand" wasn't
   "--dry-run" in the submodules.


2.12.0
* "git clone --reference $there --recurse-submodules $super" has been
   taught to guess repositories usable as references for submodules of
   $super that are embedded in $there while making a clone of the
   superproject borrow objects from $there; extend the mechanism to
   also allow submodules of these submodules to borrow repositories
   embedded in these clones of the submodules embedded in the clone of
   the superproject.
* "git grep" has been taught to optionally recurse into submodules.
* "git submodule push" learned "--recurse-submodules=only option to
   push submodules out without pushing the top-level superproject.
* A new submodule helper "git submodule embedgitdirs" to make it
   easier to move embedded .git/ directory for submodules in a
   superproject to .git/modules/ (and point the latter with the former
   that is turned into a "gitdir:" file) has been added.


2.13.0
* "git checkout" is taught the "--recurse-submodules" option.
* The output from "git status --short" has been extended to show
   various kinds of dirtiness in submodules differently; instead of to
   "M" for modified, 'm' and '?' can be shown to signal changes only
   to the working tree of the submodule but not the commit that is
   checked out.
* "what URL do we want to update this submodule?" and "are we
   interested in this submodule?" are split into two distinct
   concepts, and then the way used to express the latter got extended,
   paving a way to make it easier to manage a project with many
   submodules and make it possible to later extend use of multiple
   worktrees for a project with submodules.
* Fix for NO_PTHREADS option.
   (merge 2225e1ea20 bw/grep-recurse-submodules later to maint).
* "git diff --submodule=diff" learned to work better in a project
   with a submodule that in turn has its own submodules.
   (merge 17b254cda6 sb/show-diff-for-submodule-in-diff-fix later to maint).
* "git push --recurse-submodules --push-option=<string>" learned to
   propagate the push option recursively down to pushes in submodules.
* "ls-files --recurse-submodules" did not quite work well in a
   project with nested submodules.


2.13.2
* "git checkout --recurse-submodules" did not quite work with a
   submodule that itself has submodules.


2.14.0
* "git reset" learned "--recurse-submodules" option.
* "git diff --submodule=diff" now recurses into nested submodules.
* "git pull --rebase --recurse-submodules" learns to rebase the
   branch in the submodules to an updated base.
* Introduce a "repository" object to eventually make it easier to
   work in multiple repositories (the primary focus is to work with
   the superproject and its submodules) in a single process.
* "git checkout --recurse-submodules" did not quite work with a
   submodule that itself has submodules.


2.14.2
* "git push --recurse-submodules $there HEAD:$target" was not
   propagated down to the submodules, but now it is.
* "git clone --recurse-submodules --quiet" did not pass the quiet
   option down to submodules.


2.14.5
* Submodules' "URL"s come from the untrusted .gitmodules file, but
   we blindly gave it to "git clone" to clone submodules when "git
   clone --recurse-submodules" was used to clone a project that has
   such a submodule.  The code has been hardened to reject such
   malformed URLs (e.g. one that begins with a dash).


2.14.6
* CVE-2019-1349:
   When submodules are cloned recursively, under certain circumstances
   Git could be fooled into using the same Git directory twice. We now
   require the directory to be empty.


2.15.0
* "git grep --recurse-submodules" has been reworked to give a more
   consistent output across submodule boundary (and do its thing
   without having to fork a separate process).
* A test to demonstrate "git mv" failing to adjust nested submodules
   has been added.
   (merge c514167df2 hv/mv-nested-submodules-test later to maint).
* "git push --recurse-submodules $there HEAD:$target" was not
   propagated down to the submodules, but now it is.
* "git clone --recurse-submodules --quiet" did not pass the quiet
   option down to submodules.
* "git -c submodule.recurse=yes pull" did not work as if the
   "--recurse-submodules" option was given from the command line.
   This has been corrected.


2.15.1
* A broken access to object databases in recent update to "git grep
   --recurse-submodules" has been fixed.


2.16.0
* "git fetch --recurse-submodules" now knows that submodules can be
   moved around in the superproject in addition to getting updated,
   and finds the ones that need to be fetched accordingly.


2.16.2
* "git add -p" was taught to ignore local changes to submodules as
   they do not interfere with the partial addition of regular changes
   anyway.
* When resetting the working tree files recursively, the working tree
   of submodules are now also reset to match.


2.18.0
* Moving a submodule that itself has submodule in it with "git mv"
   forgot to make necessary adjustment to the nested sub-submodules;
   now the codepath learned to recurse into the submodules.
* "git pull --recurse-submodules --rebase", when the submodule
   repository's history did not have anything common between ours and
   the upstream's, failed to execute.  We need to fetch from them to
   continue even in such a case.
   (merge 4d36f88be7 jt/submodule-pull-recurse-rebase later to maint).


2.19.0
* Tests to cover conflict cases that involve submodules have been
   added for merge-recursive.
* The code to try seeing if a fetch is necessary in a submodule
   during a fetch with --recurse-submodules got confused when the path
   to the submodule was changed in the range of commits in the
   superproject, sometimes showing "(null)".  This has been corrected.


2.19.2
* When fsmonitor is in use, after operation on submodules updates
   .gitmodules, we lost track of the fact that we did so and relied on
   stale fsmonitor data.


2.20.0
* "git range-diff" did not work well when the compared ranges had
   changes in submodules and the "--submodule=log" was used.


2.21.0
* "git worktree remove" and "git worktree move" refused to work when
   there is a submodule involved.  This has been loosened to ignore
   uninitialized submodules.
* "git fetch --recurse-submodules" may not fetch the necessary commit
   that is bound to the superproject, which is getting corrected.
   (merge be76c21282 sb/submodule-recursive-fetch-gets-the-tip later to maint).


2.22.0
* Error message given while cloning with --recurse-submodules has
   been updated.
* Attempt to use an abbreviated option in "git clone --recurs" is
   responded by a request to disambiguate between --recursive and
   --recurse-submodules, which is bad because these two are synonyms.
   The parse-options API has been extended to define such synonyms
   more easily and not produce an unnecessary failure.


2.23.0
* "git clone --recurse-submodules" learned to set up the submodules
   to ignore commit object names recorded in the superproject gitlink
   and instead use the commits that happen to be at the tip of the
   remote-tracking branches from the get-go, by passing the new
   "--remote-submodules" option.


2.24.0
* "git fetch --jobs=<n>" allowed <n> parallel jobs when fetching
   submodules, but this did not apply to "git fetch --multiple" that
   fetches from multiple remote repositories.  It now does.
* "git grep --recurse-submodules" that looks at the working tree
   files looked at the contents in the index in submodules, instead of
   files in the working tree.
   (merge 6a289d45c0 mt/grep-submodules-working-tree later to maint).
* "git stash save" lost local changes to submodules, which has been
   corrected.
   (merge 556895d0c8 jj/stash-reset-only-toplevel later to maint).


2.25.0
* The interaction between "git clone --recurse-submodules" and
   alternate object store was ill-designed.  The documentation and
   code have been taught to make more clear recommendations when the
   users see failures.
* "git worktree add" internally calls "reset --hard" that should not
   descend into submodules, even when submodule.recurse configuration
   is set, but it was affected.  This has been corrected.
   (merge 4782cf2ab6 pb/no-recursive-reset-hard-in-worktree-add later to maint).


2.25.1
* "git grep --no-index" should not get affected by the contents of
   the .gitmodules file but when "--recurse-submodules" is given or
   the "submodule.recurse" variable is set, it did.  Now these
   settings are ignored in the "--no-index" mode.


2.25.2
* The "--recurse-submodules" option of various subcommands did not
   work well when run in an alternate worktree, which has been
   corrected.


2.26.0
* "git clone --recurse-submodules --single-branch" now uses the same
   single-branch option when cloning the submodules.
* A fetch that is told to recursively fetch updates in submodules
   inevitably produces reams of output, and it becomes hard to spot
   error messages.  The command has been taught to enumerate
   submodules that had errors at the end of the operation.
   (merge 0222540827 es/fetch-show-failed-submodules-atend later to maint).
* The "--recurse-submodules" option of various subcommands did not
   work well when run in an alternate worktree, which has been
   corrected.


2.27.0
* Fix "git checkout --recurse-submodules" of a nested submodule
   hierarchy.
   (merge 846f34d351 pb/recurse-submodules-fix later to maint).


2.28.0
* The effect of sparse checkout settings on submodules is documented.
   (merge e7d7c73249 en/sparse-with-submodule-doc later to maint).


2.30.0
* "git pull --rebase --recurse-submodules" checked for local changes
   in a wrong range and failed to run correctly when it should.
   (merge 5176f20ffe pb/pull-rebase-recurse-submodules later to maint).


2.30.1
* "git fetch --recurse-submodules" failed to update a submodule
   when it has an uninitialized (hence of no interest to the user)
   sub-submodule, which has been corrected.


2.34.0
* After "git clone --recurse-submodules", all submodules are cloned
   but they are not by default recursed into by other commands.  With
   submodule.stickyRecursiveClone configuration set, submodule.recurse
   configuration is set to true in a repository created by "clone"
   with "--recurse-submodules" option.
* The code to make "git grep" recurse into submodules has been
   updated to migrate away from the "add submodule's object store as
   an alternate object store" mechanism (which is suboptimal).
* "git grep --recurse-submodules" takes trees and blobs from the
   submodule repository, but the textconv settings when processing a
   blob from the submodule is not taken from the submodule repository.
   A test is added to demonstrate the issue, without fixing it.


2.35.0
* "git submodule deinit" for a submodule whose .git metadata
   directory is embedded in its working tree refused to work, until
   the submodule gets converted to use the "absorbed" form where the
   metadata directory is stored in superproject, and a gitfile at the
   top-level of the working tree of the submodule points at it.  The
   command is taught to convert such submodules to the absorbed form
   as needed.
