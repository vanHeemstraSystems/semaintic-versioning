# 100 - Create project using tsdx and git push to GitHub

In a terminal create a new npm project as follows:

```
$ npx tsdx create your-package-name-you-want-to-see-on-npm-lol
```

When asked for a template:

```
? Choose a template ...
> basic
  react
  react-with-storybook
```

Choose **basic**.

After npx has created the directory and some files, move inside the newly created directory:

```
$ cd your-package-name-you-want-to-see-on-npm-lol
```

Now open your project in Visual Studio Code by typing:

```
$ code
```

From the previous step, already a directory called ```.github``` was created for you. We will now delete this folder, to create it manually.

```
$ rm .github
```

At this stage go into GitHub and create a new repository (with any name, it doesn't necessarily need to have the same name as our package). For simplicity we name it the same as our package:

**NOTE:** At this point do **not** create a README.md file (or any other content) yet as this will collide with the files you are about to push to this empty repository later.

```
https://github.com/vanHeemstraSystems/your-package-name-you-want-to-see-on-npm-lol
```

Now on the terminal inside the directory run the following commands to connect this project to the newly created GitHub repository:

```
$ cd your-package-name-you-want-to-see-on-npm-lol
$ git init
```

Adhering to modern best practices, we will assure the current branch is not called ```master```, but instead ```main```.

```
$ git branch -m main
```

Add all files to your new branch as follows:

```
$ git add .
```

Commit your first changes:

```
$ git commit -m "first commit"
```

Next, set the remote:

```
$ git remote add origin git@github.com:vanHeemstraSystems/your-package-name-you-want-to-see-on-npm-lol.git
```

Followed by a push:

```
$ git push -u origin main
```

If an error occurs, you may want to set tracking information for this branch first, like so:

```
$ git branch --set-upstream-to=origin/main main
```

Then try the following again:

```
$ git push -u origin main
```

If you now refresh the GitHub page of the repository you will see your code there:

https://github.com/vanHeemstraSystems/your-package-name-you-want-to-see-on-npm-lol
