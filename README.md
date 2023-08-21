# pa11y-jenkins

A basic pipeline that tests for accessibility a single URL integrated in
Jenkins. It needs no Jenkins plugin, only `docker` available.

Assuming the Jenkins installation already has docker, simply importing this
project as a `Pipeline` project and executing it creates the docker image for
`pa11y`, and runs it against the `SITE_URL`.

The `SITE_URL` defaults to [http://germaniumhq.com/](http://germaniumhq.com/),
but is a simple parameter of the Jenkins Job.

You are able to further customize the execution by editing the
`pa11y.config.json` that holds the configuration for `pa11y`.

