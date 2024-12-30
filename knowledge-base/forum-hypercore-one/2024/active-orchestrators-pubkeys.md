Thread: active-orchestrators-pubkeys
0x3639 | 2023-06-14 13:49:41 UTC | #1

active orchestrators pub_key

12D3KooWSbX1rY9UYE3xUX2v8FYkMjh3WRTzZdB3zfuN2FMpyw8W
12D3KooWQBKTb3jNeasVCHUvZ8WmRCo6GYeJeatsWQVJKtjqqtF5
12D3KooWQTzQoiTLrD2YYNNZZjjdbzh5CYTiFfCYz9h7LrJWRyMN
12D3KooWRZg6XH18LpEWX5nBWpQNqQRA49r7Pk7QGTPhgKHuECkt
12D3KooWRsgJWukbTb5Uk9GQ4y4kgxCtELsLpKq8oDyPQebEPvcd
12D3KooWAUqGSJB5EXtCCesBPUtqKvUi3Di1FzJLTi9phfG4BZRy
12D3KooWAXk5G1oMJVPTuFGFA7eqo2bKqzCHM2ZpGi1Gd6qC5vuE
12D3KooWBHQRAXyXh9vTF7XckWU3EBLdgWYhWDDTivzxskTGECQr
12D3KooWBuiGGUp5XDTK7RwdTMXQ79SCoL7G8XA94xtRMG5DwwtJ
12D3KooWExeVPndEzjbiuArdUiN4GKAFvme26QGSFx3YkNM5QnjT
12D3KooWGoYbRsMbjuf2PesqN5AFeFojuxNjdF7PqvtfJCqXWrk4
12D3KooWHHU7XdH3RBj1FHPTrmjhPE61bShi4uiALHLtwgLAmxce
12D3KooWHqLbDNdeijummpS3CQHCTNTDnfqsBZWRfERJEJVpgoVU
12D3KooWHxXSV59Xk4LU8pCZniXDbRsG4z4iZ9n8aeNxsgMB5d4B
12D3KooWJMuAUQ7YVtvRT2Qms9D2v2LFAEbrNHQ5vLQFiT1JMx72
12D3KooWKXjWe1DD1yrERztA28ufWjEZLKKneRY7mzrxet3183YT
12D3KooWLD4QH6EXAZ2uM6mnixyDSstC5GL7bg7AMhi4vger7ynP
12D3KooWLeDQwzDMEURap46wQepSSRZghxKZv4CK5YWFcChHtRKB
12D3KooWM9DMciopJtGLiLVEgkXFs7f6BS3kJGaj6D4rgC5oLSgS
12D3KooWNdiu9QtKrkC7aZfAVxdQbLywbR2QULge3Eni2r63zQaJ
12D3KooWPXXnJYXJ7x9C3LZPkBpS5qEGZDqmUPHNrK9zSS9Cf16Y
12D3KooWPQcL7quAwpzNHtttYPEj3o2LrbXt7vDcYk6K9FABQ7UV
12D3KooWAXk5G1oMJVPTuFGFA7eqo2bKqzCHM2ZpGi1Gd6qC5vuE

Script

```
package main

import (
	"encoding/base64"
	"fmt"
	"os"

	ic "github.com/libp2p/go-libp2p-core/crypto"
	"github.com/libp2p/go-libp2p-core/peer"
)

func main() {
	participantKeys := []string{
		"+UwhWNUYJSmWH7MCk4Zo86hXJ+c9ph4HRrVaqZmW1Xs=",
		"1WHADaxq8Y2pb219ILfaUEGj1ITik9LxO91ee9HdcNw=",
		"2acWHC+/ukvnkBOt6DYNHh/twLdU/x0RGsSUyec4qm0=",
		"6feMjowLf582srMdH+b2BmJpx/niamg9d/+frUXEDcU=",
		"7pQ8yCUpC1kAzKw5pBCwlZptAS0l/Qo590gRgXby18Y=",
		"Cdq18YwdIT21VcOOl3uczUl/W+RGCqi9CgFIf4CLr8g=",
		"CpmU7APXF1cdqJl6Od0orj5dQFKPq/+QfYvg5KjBHtk=",
		"FcjpS5O3FfuMm+J4t4o8Uf4KpI2tjNAeEyMVjJbBVus=",
		"HxX/6MM7jcjqHAyESWHvLVN3KLWjt6GKgRAgTY9CUqc=",
		"TGmJMoGmW2keT4k/KZ8udb8qQDFji7lEbrBjne6yjQo=",
		"Z8wEFP3b27ucfwII3mdNBXglV5T3+oK0D+lp4nuBeU0=",
		"bvM2PKqywPEr1PFzFyl43Tp7i8BV21KAnwwuoa8tvd8=",
		"dx1KtnalRYrh2q+auNeei1ZYKPPw/0Z/YgMrzNKkWjM=",
		"ePSgBL7qaYNU5OYpmqmPm1ayI6BNIt0XhH0v2Yh220g=",
		"fvGMCT2U5wAV9clv2LBpTMdSKHqcUiqI3NuglmWcZkk=",
		"kFIgzLCIMS5j5ZmRnTuOzzyFAZpfvXD+iXbfIyqUPAA=",
		"mmUjmJWmTEfKNaFttMw/4UCQ672k4anRVqAbIlsCBIg=",
		"oNbZQxjWR9sPio0FuldjhfX4FwJm5ubHSOPTIEpnl7Y=",
		"qESgjxFYKQ8+B2QWI9MEP5IojDTkhrlpgUZzQQr+pws=",
		"vm37WOlgoQc2yCgVX2IUj5xCfOgObj5Za7xi9ZRpGq8=",
		"y7Oc3gWYe3z42eTYnYcuM3tCXyhe7KA4Tub77505y6E=",
		"ye2wrecgJB1YehBmqXsW2sdWQPw1kL8f4IPMWqUL52o=",
		"CpmU7APXF1cdqJl6Od0orj5dQFKPq/+QfYvg5KjBHtk=",
	}

	for _, key := range participantKeys {
		pubBytes, err := base64.StdEncoding.DecodeString(key)
		if err != nil {
			fmt.Fprintln(os.Stderr, err)
			continue
		}

		pub, err := ic.UnmarshalEd25519PublicKey(pubBytes)
		if err != nil {
			fmt.Fprintln(os.Stderr, err)
			continue
		}

		id, err := peer.IDFromPublicKey(pub)
		if err != nil {
			fmt.Fprintln(os.Stderr, err)
			continue
		}

		fmt.Println(id)
	}
}
```

-------------------------

Chadass | 2023-06-14 16:10:36 UTC | #2

When a new ceremony is planned (if planned)?

-------------------------

0x3639 | 2023-06-14 20:30:35 UTC | #3

Not sure.  Maybe we can have another one when we upgrade to go-zenon v0.0.6.  I think many operators are working out stability issues and more can participate in the near future.

-------------------------

