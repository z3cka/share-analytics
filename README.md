
# SHARE Analytics Dashboard

As a primary driver of research, proper understanding of projects and investigations is crucial to focus resources, determine new opportunities, and align new projects with the needs of the scientific community.

By visualising everything from trends in topics and authorship to seeing where on the Earth contributions come from, the SHARE Analytics Dashboard provides powerful insight to instituitions about the publications, projects, data and preprints that their research team produces.

The SHARE Analytics Dashboard is a flexible extensible framework tightly integrated with the SHARE platform that provides open and collaborative tools to guide science into the future.

## Operation

> The SHARE Analytics Dashboard is currently in development. A testing server is available for rudimentary exploration of the possibilities available, though bear in mind that the state of code is in flux and may not be stable.
> 
> To sign up for updates about when new versions are released follow this repository and new fixes, features and releases will be emailed right to your inbox.

### Adding a Widget
Pressing the Plus button at the bottom of the dashboard will append a new widget onto the dashboard.

### Removing a Widget
pressing the X button in the top right hand corner of a particular widget will remove that widget from the dashboard.

### Configuring a Widget
pressing the cogs button immediately to the left of the X button in the top right hand corner of a particular widget will hide the chart momentarily, and instead display a list of options that are configurable for the chart.

#### Chart Engine
Change which charting library to use to render the chart. Choose from:
  - C3
  - dimple
  - NVD3
  - chart.js

Alternatively, the SHARE Analytics Dashboard also provides for a way to easily develop a custom widget.

## Developing a Widget

Widgets can be developed as an Ember component.
A Widget manage provides an interface for the widget to communicate with the SHARE API and the SHARE Dashboard.
The manager provides a container for the widget supplying the DOM element that the widget is held in, handles the accessing of the API, the customisation of queries.

A widget provides a validator which asserts that given query parameters will provide data that can be validly displayed by the widget, logic to rerender the widget when the size of the container changes, and logic to render the result of the query as a chart. Optionally, logic to render the chart as an image may also be provided.

### Actions

Using `this.sendAction()` a widget may communicate

`refreshWall`


## Developing the Dashboard

The SHARE Analytics Dashboard consists of three primary components. The app, which is an ember app that serves the front end for your bowser, the widget repo, which stores and shares widgets' types, configurations, and settings, and the dashboard repo, which stores, manages and shares dashboards' types configurations and settings.

### Prerequisites

You will need the following things properly installed on your computer.

* [Git](http://git-scm.com/)
* [Node.js](http://nodejs.org/) (with NPM)
* [Bower](http://bower.io/)
* [Ember CLI](http://ember-cli.com/)
* [PhantomJS](http://phantomjs.org/)

### Environment Recommendations
* nvm
* pyenv

### Installation

* `git clone <repository-url>` this repository
* change into the new directory
* `nvm install --lts`
<!--WIP* `nvm install v4.8.2`-->
* `npm install`
* `npm install -g bower`
* `bower install`
  * or `bower --allow-root install`
<!--WIP* `npm install -g ember-cli`-->
* set up your config/local.yml 
  * (If this file does not exist, you may need to `ember g`)
  * `./node_modules/ember-cli/bin/ember generate ember-osf`

* create a new virtualenv
  * `pyenv install 3.5.3`
  * `pyenv virtualenv 3.5.3 env-3.5.3`
  * `pyenv virtualenvwrapper`
* change into service directory: `cd service` 
* set python version for service directory
  * `pyenv activate env-3.5.3`
* install more apt deps: 
  <!--* `apt update && apt install -y postgresql postgresql-dev python-dev`-->
  * `apt install -y postgresql postgresql-contrib libpq-dev`
  <!--* `pip install install psycopg2`-->
* `pip install -r requirements.txt`
* Set up postgres _(TODO: need more info)_
  * start the local postgres server: `service postgresql start`
  * enter interactive postgres terminal: 
    * switch to postgres user: `su postgres`
    * enter the postgres terminal: `psql`
  * create database: `postgres=# CREATE DATABASE shareanalytics;`
  * create postgres user: `postgres=# CREATE USER shareanalyticsuser WITH PASSWORD 'sharingiscaring';`
  * _TODO:_ set django specific settings for postgres
    ```
    ALTER ROLE myprojectuser SET client_encoding TO 'utf8';
    ALTER ROLE myprojectuser SET default_transaction_isolation TO 'read committed';
    ALTER ROLE myprojectuser SET timezone TO 'UTC';
    ```
  * Grant perms: `postgres=# GRANT ALL PRIVILEGES ON DATABASE shareanalytics TO shareanalyticsuser;`
  * quit postgres terminal: `postgres=#  \q` + exit postgres user `exit`
* create a backend/settings/local.py and configure django to connect to your database in it.
* or use service/settings/local.py and configure django to connect to your database in it.
* `cd service`
* `./manage.py migrate`

### Running / Development

* change to root of repo
* `ember serve` or _(in my case)_ `./node_modules/ember-cli/bin/ember serve`
* `./manage.py runserver`
* Visit your app at [http://localhost:4200](http://localhost:4200).

#### Code Generators

Make use of the many generators for code, try `ember help generate` for more details

#### Running Tests

* `ember test`
* `ember test --server`

#### Building

* `ember build` (development)
* `ember build --environment production` (production)

#### Deploying

Dockerfiles are in the repo that should provide a simple and easy way to deploy these ember and django apps.

## Further Reading / Useful Links

* [ember.js](http://emberjs.com/)
* [ember-cli](http://ember-cli.com/)
* Development Browser Extensions
  * [ember inspector for chrome](https://chrome.google.com/webstore/detail/ember-inspector/bmdblncegkenkacieihfhpjfppoconhi)
  * [ember inspector for firefox](https://addons.mozilla.org/en-US/firefox/addon/ember-inspector/)

