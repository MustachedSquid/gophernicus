# Gophernicus

<<<<<<< HEAD
Version 3.0
=======
Development! DO NOT USE unless you want fiery dragons!
(you probably want to `git checkout 3.0`)
>>>>>>> docs

*Copyright (c) 2009-2019 Kim Holviala and others*

Gophernicus is a modern full-featured (and hopefully) secure gopher
daemon. It is licensed under the BSD license.

<<<<<<< HEAD
=======
(If you are looking for installation documentation, please see INSTALL.md).

>>>>>>> docs
## Support/Contact

Developers can be reached at <gophernicus AT gophernicus DOT org>.

Our IRC channel is on irc.freenode.net #gophernicus.

You most likely want to subscribe to the gophernicus mailing list at
https://lists.tildeverse.org/postorius/lists/gophernicus.lists.tildeverse.org/,
especially if you maintain a server. This is where all important announcements
are made.

## Command line options

    -h hostname   Change server hostname (FQDN)      [$HOSTNAME]
    -p port       Change server port                 [70]
    -T port       Change TLS/SSL port                [0 = disabled]
    -r root       Change gopher root                 [/var/gopher]
    -t type       Change default gopher filetype     [0]
    -g mapfile    Change gophermap file              [gophermap]
    -a tagfile    Change gophertag file              [gophertag]
    -c cgidir     Change CGI script directory        [/cgi-bin/]
    -u userdir    Change users personal gopherspace  [public_gopher]
    -l logfile    Log to Apache-compatible combined format logfile

    -w width      Change default page width          [76]
    -o charset    Change default output charset      [US-ASCII]

    -s seconds    Session timeout in seconds         [1800]
    -i hits       Maximum hits until throttling      [4096]
    -k kbytes     Maximum transfer until throttling  [4194304]

    -f filterdir  Specify directory for output filters
    -e ext=type   Map file extension to gopher filetype
    -R old=new    Rewrite the beginning of a selector

    -D text|file  Set or load server description for caps.txt
    -L text|file  Set or load server location for caps.txt
    -A admin      Set admin email for caps.txt

    -nv           Disable virtual hosting
    -nl           Disable parent directory links
    -nh           Disable menu header (title)
    -nf           Disable menu footer
    -nd           Disable dates and filesizes in menus
    -nc           Disable file content detection
    -no           Disable charset conversion for output
    -nq           Disable HTTP-style query strings (?query)
    -ns           Disable logging to syslog
    -na           Disable autogenerated caps.txt
    -nt           Disable /server-status
    -nm           Disable shared memory use (for debugging)
    -nr           Disable root user checking (for debugging)
    -np           Disable HAproxy proxy protocol
    -nx           Disable execution of gophermaps and scripts
    -nu           Disable personal gopherspaces

    -d            Debug output in syslog and /server-status
    -v            Display version number and build date
    -b            Display the BSD license
    -?            Display this help

(end of option list) -- keep this line for automatic extraction!

## Setting up a gopher site

After succesfully installing Gophernicus (see [INSTALL](./INSTALL.md)) you need to set
up the gopher root directory. By default Gophernicus serves documents
from /var/gopher so start by creating that directory and making sure
it's world-readable. Then, simply add files and directories under your
root, fire up a gopher browser (Firefox with the OverbiteFF extension,
Lynx) and open up `gopher://HOSTNAME/`
(where `HOSTNAME` is your server hostname).

That's it, your first gopher site is now up and running. If the links
on the root menu don't work make sure you are using the `-h HOSTNAME`
parameter in your configuration (with a valid resolveable hostname
instead of `HOSTNAME` - see INSTALL).

## Security

Gophernicus has been written with high security in mind. There should
be no buffer overflows or memory allocation problems so it should be
safe to run a publicly available gopher server with Gophernicus.

However, the security settings (which are non-changeable) are so strict
that you need to keep one thing in mind. Gophernicus will only serve
world-readable content. Being readable by the server process is not
enough, all files and directories MUST be world-readable or they are
simply hidden from all listings and denied if a client asks for them.

The `-nx` option prevents execution of any script or external file,
and the `-nu` option suppresses scanning for and serving of `~user`
directories (which are normally at `~/public_html/` for each user).

## Gophermaps

By default all gopher menus are automatically generated from the
content of the directory being viewed. If you want to have
informational text along with the files, or if you want to completely
replace the generated menu with your own you need to take a look at
gophermaps. See the [README.gophermap](./README.gophermap) for more information.

## Gophertags

A gophertag file can be used to virtually rename a directory. Let's
assume that you have a directory called "foo" somewhere - it will
be listed as "foo" in all automatically generated menus. Now if you
create a file foo/gophertag and put the text "bar" into it the menus
will show "bar" but the links will still point to "foo". This is
useful for creating descriptive names for directories without
littering the file system with spaces and weird characters.

## Personal gopherspaces

Gophernicus supports users personal gopherspaces. If a user has
world-readable directory called `public_gopher` under his home, a
request for `gopher://HOSTNAME/1/~user/` will serve documents from
that directory.

This is suppressed if the `-nu` option is given.
In this case, any `~` entry which otherwise initiates listing
of user directories will be displayed literally.

## Virtual hosting

Gophernicus supports virtual hosting, or serving more than one logical
domain using the same IP address. Since gopher (RFC1436) doesn't
support virtual hosting this requires some hacks.

To enable virtual hosting create one or more directories under your
gopher root which are named after your domain names. The primary vhost
directory (set with the `-h HOSTNAME` option) must exist or virtual
hosting will be disabled. Then simply add content to the hostname
directories and you're (kind of) up and running.
<<<<<<< HEAD

There is a serious issue with virtual hosting.

As stated previously, RFC1436 dosen't support virtual hosting. Clients won't
like it.

How the virtual hosting works, is that it loops through the vhosts looking for
the selector. As you might think, the root gophermap exists on all of the
vhosts, meaning it might not use the correct vhost. There is currently no easy
way to fix this.

It is recommended to add '%' on a line by itself to the bottom of your root
gophermaps. This will add "special" links of the format example.com/;example.com
which forces the correct vhost.
=======

There is a serious issue with virtual hosting.

As stated previously, RFC1436 dosen't support virtual hosting. Clients won't
like it.

How the virtual hosting works, is that it loops through the vhosts looking for
the selector. As you might think, the root gophermap exists on all of the
vhosts, meaning it might not use the correct vhost. There is currently no easy
way to fix this.

It is recommended to add '%' on a line by itself to the bottom of your root
gophermaps. This will add "special" links of the format example.com/;example.com
which forces the correct vhost. 
>>>>>>> docs

## CGI support

Gophernicus supports most parts of the CGI/1.1 standard. Most standard
CGI variables are set, and some non-standard ones are added.

By default all scripts and binaries under any directory called
`/cgi-bin/` are executed as CGI scripts (this includes cgi-bin
directories under users personal gopherspaces). Also, if a gophermap
is marked executable it is also processed as an CGI script.

As with regular files, CGI scripts must be world-executable (and
readable) or they will be ignored. Make sure your CGI script is safe
with ANY user input as poorly coded CGI scripts are the number 1
security problem with publicly open Unix/Linux/BSD servers.

The `-nx` option prevents execution of any script or external file.
In this case, they will be simply ignored and no output is given.

## Output filtering and PHP support

In addition to CGI scripts Gophernicus supports output filtering
scripts. By default output filtering is turned off, but you can turn
it on by using the `-f FILTERDIR` option, creating that directory
and creating one or more scripts in there named by either the file
suffix, or by the gopher filetype char.

If a file is to be served out which matches either the file suffix
script, or the filetype script then instead of simply sending the
file to client the output filter script is executed with the
original file as the first parameter and the output of the script
is then sent to client.

For PHP support install the CLI version of the PHP interpreter and
then symlink (or copy) that binary to the directory specified with
-f option using the destination name "php".

    $ ln -s /usr/bin/php5-cli /usr/lib/gophernicus/filters/php

After that all files with the php suffix will be "filtered" through
the PHP command line interpreter. In other words, PHP starts working.
And don't use the CGI version of PHP as it outputs HTTP headers the
gopher protocol doesn't have.

## Charset support and conversions

Gophernicus supports three charsets: US-ASCII, ISO-8859-1 and UTF-8.
All textual input is internally upconverted to UTF-8 and then
downconverted to whatever charset the client is asking for. The
conversion is input autosensing which means that you don't have to
specify your filesystem charset, or the charset of your text files -
it's all detected automatically.

With standard gopher clients this is a bit of a problem as your text
files WILL be converted to 7-bit US-ASCII. This means that all 8-bit
charaters WILL BE LOST. This decision was made because no gopher
client that I tested was reliably cabable of decoding anything else
than pure US-ASCII. If you want to disable the conversion use the
`-no` option, or if you'd like to change the default output charset to
something else than US-ASCII just use for example the `-o ISO-8859-1`
option.

## Selector rewriting

Selector rewriting lets you rewrite parts of the selector on the fly.
Well, not parts, but really just the start of it. And the rewrite
enging here is nothing like Apache's mod_rewrite as I was too lazy
to integrate any regex libraries... So, all it does is rewrite a
fixed string at the start of the selector to something else. This
will let you move your directories around while making sure that
existing deeplinks still work.

Examples:

    -R "/~user=/~luser"
    -R "/old-dir=/new-dir"


## Session tracking and statistics

To enable virtual hosting with gopher (RFC1436) clients Gophernicus
tracks users and their session. As a side effect of that session
tracking, Gophernicus has simple throttling controls to keep nasty
users from killing your precious 120MHz PPC 604e server from dying
under the load. The throttling defaults are high enough that normal
human users will never hit the limits, but it's possible (and mostly
preferrable) that a badly behaving crawling agent will be throttled.

The current sessions and other real-time status data can be viewed
by opening the URL `gopher://HOSTNAME/0/server-status` . This status
view has been modeled after the Apache server-status which means
that it's possible to integrate Gophernicus into existing server
monitoring systems. To ease up such integrations, Gophernicus
supports HTTP requests of the server-status page using an URL like
`http://HOSTNAME:70/server-status?auto` .

## TLS/SSL and proxy support

As of version 2.3 Gophernicus supports the HAproxy proxy protocol
version 1. This makes it possible to build a cluster of gopher servers
and use HAproxy in front of them all handling client routing to different
backend servers.

More useful is putting Gophernicus behind Stunnel4 for TLS/SSL support
and use the same proxy protocol to tell Gophernicus the correct remote IP
address. The below sample stunnel configuration is all you need to
TLS-enable your gopher server. Well, you'll need a certificate too and for
that I recommend Let's Encrypt.

In addition to configuring Stunnel for TLS you should add `-T TLSPORT`
to Gophernicus options so that it knows which connetions are coming in
encrypted and which are not. Using proper `-T` also makes it possible for
CGI programs to use the `$TLS` environment variable to know whether the
current request was encrypted or not.

Example:

    ;
    ; Gophernicus behind Stunnel4 for gopher over TLS
    ;
    
    ; User/group for stunnel daemon
    setuid = stunnel4
    setgid = stunnel4
    
    ; PID file location
    pid = /var/run/stunnel4/gophernicus.pid
    
    ; Log to file, not syslog
    output = /var/log/stunnel4/gophernicus.log
    syslog = no
    
    ; Certificate in pem format is needed for TLS
    cert = /etc/ssl/private/gophernicus.pem
    
    ; Enable TCP wrappers
    libwrap = yes
    service = gophernicus-tls
    
    ; Gopher over TLS service
    [gophernicus]
    accept  = :::7070
    connect = 127.0.0.1:70
    protocol = proxy
