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

## 200 - Create our first GitHub Action


From the previous step, already a directory called ```.github``` was created for you. We will now delete this folder, to create it manually.

```
$ rm .github
```

At this stage go into GitHub and create a new repository (with any name, it doesn't necessarily need to have the same name as our package). For simplicity we name it the same as our package:

```
https://github.com/vanHeemstraSystems/your-package-name-you-want-to-see-on-npm-lol
```

Now on the terminal inside the directory run the following commands to connect this project to the newly created GitHub repository:

```
$ cd your-package-name-you-want-to-see-on-npm-lol
$ git init
```





MORE ...

## 300 - Setup semantic-release


## 400 - Setup commitizen


## 500 - Create publish job inside GitHub Actions using semantic-release


## 600 - How to handle Pull Requests and Merges in order to keep semantic-release "happy" :)

