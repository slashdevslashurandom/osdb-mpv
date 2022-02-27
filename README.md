# OSDb-mpv

OpenSubtitles automatic downloader script for [MPV](http://mpv.io/). Relies on LuaSocket, lua-xmlrpc and lua-zlib.

# Prerequisites

Obviously, you need to install MPV first.

*lua-xmlrpc* and its dependencies are available on LuaRocks:

    luarocks install luaxmlrpc lua-zlib

MPV is using Lua 5.2 by default, so it's recommended to use LuaRocks for the same version of Lua.

Alternatively, one can use distribution Lua packages (confirmed working on Ubuntu 16.04 and derivatives):

    sudo apt-get install lua-socket lua-xmlrpc lua-zlib
    # Currently, symlink is required to be able to use xmlrpc in Lua 5.2
    sudo ln -s /usr/share/lua/5.1/xmlrpc /usr/share/lua/5.2/xmlrpc

# Installation

Just drop *osdb.lua* and *osdb-rpc.lua* into **~/.mpv/scripts** (or **~/.config/mpv/scripts**).

# Configuration

At the moment, this plugin has the following options:

    user=foo
    password=bar

Optional credentials to use with OpenSubtitles API - your login and password that you use on opensubtitles.org.

    autoLoadSubtitles=[yes|no]

Automatically load subtitles when a file is loaded. Default is 'no'.

    numSubtitles=10

Number of matching subtitles to query from OpenSubtitles. Default is 10. Maximum allowed is 500.

    languages={'eng'}

An array of subtitle language options to search for. Default is 'eng'. Each value in the array can be a language name or can be multiple language names, comma-separated. If you specify multiple values (for example, `{'eng','rus'}`), then you can use the "change language" hotkey (Ctrl+L by default) to choose which language to search for. If you specify multiple language names in one value (for example, `{'eng,rus'}`), then the search will include them both.

    autoFlagSubtitles=[yes|no]

Flag subtitles automatically when switching to the next subtitle suggestion. Default is 'no'.

You can either add those to MPV configuration file, for example:

    script-opts=osdb-autoLoadSubtitles=yes,osdb-numSubtitles=100

Or create a separate lua-settings/osdb.conf file with following contents:

    autoLoadSubtitles=yes
    numSubtitles=100
    user=foo
    password=bar

# Usage

If *autoLoadSubtitles* is enabled, subtitles will be found automatically when a file is loaded.

Otherwise, press **Ctrl+F** to search for subtitles.

To cycle through different subtitles found on OSDb, press **Ctrl+F** again.

To flag a subtitle, if it has invalid timings and/or designed for another release of the same movie, press **Ctrl+R**.

To swap between different languages, use **Ctrl+L**. After that, searching with **Ctrl+F** will return the first subtitle matching that language.
