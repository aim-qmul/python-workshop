# Setting up SSH for AIM

The official docs for this can be found here: http://support.eecs.qmul.ac.uk/services/ssh/

## SSH keys

Before doing anything on the servers, you should have created an SSH key and copied it to the 
login server (which is `frank` for PhDs). If you haven't done this yet, follow the instructions 
for your operating system under "SSH Keys" here http://support.eecs.qmul.ac.uk/services/ssh/

## SSH config

I recommend setting up an SSH config to make it easier to work with the servers.

Edit the file `~/.ssh/config` to look like the following (remember to replace `<__YOUR_USERNAME_GOES_HERE__>` with your username):

```
# Read more about SSH config files: https://linux.die.net/man/5/ssh_config

# The following lines help to keep the connection alive for longer
ServerAliveInterval 15
ServerAliveCountMax 20

# frank is the only server which is accessible from the outside world
# This setup is commonly used to increase the security of the machines
# It is known as a "bastion host" or a "jump host" if you need to google it
Host frank
    HostName frank.eecs.qmul.ac.uk
    User <__YOUR_USERNAME_GOES_HERE__>
    IdentityFile ~/.ssh/id_rsa
    
# The following is an example of one of the compute servers
# By specifying `ProxyCommand`, you don't need to login to frank before running commands
Host epstein
    HostName epstein.eecs.qmul.ac.uk
    User <__YOUR_USERNAME_GOES_HERE__>
    IdentityFile ~/.ssh/id_rsa
    ProxyCommand ssh -q -W %h:%p frank
    
# ... more server names and configs go here ...
```

## Logging into servers via SSH

With the above config in place, you should be able to run:

```
ssh epstein
```

## SSH Tunneling / port forwarding

Sometimes it can be useful to send data to a specific port but these are typically blocked by a firewall.

For example, if a jupyter notebook server is serving HTTP requests on port 8888 on the `epstein` server, ideally 
you would visit http://epstein.eecs.qmul.ac.uk:8888 but that port is blocked.

Instead, you can use a local port (which is not blocked) and then use SSH to forward the data to the remote server like so:

```
ssh -J <YOUR_USERNAME_HERE>@frank.eecs.qmul.ac.uk <YOUR_USERNAME_HERE>@epstein.eecs.qmul.ac.uk -NL 8888:localhost:8888
```

If you setup your `~/.ssh/config` file as described above, you can use this command instead:

```
ssh epstein -NL 8888:localhost:8888
```

The last part of the command uses the following flags:

```
-N Do not execute a remote command.  This is useful for just forwarding ports.
```

and

```
-L Specifies that connections to the given TCP port or Unix socket on the local (client) host are to be forwarded to the given host
             and port, or Unix socket, on the remote side.
```

There are a few formatting options for `-L`. In this case, we use `<local_port>:<remote_hostname>:<port_on_remote_host>`.
