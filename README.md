This is an application that copies its code to your GitHub profile. 

### How it works?

You click the link: <br>
https://github-replication-app.herokuapp.com/ <br>

And it takes you to GitHub authentication page, where you can log in to your Github profile.
The code then gets automatically copied to a newly created **self_replicating_github_app** public
repository in your GitHub.


### How to create the same app?


If you want to make the same app, below are instructions to make this happen.
You already have the most important part - the code - in your GitHub.

#### First, let's spin up an app server

If you have never done this before, please don't be afraid. 
There are solutions that make it easy and I will explain how it's done with heroku.com service.
You will need an account with them -- a free one works perfect. 
After you log in, on the start page you will see an option to create a new application. 
Click the **New** button (in the upper right corner) and then select **Create new app**. 
Fill in the fields and click **Create app**.

Almost there :)

You're now in the **Deploy** pane. 
Select the "Connect to GitHub" tile, link your GitHub account by following the onscreen instructions,
and then paste **self_replicating_github_app** as the name of your repository.
You can enable automatic deploys and then click **Deploy Branch**.
The build process will start...

If the build fails, you have a Troubleshooting section below at your disposal.

By the way, your app already has its own URL! 
You can get it in the **Settings** pane from the **Domains** section.
Now let's go there and copy the application link to prepare for the next step.

#### Second, let's set up environment variables

Although it might sound complicated, the process is straightforward and 
does't require any special technical skills. 
The variables that we need are for the GitHub authentication flow, 
and this is the page where you can get them: <br>
https://github.com/settings/applications/new

Pick a comprehensible name and put a few words into the description -- that's the hardest part.
In the **Homepage URL** field, put the full link to your application that 
you copied from the **Settings** pane earlier. <br>

Let's suppose you have `https://my-first-app.herokuapp.com/` as your **Homepage URL**.<br>
In the **Authorization callback URL**, put the same application link and add `/replicating_code` in the end.<br> 
So that you will have `https://my-first-app.herokuapp.com/replicating_code` as the callback URL. <br>

After the registration, you will get the **Client ID** and the **Client Secret**. 
That's what we're going to set as environmental variables. 

Let's go back to our heroku app, the same familiar **Settings** pane 
and click **Reveal Config Vars** button in the **Config Vars** section.
You will see two blank fields: KEY and VALUE. To set up **Client ID**, 
put `client_id` into the KEY field and its value (alphanumeric code you got from GitHub) into the VALUE field. 
For **Client Secret**, the KEY is `client_secret` and the VALUE is the code you got from GitHub.

You're all set! Now you have a working link to _your_ application, which is the URL from the **Settings** pane.

One more thing...

#### Troubleshooting

Yeah, things don't always go smoothly and you need to be prepared. 
In case something goes wrong on heroku's side, you can see this in the application logs.
To do this, install heroku command line tool, which is intuitive to use: <br>
https://devcenter.heroku.com/articles/heroku-cli

After login (`heroku login` command), you can see the logs for your application. 
Let's use the example name of the application mentioned above, my-first-app.
To see its logs, you would need to type `heroku logs -a my-first-app`. 

If something went wrong, you will see words like `Error` and `Traceback` in the console output.
If you don't know how to fix the issue, search for the error message in the Internet. 
Most probably, you encountered a common problem that already has a solution. 
Heroku also has error codes that help you understand the issue better:<br>
https://devcenter.heroku.com/articles/error-codes

Talking of the errors, there is a frequent issue when heroku doesn't provide 
a web server for your app (which you need). The error looks like this in logs:
`H14 error in heroku - “no web processes running”`

It's easily fixable, though, with just one line in console:
`heroku ps:scale web=1 -a my-first-app`

### What else you can do with the app?

Well, you can use the app to copy the code of any public repo in GitHub. 
What you need, is open app.py file and assign a new value for the `REPO_WITH_APP_CODE` variable.
To work properly, it should be a github username followed by the repository name, 
like `'alisa-test/self_replicating_github_app'`. Commit your changes to GitHub and 
deploy the changed code to your app server (unless you enabled those convenient automatic deploys). 

Have Fun!

____

If you have read until this, you might be interested in 
the technical specification for this project, you nerd!

It's here, in a [Google Doc](https://docs.google.com/document/d/1cx0FohDNI9EP5bybJ_hh9nxaztiKvt_zSnMioeu3cSg/edit?usp=sharing)
