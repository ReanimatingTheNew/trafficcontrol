#TO Client Library Golang
_This version of the SDK is deprecated in favor of the newer [TO API v1.3 Client Library](https://github.com/apache/incubator-trafficcontrol/tree/master/traffic_ops/client/v13)_

##Getting Started
1. Obtain the latest version of the library

`go get github.com/apache/incubator-trafficcontrol/traffic_ops/client`

2. Get a basic TO session started and fetch a list of CDNs
```
package main

import (
	"fmt"
	"os"
	"time"

	"github.com/apache/incubator-trafficcontrol/lib/go-tc/v13"
	toclient "github.com/apache/incubator-trafficcontrol/traffic_ops/client"
)

const TOURL = "http://localhost"
const TOUser = "user"
const TOPassword = "password"
const AllowInsecureConnections = true
const UserAgent = "MySampleApp"
const UseClientCache = false
const TrafficOpsRequestTimeout = time.Second * time.Duration(10)

func main() {
	session, remoteaddr, err := toclient.LoginWithAgent(
		TOURL,
		TOUser,
		TOPassword,
		AllowInsecureConnections,
		UserAgent,
		UseClientCache,
		TrafficOpsRequestTimeout)
	if err != nil {
		fmt.Printf("An error occurred while logging in:\n\t%v\n", err)
		os.Exit(1)
	}
	fmt.Println("Connected to: " + remoteaddr.String())
	var cdns []v13.CDN
	cdns, _, err = session.GetCDNs()
	if err != nil {
		fmt.Printf("An error occurred while getting cdns:\n\t%v\n", err)
		os.Exit(1)
	}
	for _, cdn := range cdns {
		fmt.Println(cdn.Name)
	}
}
```