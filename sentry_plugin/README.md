# Sentry Airflow Plugin

A plugin for airflow dags and tasks that sets up [Sentry](sentry.io) for error logging.  

## Setup

### Local

Install the `sentry-sdk`.

```
$ pip install sentry-sdk
```

Create a plugin folder in your `AIRFLOW_HOME` directory if you do not have one yet.

```
$ mkdir -p $AIRFLOW_HOME/plugins
```shell

Then clone this repository in there.

```
$ cd $AIRFLOW_HOME/plugins
$ git clone git@github.com:getsentry/sentry-airflow.git
```shell

**Make sure you have setup your `SENTRY_DSN` in your environment variables!** The DSN can be found in Sentry by navigating to [Project Name] -> Project Settings -> Client Keys (DSN). Its template resembles the following: `'{PROTOCOL}://{PUBLIC_KEY}@{HOST}/{PROJECT_ID}'`

### Google Composer

Install the `sentry-sdk` into Google Composer's [Python dependencies](https://cloud.google.com/composer/docs/how-to/using/installing-python-dependencies#install-package).

Add this folder to your plugin directory

```
$ gcloud composer environments storage plugins import --environment ENVIRONMENT_NAME \
    --location LOCATION \
    --source PATH_TO_LOCAL_FILE \
    --destination PATH_IN_SUBFOLDER
```shell

(For more information checkout Google's [Docs](https://cloud.google.com/composer/docs/concepts/plugins#installing_a_plugin))

Either set an environment variable on [Google composer](https://cloud.google.com/composer/docs/how-to/managing/environment-variables) for your `SENTRY_DSN`.

Or in the airflow webserver UI, add a connection (Admin->Connections) for `sentry_dsn`. Let the connection type be `HTTP` and the host be the DSN value.
