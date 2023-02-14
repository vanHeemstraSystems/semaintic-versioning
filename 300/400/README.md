# 400 - Setup commitizen

**WARNING**: Make sure you have **Node** version 18 or newer.

```
$ node --version
```

You can upgrade **Node** as described at https://blog.hubspot.com/website/update-node-js

First, install the Commitizen CLI tools:

```
$ npm install --save-dev commitizen
```

They have a way for us to set it up, which is:

```
$ npx commitizen init cz-conventional-changelog --save-dev --save-exact
```

As soon as we let it run, which will be two or three minutes, but as soon as that finishes go to our ```package.json```.

Add a command called ```commit``` to package.json.

```
...
"scripts": {
  ...
  "commit": "git-cz",
  ...
},
...  
```
package.json

You should still type ```git add .``` to add any changed files to your staging, before you commit.

```
$ git add .
```

However, instead of next typing ```commit```, we will be typing ```npm run commit``` from now on.

```
$ npm run commit
```

Now ```git-cz``` will run and you will get these very nice message helpers in your terminal window.

You will be prompted as follows:

```
? Select the type of change you are committing:
...
```

So, let's say that we added a new **feature**, whatever feature that was. 

From the menu, move the arrow to ```feat: A new feature``` using the up/down arrow keys and press ENTER.

Next, you will be prompted as follows:

```
? What is the scope of this change (e.g. component or file name): (press enter to skip)
```

Let's say that feature is part of you creating a blog, and it's in the user settings that you've changed something. 

So you will enter ```user-settings``` and click ENTER.

Again, you will be prompted:

```
? Write a short, imperative tense description of the change (max 79 chars):
  (0)
```

Whilst you type a description the counter will go up to stay within the maximum of 79 characters. Type something like: ```Add avatar to user-settings.``` and press ENTER.

The next prompt:

```
? Provide a longer description of the change: (press enter to skip)
```

You can either skip this or type for example: ```Add the possibility for a user to add their avatar in user-settings.``` and press ENTER.

Now, when prompted:

```
? Are there any breaking changes? (y/N)
```

As there are no broken changes caused by our example change, we just click ENTER, which by default enters N for No.

Finally, the last prompt:

```
? Does this change affect any open issues? (y/N)
```

Should we choose y for Yes, than we can type the issue numbers this change addresses, it will put a nice link between your release and the issues that you fixed. If none are affected, simply click ENTER and we will see that our commit gets executed.

Now we can do a git push:

```
$ git push
```

You will see that all of those changed files are now there on GitHub. See https://github.com/vanHeemstraSystems/your-package-name-you-want-to-see-on-npm-lol
