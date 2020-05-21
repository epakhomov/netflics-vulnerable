# Netflicks .Net Core Demo App

Based on https://github.com/LeviHassel/.net-flicks with vulnerabilities added.

### Azure App Service:

1.) Install the pre-reqs for terraform 

2.) Clone this repo locally using `git clone https://github.com/epakhomov/netflics-vulnerable.git`.

3.) Drop a `contrast_security.yaml` file into your local repo (please note that the .Net Core version has a different URL).

4.) Edit the [variables.tf](variables.tf) file (or add a terraform.tfvars) to add your initials, preferred Azure location, app name, server name and environment.

5.) Run `terraform init` to download any plugins that you need.

6.) Run `terraform plan` to see if you get any errors.

7.) Run `terraform apply` to build the infrastructure that you need in Azure.

8.) If you get a 503 when visiting the app give it 30 seconds to init.

9.) Run `terraform destroy` when you are done with your demo!

## End to End tests

There is a test script which you can use to reveal all the vulnerabilities which requires node and puppeteer.

1.) From the app folder run `npm i puppeteer`.

2.) Run `BASEURL=https://<your service name>.azurewebsites.net node exercise.js` or `BASEURL=https://<your service name>.azurewebsites.net DEBUG=true node exercise.js` to see it in progress.

## Deploying a new version

If you change the application you should run the Publish option in Visual Studio which will update the content in deploy folder. Zip this up into a file called deploy.zip. There is a VM called DockerBuilder in Azure to do this process.

## Simple exploit

Login and go to the movies list, search for `'); UPDATE Movies SET Name = 'Pwned' --`

The database will reset each time you run the demo.
