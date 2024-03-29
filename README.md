# Terraria Sever Docker configuration and setup

## Basic guide for installation

Firstly, download Docker itself and test it using a basic docker like hello-world

```sh
sudo docker run hello-world
```
Also you need to add yourself in the docker group (search it and make one) to not use sudo again and again

Now here comes the actual thing:

```sh
# ":latest" will pull the most recent Terraria version.
docker pull ghcr.io/beardedio/terraria:latest
```

## Generating a new world
To run with out user intervention Terraria Server needs to be configure to use an already generated world. This means you can use one that you have already generated or you can generate one via docker by running this command:
```
sudo docker run --rm -it -p 7777:7777 \
    -v $HOME/terraria/config:/config \
    --name=terraria \
    ghcr.io/beardedio/terraria:latest
```
You can then follow the prompts to create a new world.

## Starting your server with a preexisting world
The world file needs to exist in the config folder.
To start a server using an already generated world, use this command:
```
sudo docker run --rm -dit \
  --name=terraria \
  -v $HOME/terraria/config:/config \
  -e world=<world_file_name> \
  -p 7777:7777 \
  ghcr.io/beardedio/terraria:latest
```

If you get an error from docker saying the container name already exists, it means you need to remove your old docker container process.
`sudo docker rm terraria`

If you want to reattach to any running containers:
`sudo docker attach terraria`
Now you can execute any commands to the terraria server. Ctrl-p Ctrl-q will detatch you from the process.

## Interacting with the Server

To send commands to the server once it has started, use the following command on your Host machine. The below example will send "Hello World" to the game chat.

```bash
docker exec terraria inject "say Hello World!"
```
You can alernatively use the UID of the container in place of `terraria` if you did not name your configuration.

## Another tip:

If you are stuck behind a NAT router (like me), It would be pretty good to use a software called ngrok, which tunnels your network outwards. Because I like dockers, I just followed the guide by Hardware Haven and used his [docker image](https://hub.docker.com/r/hardwarehaven/ngrok2discord#!) to get a notification on discord (yay!). Also please get a ngrok account (free one would suffice) or else it won't work.
If you dont wanna use Ngrok, there is a way to utilise a VPN to simulate a V-LAN. The guide is [right here](https://github.com/Sid-352/Terraria-server/blob/main/Tailscale.md).

BUT before you do this, you need ngrok-systemd and used the web-addr flag in the configuration file instead of just using localhost (won't work without it)

## Notes
Pulled off from [here](https://github.com/beardedio/terraria/blob/main/README.md) and Hardware Haven's 3 videos
(just changed enough to get it working for Terraria):

Also, he used a different distro in the first video and Ubuntu server later on.
1. [Incredible budget home server!](https://youtu.be/72D3MvPk3Xs?si=ipsmi4XTT6g1b_x1)
2. [Building a minecraft server with 12 yr old pc](https://youtu.be/eIHiRW4QH6I?si=7t0eujgKF19Qx1zP)
3. [Host a game server when your isp doesnt want you to](https://youtu.be/SZmc5uoNCko?si=bxWIzCUZ4zhhWPnz)
