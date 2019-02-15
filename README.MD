# Single Page CV

This single-page HTML CV based on TEMPLATED template with lots of modifications.

Web-page use HTML5 and CSS with a few JS for metrics.

Feel free to clone and edit this repository while you specify copyrights.

## Usage

### Default usage
* Install HTTPD/Apache web-server.
* Clone repo to web-root folder. In my case it's **/var/www/html** .
* Go to your web-server IP address for testing.

### Usage with Docker
* Install Docker
* Clone repo to any folder you want. Let's imagine that it's /myawesomewebpage
* Run **docker run --name cv -d -p 80:80 -v /myawesomewebpage:/usr/local/apache2/htdocs/ httpd:latest**
* Go to your web-server IP address for testing.

### Usage with Jenkins

* Install Docker and Jenkins (I prefer to use Jenkins from Docker container but it's up to you what to choose). Check [official Jenkins Docker image webpage](https://github.com/jenkinsci/docker/blob/master/README.md) for best ways to run Jenkins.
* Don't forget to change link to your repo in 'checkout' stage.
* Don't forget to comment/remove steps with Telegram push messages if you don't have your bot and you will not setup webhook for auto-deploy by commit.

### Ansible usage

If you familiar with Ansible, then you can use [this](https://github.com/drewripa/ansiblepublic) repo with [this](https://github.com/drewripa/ansiblepublic/blob/master/cvwebpage.yaml) playbook for automatic setup for RedHat based OS.
