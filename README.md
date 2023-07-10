# tasmota-cmd

**tasmota-cmd** allows to execute sequence of commands on Tasmota device
connected to network. With it you can automate setup of Tasmota devices.

## Usage

Program reads commands from stdin, line by line. Each line should be in format
`command=value`.

Most basic usage is to write sequence of commands to file:

```sh
$ cat tasmota_setup
Hostname=mydevice

# comment line (like this) and empty lines are ignored
FriendlyName=My First Device
```

and use that file as an input:

```sh
$ ./tasmota-cmd 192.168.1.101 <tasmota_setup
> GET http://192.168.1.101/cm?cmnd=Hostname%20mydevice
< {"Hostname":"mydevice"}

> GET http://192.168.1.101/cm?cmnd=FriendlyName%20My+first+device
< {"FriendlyName1":"My First Device"}

```

Also it can be used in interactive mode, where user enter one command at once.
To exit that mode user need to write EOF character (press `Ctrl+D`). Example:

```sh
$ ./tasmota-cmd mydevice.lan
Status=8
> GET http://mydevice.lan/cm?cmnd=Status%208
< {"StatusSNS":{"Time":"1970-01-01T00:01:13"}}

```

## Installation


Using `curl`:
```sh
curl -fLO https://raw.githubusercontent.com/macie/tasmota-cmd/master/tasmota-cmd
chmod +x tasmota-cmd
```

or with `wget`:

```sh
wget https://raw.githubusercontent.com/macie/tasmota-cmd/master/tasmota-cmd
chmod +x tasmota-cmd
```

## License

[MIT](https://tldrlegal.com/license/mit-license)
