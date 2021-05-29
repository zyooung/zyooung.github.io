### Work with GitHub (Multiple Accounts)

#### Step 1 - Create a New SSH Key

Generate a unique SSH key for our second GitHub account.

```bash
ssh-keygen -t rsa -C "your-email-address"
```

Don't override the existing key. Instead, when prompted, save the file as id_rsa_COMPANY. 

#### Step 2 - Attach the New Key

Next, login to GitHub account, browse to "Account Overview," and attach the new key, within the "SSH Public Keys" section. To retrieve the value of the key that you just created, return to the Terminal, and type: vim ~/.ssh/id_rsa_COMPANY.pub. Copy the entire string that is displayed, and paste this into the GitHub textarea. 

Next, because we saved our key with a unique name, we need to tell SSH about it. Within the Terminal, type: 

```bash
ssh-add ~/.ssh/id_rsa_COMPANY
``` 

#### Step 3 - Create a Config File

Now we need a way to specify when we wish to push to our personal account, and when we should instead push to our company account. To do so, create a config file.

```bash
touch ~/.ssh/config
```

Paste in the following snippet.

```
Host github.com

  HostName github.com

  User git

  IdentityFile ~/.ssh/id_rsa
```

This is the default setup for pushing to our personal GitHub account. Notice that we're able to attach an identity file to the host. Let's add another one for the company account. Directly below the code above, add:

```
Host github-COMPANY

  HostName github.com

  User git

  IdentityFile ~/.ssh/id_rsa_COMPANY
```

This time, rather than setting the host to github.com, we've named it as github-COMPANY. The difference is that we're now attaching the new identity file that we created previously: id_rsa_COMPANY. Save the page and exit!

#### Step 4 - Push/pull remote

Set the remote URL with the host name set up in Step 3:


```bash
git remote add origin git@github-COMPANY:Company/testing.git

git push origin master
```

Note that, this time, rather than pushing to git@github.com, we're using the custom host that we create in the
config file: git@github-COMPANY.
