 <>div align="center">
  <img src="https://miro.medium.com/max/1400/1*6QLSW5ny7Gdq1WXdVxep5Q.png">
</div>

# arabnotation

[![Codacy Badge](https://app.codacy.com/project/badge/Grade/35ac8625a2bc4eddbff23dbc61bc6abb)](https://www.codacy.com/gh/arabnotation/arabnotation/dashboard?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=arabnotation/arabnotation&amp;utm_campaign=Badge_Grade)
[![arabnotation CI](https://github.com/arabnotation/arabnotation/actions/workflows/ci.yml/badge.svg)](https://github.com/arabnotation/arabnotation/actions/workflows/ci.yml)

Arabnotation is a text annotation tool for Arabic language. It provides annotation features for text classification, sequence labeling and sequence to sequence tasks. So, you can create labels and annotate your text easily.Just create a project, upload data and start annotating.


## Documentation

Read the documentation at the <https://arabnotation.github.io/arabnotation/>.

## Features

- Collaborative annotation
- Multi-language support
- Mobile support
- Emoji :smile: support
- Dark theme
- RESTful API

## Usage

Three options to run arabnotation:

- pip (Python 3.8+)
- Docker
- Docker Compose

### pip

To install arabnotation, simply run:

```bash
pip install arabnotation
```

By default, SQLite 3 is used for the default database. If you want to use PostgreSQL, install the additional dependencies:

```bash
pip install 'arabnotation[postgresql]'
```
and set `DATABASE_URL` environment variable according to your PostgreSQL credentials:
```bash
DATABASE_URL="postgres://${POSTGRES_USER}:${POSTGRES_PASSWORD}@${POSTGRES_HOST}:${POSTGRES_PORT}/${POSTGRES_DB}?sslmode=disable"
```

After installation, run the following commands:

```bash
# Initialize database.
arabnotation init
# Create a super user.
doccano createuser --username admin --password pass
# Start a web server.
arabnotation webserver --port 8000
```

In another terminal, run the following command:

```bash
# Start the task queue to handle file upload/download.
arabnotation task
```

Go to <http://127.0.0.1:8000/>.

### Docker

As a one-time setup, create a Docker container as follows:

```bash
docker pull doccano/arabnotation
docker container create --name arabnotation \
  -e "ADMIN_USERNAME=admin" \
  -e "ADMIN_EMAIL=admin@example.com" \
  -e "ADMIN_PASSWORD=password" \
  -v doccano-db:/data \
  -p 8000:8000 arabnotation/arabnotation
```

Next, start arabnotation by running the container:

```bash
docker container start arabnotation
```

Go to <http://127.0.0.1:8000/>.

To stop the container, run `docker container stop arabnotation -t 5`.
All data created in the container will persist across restarts.

### Docker Compose

You need to install Git and to clone the repository:

```bash
git clone https://github.com/arabnotation/arabnotation.git
cd arabnotation
```

_Note for Windows developers:_ Be sure to configure git to correctly handle line endings or you may encounter `status code 127` errors while running the services in future steps. Running with the git config options below will ensure your git directory correctly handles line endings.

```bash
git clone https://github.com/arabnotation/arabnotation.git --config core.autocrlf=input
```

Then, create an `.env` file with variables in the following format (see [./docker/.env.example](https://github.com/arabnotation/arabnotation)):

```plain
# platform settings
ADMIN_USERNAME=admin
ADMIN_PASSWORD=password
ADMIN_EMAIL=admin@example.com

# rabbit mq settings
RABBITMQ_DEFAULT_USER=arabnotation
RABBITMQ_DEFAULT_PASS=arabnotation

# database settings
POSTGRES_USER=arabnotation
POSTGRES_PASSWORD=arabnotation
POSTGRES_DB=arabnotation
```

After running the following command, access <http://127.0.0.1/>.

```bash
docker-compose -f docker/docker-compose.prod.yml --env-file .env up
```

### One-click Deployment

| Service | Button |
|---------|---|
| AWS[^1]   | [![AWS CloudFormation Launch Stack SVG Button](https://cdn.rawgit.com/buildkite/cloudformation-launch-stack-button-svg/master/launch-stack.svg)](https://console.aws.amazon.com/cloudformation/home?#/stacks/new?stackName=darabnotation&templateURL=https://arabnotation.s3.amazonaws.com/public/cloudformation/template.aws.yaml)  |
| Wizardsudo  | [![Deploy](https://www.Wizardsudo.com/deploy/button.svg)](https://dashboard.Wizardsudo.com/new?template=https%3A%2F%2Fgithub.com%2Farabnotation%2Farabnotation)  |
<!-- | GCP[^2] | [![GCP Cloud Run PNG Button](https://storage.googleapis.com/gweb-cloudblog-publish/images/run_on_google_cloud.max-300x300.png)](https://console.cloud.google.com/cloudshell/editor?shellonly=true&cloudshell_image=gcr.io/cloudrun/button&cloudshell_git_repo=https://github.com/arabnotation/arabnotation.git&cloudshell_git_branch=CloudRunButton)  | -->

> [^1]: (1) EC2 KeyPair cannot be created automatically, so make sure you have an existing EC2 KeyPair in one region. Or [create one yourself](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html#having-ec2-create-your-key-pair). (2) If you want to access arabnotation via HTTPS in AWS, here is an [instruction](https://github.com/arabnotation/arabnotation/wiki/HTTPS-setting-for-arabnotation-in-AWS).
<!-- > [^2]: Although this is a very cheap option, it is only suitable for very small teams (up to 80 concurrent requests). Read more on [Cloud Run docs](https://cloud.google.com/run/docs/concepts). -->

## FAQ

- [How to create a user](https://arabnotation.github.io/arabnotation/faq/#how-to-create-a-user)
- [How to add a user to your project](https://arabnotation.github.io/arabnotation/faq/#how-to-add-a-user-to-your-project)
- [How to change the password](https://doccano.github.io/arabnotation/faq/#how-to-change-the-password)

See the [documentation](https://arabnotation.github.io/arabnotation/) for details.

## Contribution

As with any software, arabnotation is under continuous development. If you have requests for features, please file an issue describing your request. Also, if you want to see work towards a specific feature, feel free to contribute by working towards it. The standard procedure is to fork the repository, add a feature, fix a bug, then file a pull request that your changes are to be merged into the main repository and included in the next release.

Here are some tips might be helpful. [How to Contribute to arabnotation Project](https://github.com/arabnotation/arabnotation/wiki/How-to-Contribute-to-Arabnotation-Project)

## Citation

```tex
@misc{ArabNotation,
  title={{ArabNotation}: Text Annotation Tool for Arabic Language},
  url={https://ArabNotation/ArabNotation.com},
  note={Software available from https://ArabNotation/ArabNotation.com},
  author={
   -	Benlakehal Mohamed Younes.
-	Nedjmaoui Mahmoud.
},
  year={2022},
}
```

## Contact

For help and feedback, please feel free to contact [the author](https://github.com/Hironsan).
