# 400 - Setup commitizen

MORE  ...





right i
11:34
never know how to type communism so
11:37
google will help me out and when you
11:39
have communism
11:41
you can go over here and set up
11:43
committees and and committees and will
11:45
open
11:46
a window like this every time that you
11:48
do get cz
11:49
it will open a very very nice window so
11:52
it will help you with your commits
11:54
and you don't need to know all of those
11:56
tedious
11:57
messages out of your head and so let's
12:00
go over here to
12:02
npx and they have a way for us to set it
12:05
up
12:05
which is over here npx comet is an
12:09
init and we will just copy that and you
12:12
will see that
12:12
as soon as i copy that and let it run
12:15
which will be another
12:16
two or three minutes so another fast
12:18
forward but as soon as that finishes
12:21
we will be able to go to our
12:23
package.json
12:24
and add over here into our package.json
12:27
i'm sorry
12:28
over here into our package.json another
12:31
command called commit
12:32
and that commit we'll just do git cc
12:36
so commit and i will just do git cz
12:40
right there right and now i can go back
12:43
to my terminal
12:44
and it didn't finish yet so right now i
12:47
will fast forward this for you
12:49
right now when it finished you can still
12:51
do your pit. like you were doing before
12:54
but now instead of doing git commit we
12:56
will do
12:57
npm run commit and when you do this
13:00
npm run commit now git cz will run let
13:03
me just run this again
13:05
git cz will run and you will get these
13:08
very very nice message helpers for you
13:11
so
13:11
let's say that we added a new feature
13:14
whatever feature that was
13:15
and let's say that feature you are
13:17
creating a blog
13:18
and it's on the user settings that you
13:21
change something so you will do
13:23
user settings you will click enter and
13:25
now over here you can put a message
13:27
so we add a new picture
13:31
to the user for example i will click
13:33
enter
13:34
then i don't want a longer message you
13:36
can say that
13:38
if you have breaking changes or not
13:39
because this will impact the way that
13:41
semantic release will create the version
13:43
of your package
13:44
in my case i will say no which is the
13:46
default i will say that
13:48
it doesn't affect any open issues but if
13:50
it does you
13:51
you can say the issue number and then
13:54
when it creates the release for you
13:56
it will put a nice link between your
13:58
release and the issues that you fixed
14:00
now that that thing happened i can do a
14:03
git push
14:04
and you will see that all of those files
14:06
are now over there on github action on
14:09
github
14:10
we can go over here to our github
14:12
actions right now so
14:14
i will just go to my code and i will
14:17
open
14:18
our workflows folder the publish yaml
14:21
file
14:21
and i will click on the edit button and
14:24
over here you will see
14:26
why i love to use this bit because if
14:28
you come over here
14:30
you have all the helpers that you might
14:32
want to have
14:33
so i will call this next job i will call
14:36
it the publish
14:37
job itself so i will do publish i will
14:40
click
14:41
now enter and over here if i do control
14:44
space
14:45
you can see that i have autocomplete for
14:48
everything
14:48
i might want to have i will say that it
14:51
will run for example
14:52
on ubuntu latest and i will also say
14:56
that
14:56
in this specific job i will need the
14:59
previous job
15:00
to be finalized in this case the quality
15:03
job so
15:04
if i unit test files into our quality
15:07
job
15:08
over here i don't want my publish job to
15:10
run
15:11
right in a second i will also add
15:14
an if over there in order to only
15:17
run these if we are in master
15:20
okay so in case we are in in a pull
15:23
request
15:24
like i'm saying here let's say we are in
15:26
a pull request to master
15:27
this will run in the branch so i don't
15:29
want to publish from that branch
15:31
i really want to publish when the commit
15:33
is on master
15:34
not when there is a pull request to
15:36
master so we will add that if in a few
15:38
seconds
15:39
but before we add that if now we are in
15:42
a
15:42
very good stage to say the steps and so
15:46
let's just do the steps and in those
15:49
steps
15:50
i will say the same thing that we said
15:51
before i will use
15:53
the checkout and i will set the
15:56
environment for node.js
15:58
so let me just come over here do a
16:00
control v
16:01
and at this stage the last bit we want
16:03
to do is
16:04
npmci just to install our packages
16:08
and as you can see on the right side of
16:10
the screen
16:11
you can have a cache over there so if
16:14
you feel
16:15
that doing npmci in two different stages
16:18
of your process
16:19
is making stuff a little bit slower you
16:22
can use this
16:23
action over there called cache and it
16:26
will
16:26
keep your node modules into cache if you
16:28
want to right
16:30
now the next step after we do the npmci
16:33
will be to run let me just remove these
16:36
spices
16:37
will be to run semantic release
16:40
right and now as we have this we will
16:43
run semantic release
16:44
semantic release will understand the
16:46
commits that we have and decide the next
16:48
version to run
16:50
before we just commit this bit let's
16:52
just go
16:53
over here and as you can see in this
16:56
context i will leave all of these urls
16:58
into the video description if you want
16:59
to investigate it a bit more
17:01
yourself right but we can have this if
17:04
that i had already highlighted
17:06
and once again we will have autocomplete
17:10
for this but what's happening over here
17:12
is just
17:12
myself checking if the reference where
17:15
we are on
17:15
is the mind branch and if it is i want
17:18
to run my action
17:20
so i can come over here after the runs
17:23
on
17:23
i will put that if and as i was saying
17:26
to you if i do github dot
17:28
as you can see i have all of the
17:30
autocompletes that you might want to
17:31
have
17:32
and that's the main reason i run
17:35
all my actions code inside this little
17:38
editor
17:39
okay now that we have all of them and
17:42
i think we have everything to publish
17:44
the first version
17:46
of our package so let's do a commit
17:49
let's just say something over here
17:51
added publish job for example
17:54
right i will commit that one and now
17:57
if i go to the actions we will see if it
18:00
will run
18:01
or not it might run it might fail we
18:04
will see
18:05
and then we will fix it we can already
18:08
see that our action failed so we can go
18:10
inside and see what it felt and you can
18:14
click
18:14
on the job click once again and we can
18:17
see that
18:18
it failed so let's just read the error
18:20
can only install packages when your
18:22
package.json and package log
18:24
or are in sync please update your log
18:27
file
18:27
with an npm installed so let's just do
18:30
that
18:30
let's just do an npm first a git pool
18:34
then an npm install this once again will
18:36
take
18:37
a few minutes to run
18:41
now we can commit this again and
18:44
we will see that our actions will then
18:48
run
18:48
so i will just do an asd
18:52
in a fix i will just say asd isd in the
18:55
commit
18:56
i really don't care that much about the
18:58
commit message
18:59
at this stage right i just want to push
19:01
it
19:02
to then see our action to run so if i
19:05
come
19:06
over here and i now click on actions and
19:08
other actions started
19:10
we can click over here and hopefully
19:13
this time all our actions will run and
19:16
when they run we will have a version on
19:19
npm
19:22
to be honest even before it finished i
19:24
am already 100 sure it will fail
19:27
because we didn't put our npm underscore
19:29
token
19:30
as the environment variable so while
19:32
this thing
19:33
will run and i'm 100 sure it will file
19:37
we can go already into here open
19:40
our github actions in
19:44
our vs code and the only thing i'm going
19:46
to do
19:47
over here at the bottom will be to have
19:49
an environment
19:51
and that environment we will just do the
19:53
following
19:54
oops one two i will say npm
19:58
token column and then
20:01
i will just say the secrets secrets
20:04
dot npm underscore oops
20:08
underscore token npm token so let's put
20:11
this one
20:12
secrets dot npm uh gita
20:16
git up token we can even copy paste
20:20
to avoid any typo i will save this one
20:24
we can now come on to our command line
20:28
do our run acp
20:31
we can even say that it was a fix
20:34
package
20:34
json and now add add git
20:38
up token just to have a better message
20:42
for once and now this one
20:45
will commit and now we can go
20:48
over here to our actions click in
20:51
actions click on this one and
20:55
wait for it to run once again
20:59
and as you can see now we have a
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

