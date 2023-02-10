# 300 - Setup semantic-release

Browse to "Semantic-Release CLI" at https://github.com/semantic-release/cli

Semantic release command-line interface (cli) will help us to set up everything. 

Make sure we have pulled the latest edition of our repository locally:

```
$ git pull
```

**NOTE**: If you do not yet have an NPM Token, create one following these instructions, https://docs.npmjs.com/creating-and-viewing-access-tokens#creating-access-tokens. See also https://github.blog/2021-08-23-npm-registry-deprecating-tls-1-0-tls-1-1/

If you see a TLS error message instead, we encourage you to upgrade to a currently supported version of Node.js and the latest version of npm v7.

Also set the URL to the NPM Registry to use the **secure** https, instead of the unsecure http:

```
$ npm config set registry https://registry.npmjs.org/
```

Check is above configuration change was successful with:

```
$ npm config list
```

You should see:

```
registry = "https://registry.npmjs.org/"
```

Now create the NPM token **in a new Terminal window**.

```
$ npm login
```

Provide your NPM password when requested.

Next:

```
$ npm token create
```

In response you will be prompted as follows:

```
cidr_whitelist

readonly: false
automation: false
created: DATE AND TIME OF CREATION
token: YOUR NPM TOKEN
```

**TIP**: Keep your token somewhere safe for future reference.

First, install semantic-release cli as a dev dependency, as follows, at the package.json level of your repository:

```
$ npm install semantic-release-cli --save-dev
$ semantic-release-cli setup
```

You will be prompted as follows:

```
$ ? What is your npm registry? (http://registry.npmjs.org/)
```

Enter https://registry.npmjs.org and hit ENTER to choose the **secure** version of http://registry.npmjs.org/.

```
$ ? Which authentication method is this npm registry using? (Use arrow keys)
> Token based
  Legacy (username, password, email)
```

Use keyboard up/down arrow keys to move the ```>``` to Token and hit ENTER to choose Token

```
$ ? What is your npm username?
```

Type your npm username (here: wvanheemstra) and hit ENTER

```
$ ? What is your npm password? [input is hidden]
```

Type your npm password (minimal 10 characters) and hit ENTER

```
$ ? What is your NPM two-factor authentication code? 
```

Look in your email inbox for the email address attached to your NPM account and find the One-Time-Password (OTP) from the most recent email sent to you by NPM (an 8-digit numeric number). Enter this 8-digit numeric number and hit ENTER.

```
$ ? Provide a GitHub Personal Access Token (create a token at https://github.com/settings/tokens/new?scopes=repo)
```

Follow this link https://github.com/settings/tokens/new?scopes=repo in your browser to create such a GitHub Personal Access Token whereas the scope is set to **repo** thus including all access option for repo, and keep it safe to be pasted here. Hit ENTER.

```
# ? What CI are you using? (Use arrow keys)
  Travis CI
  Travis CI Pro
  TRAVIS CI Enterprise
  Circle CI
> GitHub Actions
  Other (prints tokens)
```

Use keyboard up/down arrow keys to move the ```>``` to GitHub Actions and hit ENTER to choose GitHub Actions

Above setup will automatically create a new secret inside of this repository. You will not be prompted anymore. 

You can check it by going to the ```Settings``` tab of your repository, from the left-hand side menu choose "```Secrets and variables```", then "```Actions```". An entry by the name of "**NPM_TOKEN**" will have been added under the ```Secrets``` tab.

```
NPM_TOKEN
```

So let's continue.

Browse the ```package.json``` file and witness that Semantic Release has already renamed the version from what it was before (e.g. 0.1.0) to the semantic naming, e.g.:

```
...

"version": "0.0.0-development",
...
```
package.json

We no longer need to care about the version, semantic release will do that for us : )

Then if we keep scrolling you will see that within ```scripts``` it also added this semantic release over here. 

```
...
  "scripts": {
     ...
    "semantic-release": "semantic-release"
...
```
package.json

We will need then to say the branches that we want to release from, because by default semantic release will only do the publish from the master branch.

In our case we are using the ```main``` branch, so let us just add ```--branches main``` before we forget about it.

```
...
  "scripts": {
     ...
    "semantic-release": "semantic-release --branches main"
...
```
package.json

If you keep scrolling to the bottom of ```package.json``` we see a few more changes. One is the addition of the npm package ```semantic release``` to the development dependencies.

```
...
  "devDependencies": {
    ...
    "semantic-release": "^20.1.0"
  },
...
```
package.json

And then it has added our repository over here:

```
...
  "repository": {
    "type": "git",
    "url": "https://github.com/vanHeemstraSystems/your-package-name-you-want-to-see-on-npm-lol.git"
  }
...
```
package.json

Now, lets commit our changes as follows:

```
$ git add . && git commit -m "add semantic-release" && git push
``

You will see that semantic release will require a specific commit message format and that's based on the Angular Commit Message Conventions.

See https://github.com/semantic-release/semantic-release#how-does-it-work

Now you start to probably thinking ```oh that's even more complicated than keeping versions```. We agree, so that's the reason that we have another tool called **commitizen**

Let's go to the next section, which will explain all about **commitizen**.
