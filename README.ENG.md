## Clash Config Builder
Clash configuration file online definition

### address
Online address: https://fndroid.github.io/clash-config-builder/

### Notice
**The Clash configuration address provided by the service provider is generally [CORS](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS), so by default this tool will proxy it through the API Request, if you are concerned about privacy issues, please use [Local Mode](#local-mode)! ! ! **


### Steps for usage
#### 1. Edit the basic configuration file
Click "Raw Config" at the top of the interface, fill in the following basic configuration and return to the main interface.
```yaml
proxies: []
proxy-groups:
   - name: UrlTest
     type: url-test
     proxies:
       - DIRECT
     url: http://www.gstatic.com/generate_204
     interval: 300
   - name: PROXY
     type: select
     proxies:
       - UrlTest
   - name: Final
     type: select
     proxies:
       - PROXY
       - DIRECT
   - name: Apple
     type: select
     proxies:
       - DIRECT
       - PROXY
   - name: GlobalMedia
     type: select
     proxies:
       - PROXY
   - name: HKMTMedia
     type: select
     proxies:
       - DIRECT
rules:
   - RULE-SET,https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/Unbreak.list,DIRECT
   - RULE-SET,https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/GlobalMedia.list,GlobalMedia
   - RULE-SET,https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/HKMTMedia.list,HKMTMedia
   - RULE-SET,https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/Global.list,PROXY
   - RULE-SET,https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/Apple.list,Apple
   - RULE-SET,https://raw.githubusercontent.com/ConnersHua/Profiles/master/Surge/Ruleset/China.list,DIRECT
   - GEOIP,CN,DIRECT
   -MATCH,Final

```

#### 2. Fill in the Clash hosting subscription
Click "Subscriptions" at the top of the interface, fill in the Clash configuration file address (one per line) provided by the service provider in the window that opens, and return to the main interface after completion.

#### 3. Synchronize node information
Click the Sync Proxies button at the bottom of the main interface to pull the node. The node will be generated in the More list on the right.

#### 4. Edit policy group
Drag the node in ``More`` to the ``Proxies`` list to add the node to the corresponding policy group. On the contrary, dragging the node from ``Proxies`` to ``More`` will remove it from the policy. The node

#### 5. Generate configuration
After clicking "Download Profile" at the bottom of the interface, the browser will prompt you to download


### model

#### Remote Mode
 
This is the default mode of this tool. In this mode:
- Subscriptions node acquisition will be proxied through the remote API (cloudcompute.lbyczf.com)
- The final configuration file will be downloaded through the browser

#### Local Mode

This mode requires starting a server locally. In this mode:
- Subscriptsions node acquisition will be through the local server proxy, no privacy issues
- The final configuration file can directly wake up Clash for Windows for updates
- Can be mounted and run in Clash for Windows

##### Configuration method

1. Download ``clash-config-builder-server.exe``, address: https://github.com/Fndroid/clash-config-builder-server/releases
2. Enter the General interface in Clash for Windows, click the small font below ``General YML`` to open text editing
3. Enter at the end of the file:
     ```yaml
     cfw-child-process:
       - command: clash-config-builder-server.exe
         options:
           cwd: C:\ # The directory where clash-config-builder-server.exe is located
     ```
4. Restart Clash for Windows and refresh the web page. If the green ``Local Mode`` is displayed in the lower right corner, it means the startup is successful.

Reference: https://docs.cfw.lbyczf.com/contents/childprocess.html
