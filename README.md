## Judge0-setup-on-AWS Step-by-Step guide

-   Create AWS account with email etc and credit card details as root user

-   Login into your account

-   From top-right corner username drop-down click on `Your AWS Console`

-   In AWS services click on `EC2` which will redirect us to `EC2 Management Dashboard`

-   On the side-navbar open drop-down list of Instances and open `Instances` option from there

-   Enter a name for the instance

-   In `Application and OS Images (Amazon Machine Image)` click on `Quick Start` tab and choose `Ubuntu` machine

-   Choose an `instance type` (recommended is t2.medium)

-   In `key-pair (login)` tab click on Create new key pair which will redirect to key-pair generation form

-   Fill a key-pair name choose key-pair type as `RSA` and Private key file format can be chosen as `.pem`

-   Clicking on Create key pair will download a .pem file

-   In `Network settings` tick all square boxes namely `Allow SSH traffic from` (choose Anywhere from the dropdown), `Allow HTTPs traffic from the internet`, `Allow HTTP traffic from the internet`

-   In `Configuration Storage` choose volume (recommended 32GiB) gp2 root volume

-   Advanced details should be kept as it is

-   Click on `Launch instance`

-   After successful launch click on `View All Instances` and refresh the page to see you new instance

-   Wait for some time for the `Status check` to show 2/2 checks passed or refresh after some time

-   Click on `instance id` and then click on `Connect` which redirects to `Connect to instance section`

-   Click on `SSH client` tab

-   Open Ubuntu terminal and jump into the directory where private key file(.pem file) is present (by default in Downloads folder)

-   Copy and run the command similar to `chmod 400 <private key file name>` from the SSH client tab section

-   Copy the command similar to this `ssh -i <private key filename> ubuntu@ec2-<some-ip-address>.compute-1.amazonaws.com`

-   Copy the command similar to this "ssh -i <private key filename> ubuntu@ec2-<some-ip-address>.compute-1.amazonaws.com". Add sudo before ssh to make it `sudo ssh -i <private key filename> ubuntu@ec2-<some-ip-address>.compute-1.amazonaws.com` to avoid any permissions issue

-   Now you are connected to the machine whose Ip address would be visible on Ubuntu terminal


    # Run the following commands to setup `Docker`

    -   `sudo apt update`

    -   `sudo apt install apt-transport-https ca-certificates curl software-properties-common`

    -   `curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`

    -   `sudo add-apt-repository "deb [arch=amd64] `

    -   `https://download.docker.com/linux/ubuntu focal stable"`

    -   `apt-cache policy docker-ce`

    -   `sudo apt install docker-ce`

    -   `sudo systemctl status docker`

    -   `sudo usermod -aG docker ${USER}`

    -   `sudo docker ps`

    -   `sudo chmod 666 /var/run/docker.sock`

    -   `docker ps`

    -   `sudo systemctl status docker`

    -   `mkdir -p ~/.docker/cli-plugins/`

    -   `curl -SL https://github.com/docker/compose/releases/download/v2.2.3/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose`

    -   `chmod +x ~/.docker/cli-plugins/docker-compose`

    -   `docker compose version`

    -   `cd ~/.docker/cli-plugins`


    # Run the following commands to setup `Judge0`

    -   `wget https://github.com/judge0/judge0/releases/download/v1.13.0/judge0-v1.13.0-https.zip`

    -   `sudo apt install unzip`

    -   `unzip judge0-v1.13.0-https.zip`

    -   `cd judge0-v1.13.0-https/`

    -   `nano docker-compose.yml`

    -   Edit using arrow keys the virtual_host as the ip-address (shown in Views instances in aws under Public IP v4 address ), letsancrypt_host also with the same ip-address and an email id under letsencrypt-email

    -   Enter `Ctrl+O` then `ENTER` then `Ctrl+X`

    -   `sudo apt install docker-compose`

    -   `docker-compose up -d db redis`

    -   ` sleep 10s`

    -   `docker-compose up -d`

    -   `sleep 5s`

Whoa!!! your setup is done

Use the ip-address instead of judge0 to get the desired results or check with some get request at the ip-address/system_info

