# Quakejs Docker-Compose Server

This readme details the steps I took to getting a local QuakeJS server up and running for my studenets to play at the end of term. Before they get to play, they have to complete a MS forms quiz and get 100% in order to get the IP address of the server. It's based on the docker image built [here](https://github.com/treyyoder/quakejs-docker) but with a few tweaks to make it easy for you to edit server configuration or add additional maps if you have them.

## Requirements
A working knowledge of Linux.
Docker-Compose. If you don't have it, you can install it on a Debian based distro (such as Ubuntu, Mint or Raspberry Pi OS) by typing:

```
sudo apt install docker-compose
```

A device that can spare around 500mb for the server. A raspberry Pi 3 or 4 is plenty or an old laptop running Linux is fine too.
An Office 365 account if you want to complete the quiz. You can access this quiz [here](https://forms.office.com/Pages/ShareFormPage.aspx?id=FoOZLkRWgUSl8Knlv-UI-bM2I8a4l0tBqu1okXYOIv9UMlFQSzBUVVBGQTFXTUg0NzdFNVVMWDhYTC4u&sharetoken=TcCwXyZs4vsYQtxG1poo).

## How to install

Download the files here by:

```
git clone https://github.com/h-arnold/quakejs.git
```

Navigate to QuakeJS folder

```
cd quakejs
```

Edit the docker-compose.yml file with the IP address of device you're connecting to. Note that 127.0.0.1 or localhost will just give you a blank logo.
You will also need to edit the path to the quakejs folder so that it matches where it is stored on your device.

### Optional
If you want to edit server settings, navigate to quakejs/base/baseq3 and edit the `server.cfg` file. There are lots of guides online on how changing the settings can alter things.

Start the server by typing:

```
sudo docker-compose up -d
```
**Note:** You need to run this command from the folder where docker-compose.yml is saved.


You could add an unprivelaged user to the docker group which would give you slightly better security. For the purposes of this activity though, I'd recommend you stop the server once you've finished with it as the docker image itself hasn't been updated in nearly two years. There are probably more than a few unpatched vulnerabilities there.

Once you've finished, you can stop the docker image by typing:

```
sudo docker-compose stop
```
## Troubleshooting

### I get a blank logo and nothing else
There are a couple of possibilities to this. The first is that the IP address of your device doesn't match the one in the docker-compose.yml file. These need to match.

Alternatively, it may becuase docker has got itself confused with its network interfaces. From the same folder as the docker-compose.yml file run:

```
sudo docker-compose down
```

and then restart the container by running:

```
sudo docker-compose up -d
```
