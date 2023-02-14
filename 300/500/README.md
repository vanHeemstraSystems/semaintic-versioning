# 500 - Create publish job inside GitHub Actions using semantic-release

Back in GitHub (https://github.com/vanHeemstraSystems/your-package-name-you-want-to-see-on-npm-lol), go to the GitHub Action we created earlier:

```
$ cd .github/workflows/publish.yml
```

Add a new line to the bottom of the file called **publish:** as follows, at the same indentation level as ```quality```:

```
...
  quality:
    ...
...
  publish:
```
.github/workflows/publish.yml


If after ```publish:``` you enter a Next Line (with ENTER) and CTRL + Spacebar you'll get a list of all commands that you want to have as auto-complete.

We type the following after **publish:**:

```
...
  quality:
    ...
...
  publish:
    runs-on: ubuntu-latest
    if: ${{ github.ref == 'refs/heads/main' }}
    needs: [quality]
    steps:
    - uses: actions/checkout@v3
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v3
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'
    - run: npm ci
    - run: npm run semantic-release
      env:
        NPM_TOKEN: ${{ secrets.NPM_TOKEN }}
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```
.github/workflows/publish.yml

Semantic release will understand the commits that we have and decide the next version to run.

Now commit our changes to .github/workflows/publish.yml


In the Actions tab in GitHub you can follow the process of where the new code will be qualified and is successfull pushed to NPM registry with the publish section.

**NOTE**: If the ```publish``` section fails with below error:

```
Run npm run semantic-release

> your-package-name-you-want-to-see-on-npm-lol@0.0.0-development semantic-release
> semantic-release --branches main

[semantic-release]: node version >=18 is required. Found v16.19.0.

See https://github.com/semantic-release/semantic-release/blob/master/docs/support/node-version.md for more details and solutions.
Error: Process completed with exit code 1.
```

Then, remove the Node versions (here: 16.x) that are incompatible with Semantic Release from your matrix:

```
...
jobs:
  quality:

    runs-on: ${{ matrix.os }}

    strategy:
      matrix:
        node-version: [16.x, 18.x] <-- REMOVE 16.x !!!
...        
```
publish.yml

Now commit your changes and push again to see if the automation of publish now succeeds.


WE ARE HERE

As you can see now we have a
21:01
successful job
21:02
we can even now go to our code and
21:05
if you click over here you can see that
21:07
we have releases over there
21:10
i will click on the releases and now you
21:12
can see
21:13
all the stuff that we did for those
21:15
releases
21:16
you can see that we have a proper change
21:19
log
21:20
of what happened in our release so if we
21:22
have a branch
21:23
let's say called development or
21:26
something like that
21:27
and you are putting a lot of features
21:29
there and a lot of bug fixes
21:31
every time that you then merge it into
21:33
the main branch
21:34
you will have a very nice change lock in
21:37
your releases which is very very nice
21:40
now you might be asking bruno show me it
21:42
on
21:43
npm so let's go to npm now npm js
21:47
and i will put this over here and
21:51
i will now get oops i probably pasted
21:54
something wrong
21:55
let me just do enter
21:58
sign in i will sign in with my username
22:03
and it should be inside my account so i
22:07
will come
22:07
over here let me just say save yes
22:10
yes google chrome save it for me i will
22:13
have
22:14
my profile and as you can see
22:18
it's already there right i can click
22:21
on this one and now i have version
22:25
1.0.0 now before we finish this video i
22:28
want to show you how to do
22:30
a pull request and more importantly is
22:32
how you can
22:33
approve that pull request in order for
22:35
semantic release to pick it up
22:37
so let's just create a new file over
22:39
here
22:40
let's come over into our vs code
22:43
change something in our index let's say
22:47
i love you all and i will just do this
22:51
i will say this is now a feature right
22:54
and i will do the folding gita dot git
22:57
check
22:58
out minus b fit slash
23:02
new message right and now that we have
23:06
that i can do our typical
23:09
npm run acp all right
23:12
and i will just say it's a new feature
23:15
and it's on the file index.dsx
23:19
and i will just write a short message
23:21
add a new message
23:23
saying i love you all
23:26
enter enter enter let's just do this
23:29
oops git push and now
23:33
that oops good job bruno it's a very
23:36
good job
23:38
so let me just delete this now we are
23:40
pushing our branch
23:42
and i will open the pull request so
23:44
let's come
23:45
over here where we are going to open the
23:48
pull request so i will go to code
23:51
i will create and compare and now i will
23:53
just
23:54
say create the pull request and now
23:57
when you merge you need to be very very
23:59
careful when you merge
24:01
you need to click here and you will need
24:03
to say
24:04
rebase and merge okay because if you
24:08
just
24:08
say all comments from this branch will
24:11
be
24:11
added to the base branch via a merge
24:14
commit so
24:15
we will lose all our nice messages so if
24:18
you do this
24:18
then semantic release will not pick it
24:20
up okay
24:22
if you just do rebase and merge which is
24:25
something that i set by default usually
24:27
then when you rebase and merge semantic
24:31
release will pick it up
24:32
and run everything for us so
24:35
as you will see i will just wait for
24:37
this to finish i will click
24:39
merge the display well not much i will
24:42
say rebase and merge and click that
24:44
button
24:44
and then i will show you one npm that
24:46
new version now that all our checks
24:48
passed
24:49
we can come over here click on rebuys
24:51
and merge
24:52
click to rebuy then merge confirm rebuys
24:56
and merge
24:56
this will be merged into our main and
24:59
now if you
25:00
open our actions over here that run in
25:03
that specific branch as you can see
25:05
in fit slash new message which was our
25:08
branch
25:08
you can see that publish was skipped and
25:11
it was kept because of that
25:12
if we added at the beginning saying
25:15
github dot refs
25:16
equals equals to our main branch right
25:19
so our publish didn't run now we can go
25:23
back to our repository come
25:26
into our default branch right
25:29
and when this becomes a check we can go
25:33
into our npm package do a force refresh
25:37
and you will see that we will have
25:38
a version different from 1.0.0
25:42
as you can see we already have a green
25:44
peak so i can come
25:45
to my package and now if i refresh
25:48
you will see that we will have a new
25:51
version from our package
25:53
and that version should be 1.1.0 because
25:55
we added a new feature
25:57
if we had done a breaking change it
25:59
would have become
26:01
2.0.0 or in the case of a bug fix
26:05
1.0.1 alright
26:07
so i really hope you enjoyed this video
26:09
if you have any question or any
26:11
suggestion on how to improve this
26:13
let me know in the comments i will try
26:15
to answer all your questions
26:16
and without anything else to say i
26:19
really hope you enjoyed this
26:20
and i see you in the next one bye bye

