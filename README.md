Redmine/ChiliProject plugin for Supybot/Limnoria
================================================

This Supybot/Limnoria plugin allows IRC Users to display informations about Redmine/ChiliProject issues and direct links to them, directly in an IRC channel.


How this plugin works
---------------------

The information is fetched from [Redmine](http://www.redmine.org/) through it's [Rest API](http://www.redmine.org/projects/redmine/wiki/Rest_api).


How to install and load this plugin
-----------------------------------

1. Clone this project into your supybot's /plugins/ folder, and rename it to 'Redmine'

2. You will need to install [Restkit](http://benoitc.github.com/restkit/) (package python-restkit on Debian), and a bunch of other packages too.

Recommended packages on Ubuntu (probably similar or the same under Debian):

apt-get install python-twisted* python-sqlite python-restkit python-simplejson

3. Load your plugin by messaging your bot: load Redmine

4. At this point the plugin is loaded, and you can find all its configuration variables by typing: config search Redmine


How to enable the REST API and obtain an API Key in Redmine/ChiliProject
------------------------------------------------------------------------

1. Enable the REST API in Administration >> Settings >> Authentication.

2. Click "My Account" and click "Show" under "API Key". This long string of letters and numbers is your API Key.


How to configure
----------------

The following variables are configurable:

 * urlbase: The base URL for the Redmine or ChiliProject instance this plugin will retrieve bug information from.

 * apikey: Your Redmine API key. The Rest API must be enabled in Redmine (Administration -> Settings -> Authentication). You can then get your API Key on your account page ( /my/account ) when logged in, on the right-hand pane of the default layout.

 * bugMsgFormat: Change the message format for bug details, following tokens will be replaced before being printed: \_ID\_, \_URL\_, \_AUTHOR\_, \_CATEGORY\_, \_SUBJECT\_, \_STATUS\_, \_PROJECT\_ .  \_CRLF\_ will split the response in two (or more) lines.

 * bugSnarfer: Determines whether the bug snarfer will be enabled, such that any bug ### seen in the channel will have its information reported into the channel. Channel Specific variable.

 * bugSnarferTimeout: Users often say "RM XXX" several times in a row, in a channel. If "RM XXX" has been said in the last (this many) seconds, don't fetch its data again. If you change the value of this variable, you must reload this plugin for the change to take effect.


Simply message the bot the following messages:

config supybot.plugins.Redmine.urlbase http://your.redmine.url.com
config config supybot.plugins.Redmine.apikey your.api.key.here
config supybot.plugins.Redmine.bugMsgFormat  _TRACKER_ _ID_ (_AUTHOR_) - _STATUS_ : _SUBJECT__CRLF__URL_
config supybot.plugins.Redmine.bugSnarfer True

Notice 1: if your Redmine/ChiliProject is available via HTTPS:// then I recommend that instead of HTTP://

Notice 2: You must 'reload Redmine' after you set config options


How to use
----------

Once the plugin is loaded and (at least) urlbase and apikey are set, you can display informations about a Redmine issue with the "bug #" command, where # is the issue number.
If you enable the bugSnarfer variable for a given channel, you won't need using the "bug" command anymore, just write "bug #", and the bot will automatically display informations about the issue.


Update
------
Get latest version at : https://github.com/veggiematts/supybot-redmine
