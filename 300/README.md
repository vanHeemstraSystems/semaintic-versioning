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

We can change it to for example quality, checks quality, any name you want. We will just rename it to ```quality```, because we are going to do the unit testing, the linting everything that you want to validate before you commence with the npm publish.

```
...
jobs:
  quality:
...
```
.github/workflows/publish.yml

Now the first thing that we need to check over here is these runs: it's running now on ubuntu the latest version.

```
...
jobs:
  quality:

    runs-on: ubuntu-latest
...
```
.github/workflows/publish.yml

You might want to run this in multiple versions of your operating system so if you really want to do that you can come over strategy / matrix and this matrix has all the options that exist. You can add a new line called ```os``` and we will provide it with ```ubuntu-latest``` and ```windows-latest```. You can also decide to add mac os latest (i.e. ```macos-latest```) if you want to, as we did. Adding those three now means our operating systems available in this matrix are ubuntu latest, windows latest, and mac os latest.

```
...
jobs:
  quality:

    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [14.x, 16.x, 18.x]
        os: [ubuntu-latest, windows-latest, macos-latest]
        # See supported Node.js release schedule at https://nodejs.org/en/about/releases/
...
```
.github/workflows/publish.yml

Now the only change we need to do is for ```runs-on``` to replace its previous content (```ubuntu-latest```) with ```${{ matrix.os }}```:

```
...
jobs:
  quality:

    runs-on: ${{ matrix.os }}
...
```
.github/workflows/publish.yml

So this matrix now has three operating systems and three versions of node (```14.x, 16.x, 18.x```), so we are going to create nine possible jobs: every single version of node to ubuntu latest, windows latest, and mac os latest so we will have nine jobs running.

We can start to look into what really matters for us, which is the steps.

```
...
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
...

```
.github/workflows/publish.yml

First one is just to clone and check out our branch so this one is very needed.

The second one is just to set up node.js and as you can see it's already using that matrix for the node version that we are using

Then we have our run commands:

- The first one is the npm ci, which is similar to npm installed.

- Then we are building this library.

- Lastly, we are running tests and you can run a lot of other stuff over here.

Commit the changes we have applied to ```publish.yml```. You can see that if you go now to the Actions tab, it will have started already a new action and this action will take anywhere from one minute to five minutes more or less.

The more operating systems and the more versions of node.js you put the more jobs will run. If you are in a public repository is not a big deal, but if you are in a private repository you have only 2 000 minutes free per month and after that amount you will start to be charged for it.

**NOTE**: You may find that a combination of an operating system and a node version fails, with the following error:

```
npm ERR! The `npm ci` command can only install with an existing package-lock.json or
npm ERR! npm-shrinkwrap.json with lockfileVersion >= 1. Run an install with npm@5 or
npm ERR! later to generate a package-lock.json file, then try again.
```

Follow the advice given and first generate the ```package-lock.json``` as follows, inside the directory of ```package.json``` run:

```
$ npm install
```

Commit the newly created file ```package-lock.json``` and the actions should start automatically. Check if now all succeed, from the Actions tab.

Now the next step we are going to set up is: semantic release.

## 300 - Setup semantic-release


WE ARE HERE ....


## 400 - Setup commitizen


## 500 - Create publish job inside GitHub Actions using semantic-release


## 600 - How to handle Pull Requests and Merges in order to keep semantic-release "happy" :)

