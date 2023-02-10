# 300 - Building Our Application

## 100 - Create project using tsdx and git push to GitHub

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

## 200 - Create our first GitHub Action

The next step is to create our **GitHub Action** so go to the tab called "Actions" along the top of the repository page on GitHub and click on it.

Search for a GitHub Action that is called **Node.js**:

```
Node.js
By GitHub Actions

Node.js logo
Build and test a Node.js project with npm.
```

On this card click **Configure**.

A brand new file at ```.github/workflows/node.js.yml``` is opened automatically for you to start editing.

```
# This workflow will do a clean installation of node dependencies, cache/restore them, build the source code and run tests across different versions of node
# For more information see: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs

name: Node.js CI

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:

    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [14.x, 16.x, 18.x]
        # See supported Node.js release schedule at https://nodejs.org/en/about/releases/

    steps:
    - uses: actions/checkout@v3
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v3
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'
    - run: npm ci
    - run: npm run build --if-present
    - run: npm test
```
.github/workflows/node.js.yml

As a manner of best practise, rename the file to ```publish.yml``` and save it at its location by clicking **Start commit**, using the default values.

We will now come back to this saved file ```publish.yml``` to make a few changes:

If we wanted to trigger our GitHub Action by a pull request on other branches than ```main```, we would make a change like so:

```
...
on
...
  pull_request:
    branches: [ "main", "other-branch", "yet-another-branch" ]
...
```
.github/workflows/publish.yml

Equally, to have the GitHub Action run on pull requests on *any* branch, set it to '\*' without brackets, like so:

```
...
on
...
  pull_request:
    branches: '*'
...
```
.github/workflows/publish.yml

For now, we will just leave it to be set to ```main``` only.

Okay then the first thing that we have over here is jobs where ```build``` is the name of our job.

```
...
jobs:
  build:
...
```
.github/workflows/publish.yml

We can change it to for example quality, checks quality, any name you want. We will just rename it to ```quality```, because we are going to do the unit testing, the linting everything that you want to validate before you commence with the git publish.

```
...
jobs:
  quality:
...
```
.github/workflows/publish.yml










MORE ...

## 300 - Setup semantic-release


## 400 - Setup commitizen


## 500 - Create publish job inside GitHub Actions using semantic-release


## 600 - How to handle Pull Requests and Merges in order to keep semantic-release "happy" :)

