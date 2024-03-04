# Getting Started

## Installing software
Makre sure you have Git and Python installed on your PC. Open your terminal and type:
```
git --version
```
If you do not have git installed it can be downloaded from:
> https://git-scm.com/download/win

Make sure you have Python installed on your PC. You can check if python is installed with this command:
```
python --version
```
Otherwise, it can be installed from:
> https://www.python.org/downloads/

Install the IDE, Visual Studio Code:
> https://code.visualstudio.com/

## Signing up for GitHub
If you do not have a GitHub account, create one for yourself at:
> https://github.com/signup

# Objectives
## 1. Creating a Python example app
Create a new folder in your documents folder named `python-example-app`. Open the folder in Visual Studio Code.

Add all of the files found in this repository:
* `api/index.py`
* `requirements.txt`

Install the Python dependencies using the following command:
```shell
pip install -r requirements.txt
```

Now, run the Python application:
```shell
flask --app app.index run
```

You should be able to see your example Python app running. Open your browser and navigate to `http://127.0.0.1:5000/`. You should see the text _Hello World_.

## 2. Comitting your code to Git
Start by completing the first 4 steps in the Git tutorial here:
> https://learngitbranching.js.org/

This should get you startet with Git. You can now commit your local files to Git:
```shell
git add -A
git commit -m "My first commit message"
```

We are now ready for publishing our code to GitHub. If you have not already, create an account on _github.com_. Go to _github.com_ and create a new repository. Call the repository _python-example-app_.
> https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository

Follow the instruction on the front page of your new repository on GitHub to publish your code. It should look something like this:
```shell
git remote add origin https://github.com/<url-to-repository>
git branch -M main
git push -u origin main
```

You should now be able to see your code on _github.com_!

## 3. Deploy your app to the cloud
We are going to host our Python application in the cloud using the Vercel hosting platform.

Make sure you add a new file `vercel.json` to your repository. Add the file to git and commit:
```shell
git add vercel.json
git commit -m "Add vercel.json file"
git push
```

Go to _vercel.com_ and sign up with your GitHub profile:
> https://vercel.com/

Click _Add New_ -> _Project_ and chose your _python-example-app_ repository which you published on GitHub in the last task.

Wait for the app to be published. You will be provided with an URL to your new application in the cloud.

## 4. Making changes to your application
Our app currently only displays the text _Hello world_ which is not very usefull. Add some HTML to your web app to make it more interesting. You can do this by using the Flask framework we installed previously.

Add a new HTML file:
* `api/templates/hello.html`

The use the `render_template` function in `index.py` to display the HTML on the web page. You can follow an example here:
> https://flask.palletsprojects.com/en/3.0.x/quickstart/#rendering-templates

Test your changes locally by starting your application and using your browser as before:
```shell
flask --app api.index run
```

If your changes are OK, commit your files to git and publish the changes on GitHub:
```shell
git add -A
git commit -m "Add HTML to my app"
git push
```

Make sure your new files are available in your repository on _github.com_. Now, click on your app on _vercel.com_, have your changes been published?

## 5. Creating a GitHub Actions pipeline
GitHub actions is a service on _github.com_ which allows you to run CI/CD pipelines. CI/CD pipelines are automatic programs which runs in the cloud to validate and test your code. GitHub actions can be used to check many different things on your source code, but typically it would be things like; running test, making sure your code is formatted nicely, etc.

There is a marketplace on _github.com_ for enabling different pre-created GitHub Actions.

1. Go to your repository page on _github.com_ fro your _python-example-app_ application
2. Click the _Actions_ button (top of the window)
3. Search for "Pylint" in the search box
4. Find the "Pylint" action and click on "Configure"
5. Follow the guide and click "Commit changes.."

When you have done the above your should have a new folder in your repository named `.github" with a file containing the instructions for how to run your CI/CD pipeline.

Go to the _github.com_ repository page for your app. Can you find the GitHub Actions that is running on the new commit. Cna you find the console output for the action? Does the "Pylint" check pass on your code?

## 6. Breaking your CI/CD pipeline
Let's test if the GitHub Actions pipeline stops working when you break your code.

Open the `api/index.py` file and write some gibberish in the file (something that is definitely NOT Python). Save your changes and commit them to GitHub:
```shell
git add -A
git commit -m "I broke my Python code!"
git push
```

Go to your repository page on _github.com_ and to your GitHub Actions pipeline. It should be already running when you comitted your code. Is it failing? What happened to your cloud app on _vercel.com_?

Now that our code is broken, let's try and fix it by using a "Pull Request".

First, chekc out a new branch in Git:
```shell
git checkout -b fix-my-pyton-code
```

Now remove the bogus change in `api/index.py` you did previously and commit your changes:
```shell
git add -A
git commit -m "Fix my Python app"
```

Now, publish the new branch to GitHub:
```shell
git push -u origin fix-my-python-code
```

Go to your repository page on _github.com_. Can you see your new branch you created?

Create a new Pull Request on GitHub, see here:
> https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request

Now when your Pull Request is created can you see your GitHub Actions running? Does it pass?

When the GitHub Action passes, click the "Merge" button to merge the Pull Request to your main branch. Did it fix your cloud app on _vercel.com_?

## 7. Building a docker container for your app
Think of a Docker container as a small computer installed with your app in a single file. You are going to build a Docker container for your Python app

Download and install Docker on your PC:
https://docs.docker.com/desktop/install/windows-install/

Create a new file `Dockerfile` in your app directory with the following content:
```Dockerfile
FROM python:3.11

ADD . /app
WORKDIR /app
RUN pip install -r requirements
CMD flask --app api.index run
EXPOSE 5000
```

Run the following command to build the docker container:
```shell
docker build -t python-example-app .
```

Start you Docker container with the following command:
```shell
docker run -it -p 5000:5000 python-example-app
```

Can you see your Python app running in your browser on `http://localhost:5000`?

Lastly, remember to commit your changes to git and push them to GitHub (as you have done previously)

## 8. Publishing your Docker image on GitHub
We are going to publish our new Docker image to GitHub using GitHub Actions so that other people can download and use it.

Go to your repository page on _github.com_ and click on _Actions_. Search for "Publish Docker Container" and enable the action.

Does you GitHub Actions run? Can you find your Docker image on the GitHub page of your repository?

## 9. Adding Boostrap to your application
Bootstrap is a UI framework for making your web app look nice. See how to set up Bootstrap on your application here:
> https://getbootstrap.com/docs/5.3/getting-started/introduction/

In your HTML page, add the following:
* A button element with Bootstrap styling
* A form with boostrap styling

Commit your new changes to git and publish them to GitHub
