<h1 align="center">Twitter-Archive</h1>
<p align="center"
<a href="https://github.com/jarulsamy/Twitter-Archive/actions"><img alt="Action Status" src="https://github.com/jarulsamy/Twitter-Archive/actions/workflows/python-version-test.yml/badge.svg"></a>
<img alt="Python Versions" src="https://img.shields.io/pypi/pyversions/Twitter-Archive">
<a href="https://pypi.org/project/Twitter-Archive/"><img alt="PyPI" src="https://img.shields.io/pypi/v/Twitter-Archive"></a>
<img alt="Total LOC" src="https://img.shields.io/tokei/lines/github.com/jarulsamy/twitter-bookmark-downloader">
<a href="https://github.com/psf/black"><img alt="Code style: black" src="https://img.shields.io/badge/code%20style-black-000000.svg"></a>
<a href="https://github.com/jarulsamy/Twitter-Archive/blob/master/LICENSE"><img alt="License" src="https://img.shields.io/github/license/jarulsamy/Twitter-Archive"></a>
</p>

A CLI Python application to download all media (and hopefully more) from
bookmarked tweets (for now). Eventually I hope to make this a general archive
utility for Twitter, allowing users to download/archive all kinds of tweets.

Originally, before the V2 Twitter API, this app used Selenium to try and scrape
the contents of a users bookmarks page. Now, since the release of the V2 API,
the application has been rewritten. This new version is much faster and more
robust.

---

## Installation and Setup

### Installation

_Twitter-Archive_ can be installed with `pip`

    $ pip install twitter-archive

Alternatively, you can fork, clone and install from the repository
instead of from PyPi.
    
    $ Fork the repository
    $ git clone https://github.com//your_username/Twitter-Archive
    $ cd Twitter-Archive
    $ pip install -r requirements.txt

To properly authenticate with the Twitter API, you will have to create a
developer application. This will provide you with a client ID and client secret.

### Twitter Developer App Setup

1. Create a Twitter developer account here: [Twitter Developer
   Portal](https://developer.twitter.com/en/portal/dashboard)
2. Create an project and application.
3. Generate an OAuth 2.0 client ID and client secret by following this
   documentation: [Twitter API Key and Secret
   Docs](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret)

   > Ensure you grant these scopes: 'tweet.read', 'users.read', and 'bookmark.read'

4. Save your tokens to use with this application.

### Authentication and Usage

There are several options for passing the client ID and client secret to the
application. Only one of the following is required.

#### Option 1: Environment Variables

Set the relevant environment variables as so:

```sh
$ export TWITTER_ARCHIVE_CLIENT_ID="YOUR_CLIENT_ID_HERE"
$ export TWITTER_ARCHIVE_CLIENT_SECRET="YOUR_CLIENT_SECRET_HERE"
```

Now you can use the application until you restart your shell.

#### Option 2: Dotenv Variables

Alternatively to environment variables, you can save your tokens in a `.env`
file in your current working directory. This file is automatically read and
loaded by `twitter-archive` at runtime to load the necessary variables. An
example `.env` file would look like this:

```txt
TWITTER_ARCHIVE_CLIENT_ID=YOUR_CLIENT_ID_HERE
TWITTER_ARCHIVE_CLIENT_SECRET=YOUR_CLIENT_SECRET_HERE
```

#### Option 3: CLI Flags

The tokens can also be passed in as CLI flags, but this is generally discouraged
as most shells keep a history of commands entered, and this obviously risks
leaking your keys. For example:

```sh
$ twitter-archive --client-id="YOUR_CLIENT_ID_HERE" --client-secret="YOUR_CLIENT_SECRET_HERE"
```

#### Usage

You can then invoke the app with:

    $ twitter-archive

By default, the app will print a URL to prompt the user to authorize the
application with Twitters official APIs. Once you navigate to that link and
login with Twitter, the app will fetch a manifest of all the bookmarked tweets
and begin saving any photos/videos to disk.

You can view the built-in CLI help menu for more info:

```txt
$ twitter-archive --help
Usage: twitter-archive [--client-id ID] [--client-secret ID] [--headless] [--no-clobber] [--num-download-threads N] [--quiet]
                       [-o FILE] [-i FILE | -m FILE] [-v] [--version] [--help]

A CLI Tool to archive tweets v0.0.7

Options:
  --client-id ID        Specify the client ID. (default: None)
  --client-secret ID    Specify the client ID. (default: None)
  --headless            Don't use interactive authentication. (default: False)
  --no-clobber          Don't redownload/overwrite existing media. (default: False)
  --num-download-threads N
                        Number of threads to use while downloading media. (default: 8)
  --quiet               Disable download progress bars (default: False)
  -o FILE, --media-output FILE
                        Path to output downloaded media. (default: media)
  -i FILE, --manifest-input FILE
                        Use an existing manifest and download all media. (default: None)
  -m FILE, --manifest-output FILE
                        Path to output bookmark manifest. (default: bookmark-manifest.json)
  -v, --verbose
  --version             show program's version number and exit
  --help                Show this help message ane exit.
```

## Acknowledgment

The Twitter developer team did an excellent job on the new APIs. The new APIs
are substantially more intuitive and allow us to interact with many more
features of Twitter. While it did take two years, the openness, transparency,
and attention to feedback is much appreciated!

The relevant forum post is available
[here](https://twittercommunity.com/t/build-with-bookmarks-on-the-twitter-api-v2/168804).
