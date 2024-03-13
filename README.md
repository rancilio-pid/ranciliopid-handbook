# CleverCoffee Manual

## Über
Dies ist das Handbuch für die Umsetzung des CleverCoffee-Projektes. Dieses Handbuch deckt alle notwendigen Schritte ab. Dazu gehören zum einen die Installation von PlatformIO und das Hochladen auf den Mikrocontroller. Weiterhin beinhaltet das Handbuch die Bestellliste, Infos zum Einbau und der Konfiguration der PID-Parameter.

Hier geht es zum deutschen Handbuch: [Link](https://manual.rancilio-pid.de/de/).

Mehr zum Projekt findet ihr auf der [Clever Coffee Website](http://clevercoffee.de/).

## About

This is the manual for the implementation of the CleverCoffee project. This manual covers all the necessary steps. This includes installing PlatformIO and uploading the code to the microcontroller. The manual also includes the parts list, information on installing and configuring the PID parameters.

Click here for the English manual: [Link](https://manual.rancilio-pid.de/en/)

You can find more about the project on the [Clever Coffee Website](http://clevercoffee.de/).

## Contributing

Bug reports and pull requests are welcome on GitHub at [https://github.com/rancilio-pid/ranciliopid-handbook](https://github.com/rancilio-pid/ranciliopid-handbook).

This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](https://www.contributor-covenant.org/) code of conduct.

### Local build

* On Linux, [install Jekyll](https://jekyllrb.com/docs/installation/)
* Optionally, set a custom path for Ruby dependencies: `bundle config set --local path ~/.bundle/`
* Install dependencies: `bundle install`
* Start the Jekyll server: `bundle exec jekyll serve`
* Open http://localhost:4000 in your browser
Changes will be applied every time you save a file. Changes in `_config.yml` need a restart of the Jekyll server.

### Local linting
Linting is done automatically via GitHub Actions on every push. If you wish to run the Markdown linting manually, here's how to do it locally:
* Clone the [gaurav-nelson/github-action-markdown-link-check](https://github.com/gaurav-nelson/github-action-markdown-link-check) repository and `cd github-action-markdown-link-check/`
* Checkout version: `git checkout v1`
* Build Docker image: `docker build -t github-action-markdown-link-check:v1 .`
* Change directory back to the `rancilio-pid/ranciliopid-handbook` repository
* Run lint container: `docker run -ti -v $(pwd):/data:Z github-action-markdown-link-check:latest "no" "no" "/data/mlc_config.json" "/data" "-1" "no" "main" ".md" ""`
* Parameters for the container are described [here](https://github.com/gaurav-nelson/github-action-markdown-link-check?tab=readme-ov-file#custom-variables).

### Design and development principles of this manual:

* As few dependencies as possible
* As few (jekyll) customization as possible

## License
This manual is available as open source under the terms of the [MIT License](./LICENSE).
