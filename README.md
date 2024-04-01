# About this fork
- Simplified script by removing the array to store multiple zoneIDs and domainIDs. May not be viable if DDNS for multiple domains and interfaces are needed, but confirmation is needed.
- Fixed resolving the IP if proxied, by requesting it from Cloudflare's API. The original script only used a lookup, which is fine for a DNS only record.
- Readme has been translated and adapted to the fork.

# RouterOS-DDNS-Cloudflare
RouterOS script for Cloudflare DDNS using API_Token as authorization.

### 1. Environment preparation
1. You need to import `JParseFunctions` into `scripts` of RouterOS
    After importing, run the following command in the RouterOS terminal
    `/system script run "JParseFunctions"; global JSONLoad; global JSONLoads; global JSONUnload`
    This will need run after every startup, create a Scheduler task id needed.
2. Get API_TOKENS from Cloudflare
    Note that this script does not require your API_KEY and email address
    Only `API_TOKENS` with `Edit Zone DNS` permission is required to complete the task
3. Import `ros-ddns-sample` into `scripts` of RouterOS
### 2. Using scripts
1. Modify the corresponding key value according to the prompts in the `ros-ddns-sample` file
    What you need to enter is `uniqueID` , `WANInterface` , `CFdomain` , `CFzone` , `TTL` , `CFproxied` , `CFapitoken`, `cTimestamp`
2. `uniqueID` must be unique, it is used to record `zoneID` and `domainID`
    Setting the same `uniqueID` for multiple DDNS scripts causes DNS records to be incorrectly updated
3. `TTL` unit is seconds, minimum is 60
4. `CFproxied` is used to switch `Cloudflare's DNS Proxy` function (orange cloud icon)
5. `WANInterface` fill in the target interface name to obtain the ip
(For pppoe dial-up, fill in the pppoe interface name)
6. Set up a Scheduler task to run the script at the desired interval

### 3. Cleanup
1. Run `$JSONUnload` in RouterOS terminal
    This will automatically clear all global variables loaded by `JParseFunctions`

# Thanks: 
https://github.com/Winand/mikrotik-json-parser  
https://github.com/kiss2u/ros-cloudflare-ddns  
