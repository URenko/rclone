---
title: "Terabox"
description: "Rclone docs for Terabox"
versionIntroduced: "v1.70"
---

# {{< icon "fa fa-inbox" >}} Terabox

This is a Backend for Terabox Cloud storage (beta). 

**Notice** This integrations is not official, because official integration required special `client id` and `client secret` which only can be provided by Terabox. I made a few requests for this, but did not got a responce, yet. If Terabox will provide the keys for official integration, will update the integration.

Paths are specified as `remote:path` or `remote:/path`

Paths may be as deep as required, e.g. `remote:directory/subdirectory`.


## Limitations

**For now** max upload filesize is 4GB. That's mean if you have a paid account, you will still limit as free account.

Download in multithread mode and single thread mode has the same speed result.  Got about 1.7 - 1.9 MB/s for standart multithread download and the same result for one thread (with key`--multi-thread-streams 1`)

Looks like cookie live period is 1 year, I start develop a few months ago, my cookie still works.


## Configuration

To configure an Terabox backend you need provide cookie from your logined account. The field accepts one of two input options:

1) only `ndus` value.
2) **full** cookie string.


How to obtain the cookie:
* Chrome extension:
    1) Install extension `Cookie viewer`: https://chromewebstore.google.com/detail/dedhcncdjkmjpebfohadfeeaopiponca?utm_source=item-share-cb
    2) Go to your storage: https://www.terabox.com/main
    3) On search panel exrtensions click to Cookie viewer and copy `ndus` value, insert it to configuration.
    4) Remove extension `Cookie viewer`

* Chrome dev:
    1) Go to your storage https://www.terabox.com/main
    2) Right top corner `three dots` > `More tools` > `Developer tools` (**Note** The page will be automaticaly redirected to `about:blank`, no worries, it's ok.)
    3) Select `Network` tab and check `Preserve log`
    4) Push to `Go Back` button on address panel
    5) Select any request and scroll `Headers` tab to down under `Request headers` and copy cookie value.
    6) Close dev tools

Here is an example of how to make a remote called `remote` with the default setup.
First run:

    rclone config

This will guide you through an interactive setup process:

```
e) Edit existing remote
n) New remote
d) Delete remote
r) Rename remote
c) Copy remote
s) Set configuration password
q) Quit config
e/n/d/r/c/s/q> n
name> remote
Type of storage to configure.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
[...]
52 / Terabox
   \ "terabox"
[...]
Storage> terabox

Option cookie.
Set full cookie string from browser or only 'ndus' value from cookie string
Enter a value.
cookie> xxx

Edit advanced config? (y/n)
y) Yes
n) No (default)
y/n> n

Configuration complete.
--------------------
[terabox]
type = terabox
cookie = xxx
--------------------
Keep this "remote" remote?
y) Yes this is OK (default)
e) Edit this remote
d) Delete this remote
y/e/d> 
```
Once configured you can then use `remote` like this,

List directories in top level of your Terabox

    rclone lsd remote:

List all the files in your Terabox

    rclone ls remote:

To copy a local directory to a Terabox directory called backup

    rclone copy /home/source remote:backup


{{< rem autogenerated options start" - DO NOT EDIT - instead edit fs.RegInfo in backend/terabox/terabox.go then run make backenddocs" >}}
### Standard options

Here are the Standard options specific to Terabox.

#### --terabox-cookie

Your cookie.

Properties:

- Config:      cookie
- Env Var:     RCLONE_TERABOX_COOKIE
- Type:        string
- Required:    true

### Advanced options

Here are the Advanced options specific to Terabox.

#### --terabox-upload-threads

How many parallels chunks will be upload. (Be careful with this setting, you can got a ban)

Properties:

- Config:      upload_threads
- Env Var:     RCLONE_TERABOX_UPLOAD_THREADS
- Type:        uint8
- Default:     3

#### --terabox-delete-permanently

Set if you want to clean Trash bin after file deleted.

Properties:

- Config:      delete_permanently
- Env Var:     RCLONE_TERABOX_DELETE_PERMANENTLY
- Type:        bool
- Default:     false

#### --terabox-user-agent

Set if you want to to change default user agent.

Properties:

- Config:      user_agent
- Env Var:     RCLONE_TERABOX_USER_AGENT
- Type:        string
- Default:     "terabox;1.37.0.7;PC;PC-Windows;10.0.22631;WindowsTeraBox",

#### --terabox-debug-level

Set extra verbose level from 0 to 4.
* 0 - none
* 1 - Caled functions and params
* 2 - response from terabox (params and body)
* 3 - request to terabox (params)
* 4 - request to terabox (body)

Properties:

- Config:      debug_level
- Env Var:     RCLONE_TERABOX_DEBUG_LEVEL
- Type:        uint8
- Default:     0,

#### --terabox-encoding

The encoding for the backend.

See the [encoding section in the overview](/overview/#encoding) for more info.

Properties:

- Config:      encoding
- Env Var:     RCLONE_TERABOX_ENCODING
- Type:        Encoding
- Default:     Slash,LtGt,DoubleQuote,BackQuote,Del,Ctl,LeftSpace,InvalidUtf8,Dot

#### --terabox-description

Description of the remote.

Properties:

- Config:      description
- Env Var:     RCLONE_TERABOX_DESCRIPTION
- Type:        string
- Required:    false

{{< rem autogenerated options stop >}}
