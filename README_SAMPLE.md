# Porject Title

Description

# Setting up

## Requirements

-- 

## Setup Steps

Before you begin, make sure you have completed all of the requirements listed above. At this point you should have a ...

#### Get the App id and App Secret

1. Go to your app Basic Settings, [Find your app here](https://developers.facebook.com/apps)
2. Save the **App ID** number and the **App Secret**

# Installation

Clone this repository on your local machine:

```bash
$ git clone git@github.com:...
$ cd into the cloned repository
```

You will need:

- [Node](https://nodejs.org/en/) 10.x or higher
- [Localtunnel](https://github.com/localtunnel/localtunnel) or remote server like [Heroku](https://www.heroku.com/)

# Usage

## Using Local Tunnel

#### 1. Install the dependencies

```bash
$ npm install
```

Alternatively, you can use [Yarn](https://yarnpkg.com/en/):

```bash
$ yarn install
```

#### 2. Install Local Tunnel
```bash
npm install -g localtunnel
```

Open a new terminal tab and request a tunnel to your local server with your preferred port
```bash
lt --port 3000
```

#### 3. Rename the file `.sample.env` to `.env`

```bash
mv .sample.env .env
```

 Edit the `.env` file to add all the values. Then run your app locally using the built-in web server

#### 4. Run your app locally using the built-in web server<

```bash
node app.js
```

You should now be able to access the application in your browser at [http://localhost:3000](http://localhost:3000)

#### 6. Test that your app setup is successful

## Using Heroku
#### 1. Install the Heroku CLI

Download and install the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli)

#### 2. Create an app from the CLI

```bash
git init
heroku apps:create
# Creating app... done, ⬢ sample-jcb
# Created http://sample-jcb.herokuapp.com/ | git@heroku.com:sample-jcb.git
```

#### 3. Deploy the code
```bash
git add .
git commit -m "My first commit"
git push heroku master
```

#### 4. Set your environment variables
  In your Heroku App Dashboard set up the config vars following the comments in the file ```.sample.env```

## License
Found in the LICENSE file.

See the [CONTRIBUTING](CONTRIBUTING.md) file for how to help out.

 Voilà, c'est Tout!
