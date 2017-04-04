..................... dotjs-ubuntu .................

dotjs-ubuntu  is a  Google Chrome  extension  that 
executes JavaScript files in `~/.js` based on their 
filename. 

  This version of dotjs is maintained for
  users under Ubuntu. The original dotjs for Mac OSX
  can be found here: `https://github.com/defunkt/dotjs`

If  you navigate to  `http://www.google.com/`, dotjs
will execute `~/.js/google.com.js`.

This makes it super  easy to spruce up your favorite
pages using JavaScript.

On subdomains such as `http://gist.github.com` dotjs
will try to load `~/.js/gist.github.com.js`  as well
as `~/.js/github.com.js` and `~/.js/com.js`.

Bonus:  files  in `~/.js`  have jQuery 1.9  loaded,
regardless  of  whether  the  site  you're  hacking
uses jQuery.

Double bonus: `~/.js/default.js`  is loaded on every
request,  meaning you  can stick  plugins  or helper
functions in it.

GreaseMonkey user scripts are great, but you need to
publish them  somewhere and re-publish  after making
modifications. With dotjs, just add or edit files in
`~/.js`.

## Example

    $ cat ~/.js/github.com.js
    // swap github logo with trollface
    $('a.header-logo-blacktocat').html(
        $('<img>')
            .attr('src', '//bit.ly/ghD24e')
            .css({'width': 'auto', 'height': '22px'})
        );

![](http://puu.sh/1Kjvw)

## How It Works

Chrome extensions can't access the local filesystem,
so dotjs  runs a tiny  web server on port  3131 that
serves files out of ~/.js.

The ```dotjs``` executable is installed into `~/bin`
and then should be added into [crontab](#install),
so that the server's started when the OS starts.

The dotjs Chrome extension then makes ajax requests
to http://localhost:3131/convore.com.js any time you
hit a page on convore.com, for example, and executes
the returned JavaScript.

# SSL certificate

In Google Chrome the server will give an error saying that the Certificate Authority is invalid.
You can simply go to: Settings > Show advanced settings > HTTPS/SSL > Manage certificates > Authorities > Import
Here you can upload the `cert.pem` file in this project.

## Requires

- Ubuntu
- Ruby 1.8
- rake (gem install rake)
- Google Chrome
- `/path/to/home/bin` in your $PATH

## Install

    git clone https://github.com/glenbot/dotjs-ubuntu.git
    cd dotjs-ubuntu
    rake install

After installation add the following line to your crontab

    $ crontab -e
    @reboot /path/to/home/bin/djsd -d

For the impatient run the daemon right away

    djsd -d

For the patient reboot and enjoy!

Now open https://localhost:3131 in Chrome and enable the SSL.

Then install the Google Chrome extension:

http://bit.ly/dotjs

## Uninstall

    rake uninstall

## Credits

- Dotjs (OSX) <https://github.com/defunkt/dotjs>
- Icon: <http://raphaeljs.com/icons/>
- jQuery: <http://jquery.com/>
- Ryan Tomayko for:

> "I almost wish you could just
   stick JavaScript in ~/.js. Do
   you know what I'm saying?"

## Windows

- [dotjs-win](https://github.com/p3lim/dotjs-win)

## Other Browsers

- [Firefox Add-on](https://github.com/rlr/dotjs-addon)
- [Safari Extension](https://github.com/wfarr/dotjs.safariextension)
- [Fluid UserScript](https://github.com/sj26/dotjs-fluid)
