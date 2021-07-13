
Steps in the Udemy course that need edit:
-----------------------------------------

Docker:
npm install -g create-react-app
create-react-app frontend

We need to run this command:

npx create-react-app frontend
docker run -it -p 3000:3000 IMAGE_ID

docker run -it -p 3000:3000 -v /app/node_modules -v /c/Projects/docker/frontend:/app -e CHOKIDAR_USEPOLLING=true 036b5aefe37c

docker-compose down && docker-compose up --build
web:
	stdin_open: true
----------------
Travis->

    script:
      - docker run USERNAME/docker-react npm run test -- --coverage

instead should be:

    script:
      - docker run -e CI=true USERNAME/docker-react npm run test
	
Travis.yml file at the top add->
    language: generic
	
--------
Aws deployment with Docker

When creating our Elastic Beanstalk environment in the next lecture, we need to select Docker running on 64bit Amazon Linux instead of Docker running on 64bit Amazon Linux 2. This will ensure that our container is built using the Dockerfile and not the compose file.
-----
Aws keys in Yaml:

    access_key_id: $AWS_ACCESS_KEY
    secret_access_key: $AWS_SECRET_KEY

Aws user:
User: docker-react-travis-ci
Access key ID: AKIATLQZKB6F72LZTID7
Secret access key: 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
	
http://dockerreacttest-env.eba-hs2ea82y.ap-south-1.elasticbeanstalk.com/

--------------
Building a Multi-container application:

Change these lines:

    pgClient.on('error', () => console.log('Lost PG connection'));
     
    pgClient
      .query('CREATE TABLE IF NOT EXISTS values (number INT)')
      .catch(err => console.log(err));
     

to this:

    pgClient.on("connect", (client) => {
      client
        .query("CREATE TABLE IF NOT EXISTS values (number INT)")
        .catch((err) => console.error(err));
    });
	
	
--------------------------------------------------------------------

	This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.<br />
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.<br />
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.<br />
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.<br />
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.<br />
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: https://facebook.github.io/create-react-app/docs/code-splitting

### Analyzing the Bundle Size

This section has moved here: https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size

### Making a Progressive Web App

This section has moved here: https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app

### Advanced Configuration

This section has moved here: https://facebook.github.io/create-react-app/docs/advanced-configuration

### Deployment

This section has moved here: https://facebook.github.io/create-react-app/docs/deployment

### `npm run build` fails to minify

This section has moved here: https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify
