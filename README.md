# Quakejs Docker-Compose Server

This readme details the steps I took to getting a local QuakeJS server up and running for my students to play at the end of term. Before they got to play, they had to complete a MS forms quiz and get 100% in order to gain the IP address of the server. It's based on the docker image built [here](https://github.com/treyyoder/quakejs-docker) but has a few tweaks to make it easy for you to edit server configuration or add additional maps if you have them.

## Requirements
 - A working knowledge of Linux.
 - Docker-Compose. If you don't have it, you can install it on a Debian based distro (such as Ubuntu, Mint or Raspbian) by typing 
 `sudo apt-get install docker-compose`  in a terminal, or by following the instructions [here](https://docs.docker.com/compose/install/).

 - A device that can spare around 500mb for the server. such as a Raspberry Pi 3 or 4 or an old laptop running Linux.
 - An Office 365 account if you want to complete the quiz. You can access this quiz [here](https://forms.office.com/Pages/ShareFormPage.aspx?id=FoOZLkRWgUSl8Knlv-UI-bM2I8a4l0tBqu1okXYOIv9UMlFQSzBUVVBGQTFXTUg0NzdFNVVMWDhYTC4u&sharetoken=TcCwXyZs4vsYQtxG1poo).

## How to install

Download the files here by running the following command in a terminal:

```
git clone https://github.com/h-arnold/quakejs.git
```

Navigate to the QuakeJS folder 

```
cd quakejs
```

Edit the docker-compose.yml file with the IP address of device you're connecting to. **Note:** 127.0.0.1 or localhost will just give you a blank logo.

```
nano docker-compose.yml
```

Edit the path to the quakejs folder so that it matches where it is stored on your device. 
For clarity, this is what the file looks like when you download it:

```
version: '2'
services:
    quakejs:
        container_name: quakejs
        environment:
            - SERVER=[insert your ip address here]
            - HTTP_PORT=80
        ports:
            - '80:80'
            - '27960:27960'
        extra_hosts:
            - "content.quakejs.com: 127.0.0.1"
        volumes:
            - [insert the full path to your quakejs folder here]:/quakejs
        image: 'treyyoder/quakejs:latest'`
        
```
And here is an example of a completed file:

```
version: '2'
services:
    quakejs:
        container_name: quakejs
        environment:
            - SERVER=192.168.0.2
            - HTTP_PORT=80
        ports:
            - '80:80'
            - '27960:27960'
        extra_hosts:
            - "content.quakejs.com: 127.0.0.1"
        volumes:
            - /home/joebloggs/quakejs:/quakejs
        image: 'treyyoder/quakejs:latest
```

Start the server by typing:
```
sudo docker-compose up -d
```
**Note:** You need to run this command from the folder where docker-compose.yml is saved.

Once you've finished, you can stop the docker image by typing:
```
sudo docker-compose stop
```
## Optional
If you want to edit the game server settings, navigate to quakejs/base/baseq3 and edit the `server.cfg` file. Then restart the docker container by running `sudo docker-compose restart`
## Troubleshooting

### I get a blank logo and nothing else:
There are a couple of possibilities for why this happens. 
- The first is that the IP address of your device doesn't match the one in the `docker-compose.yml` file. These need to match. **Note:** Remember that you cannot use `localhost` or `127.0.0.1`.

- Alternatively, it may because docker has got itself confused with its network interfaces. From the same folder as the `docker-compose.yml` file, run:

    ```
    sudo docker-compose down
    ```

    and then restart the container by running:

    ```
    sudo docker-compose up -d
    ```
