Thread: metrics-code-review-for-op-sig-meeting-by-chatgpt
0x3639 | 2024-10-21 14:27:14 UTC | #1

This Go code sets up an HTTP server that exposes metrics for monitoring purposes using Prometheus. Let’s break down the code step by step:

```
package main

import (
	"flag"
	"log"
	"net/http"
	"time"

	"github.com/prometheus/client_golang/prometheus"
	"github.com/prometheus/client_golang/prometheus/collectors"
	"github.com/prometheus/client_golang/prometheus/promhttp"

	"github.com/ignition-pillar/go-zdk/client"
	"github.com/ignition-pillar/go-zdk/zdk"
)

type metrics struct {
	syncCurrentHeight     prometheus.Gauge
	syncTargetHeight      prometheus.Gauge
	networkConnectedPeers    prometheus.Gauge
}

func NewMetrics(reg prometheus.Registerer) *metrics {
	m := &metrics{
		syncCurrentHeight: prometheus.NewGauge(
			prometheus.GaugeOpts{
				Name:       "znnd_sync_current",
				Help:       "Znnd Sync Current.",
			},
		),
		syncTargetHeight: prometheus.NewGauge(
			prometheus.GaugeOpts{
				Name:       "znnd_sync_target",
				Help:       "Znnd Sync Target.",
			},
		),
		networkConnectedPeers: prometheus.NewGauge(
			prometheus.GaugeOpts{
				Name:       "znnd_network_peers",
				Help:       "Znnd Network Peers.",
			},
		),
	}
	reg.MustRegister(m.syncCurrentHeight)
	reg.MustRegister(m.syncTargetHeight)
	reg.MustRegister(m.networkConnectedPeers)
	return m
}

func main() {
	var (
		addr              = flag.String("listen-address", ":8080", "The address to listen on for HTTP requests.")
		rpca              = flag.String("rpc-address", "https://my.hc1node.com:35997", "todo")
	)

	flag.Parse()

	rpc, err := client.NewClient(*rpca)
	if err != nil {
		log.Fatalln(err)
	}
	log.Println("Connected to", *rpca)
	z := zdk.NewZdk(rpc)

	reg := prometheus.NewRegistry()

	m := NewMetrics(reg)
	reg.MustRegister(collectors.NewBuildInfoCollector())

	go func() {
		for {
			// todo error handling
			v, _ := z.Stats.SyncInfo()
			m.syncTargetHeight.Set(float64(v.TargetHeight))
			m.syncCurrentHeight.Set(float64(v.CurrentHeight))
			time.Sleep(10 * time.Second)
		}
	}()
	go func() {
		for {
			v, _ := z.Stats.NetworkInfo()
			m.networkConnectedPeers.Set(float64(v.NumPeers))
			time.Sleep(10 * time.Second)
		}
	}()


	http.Handle("/metrics", promhttp.HandlerFor(
		reg,
		promhttp.HandlerOpts{
			EnableOpenMetrics: true,
			Registry: reg,
		},
	))
	log.Fatal(http.ListenAndServe(*addr, nil))
}
```


### 1. Imports and Dependencies
- `flag`, `log`, `net/http`, `time` – Standard Go libraries for command-line flag parsing, logging, HTTP server setup, and time manipulation.
- `github.com/prometheus/client_golang/prometheus` and `prometheus/promhttp` – Prometheus packages for creating metrics and serving them via HTTP.
- `github.com/ignition-pillar/go-zdk/client` and `go-zdk/zdk` – Custom packages used for interacting with Zenon Network (denoted by `zdk`), which provides RPC (Remote Procedure Call) methods.

### 2. Defining Metrics Structure
```go
type metrics struct {
	syncCurrentHeight     prometheus.Gauge
	syncTargetHeight      prometheus.Gauge
	networkConnectedPeers prometheus.Gauge
}
```
- This structure (`metrics`) defines three Prometheus metrics:
  - `syncCurrentHeight`: Represents the current height of blockchain synchronization.
  - `syncTargetHeight`: Represents the target height of synchronization.
  - `networkConnectedPeers`: Represents the number of peers connected in the network.
- These are `Gauge` types, which means they represent numerical values that can go up or down.

### 3. Creating New Metrics (`NewMetrics` function)
```go
func NewMetrics(reg prometheus.Registerer) *metrics {
	// Define each metric with a name and help string.
	m := &metrics{
		syncCurrentHeight: prometheus.NewGauge(
			prometheus.GaugeOpts{
				Name: "znnd_sync_current",
				Help: "Znnd Sync Current.",
			},
		),
		syncTargetHeight: prometheus.NewGauge(
			prometheus.GaugeOpts{
				Name: "znnd_sync_target",
				Help: "Znnd Sync Target.",
			},
		),
		networkConnectedPeers: prometheus.NewGauge(
			prometheus.GaugeOpts{
				Name: "znnd_network_peers",
				Help: "Znnd Network Peers.",
			},
		),
	}
	// Register each metric with Prometheus.
	reg.MustRegister(m.syncCurrentHeight)
	reg.MustRegister(m.syncTargetHeight)
	reg.MustRegister(m.networkConnectedPeers)
	return m
}
```
- The `NewMetrics` function takes a `prometheus.Registerer` as an argument to register the metrics with Prometheus.
- It initializes each metric with appropriate labels and registers them to make them available for monitoring.

### 4. Main Function
#### Command Line Arguments
```go
var (
	addr = flag.String("listen-address", ":8080", "The address to listen on for HTTP requests.")
	rpca = flag.String("rpc-address", "https://my.hc1node.com:35997", "todo")
)
```
- The `flag` package is used to define command-line flags:
  - `listen-address`: The address where the HTTP server will be listening for incoming requests.
  - `rpc-address`: The RPC endpoint to connect to the Zenon Network node.

#### Client Setup
```go
rpc, err := client.NewClient(*rpca)
if err != nil {
	log.Fatalln(err)
}
log.Println("Connected to", *rpca)
z := zdk.NewZdk(rpc)
```
- It establishes a connection with the Zenon RPC node using the address provided.
- A `NewClient` function from the `client` package is used to create an RPC client.
- If an error occurs during connection, it will log the error and terminate the program (`log.Fatalln`).
- The RPC client is then wrapped by `zdk.NewZdk` to use the higher-level Zenon API.

#### Prometheus Registry and Metric Registration
```go
reg := prometheus.NewRegistry()
m := NewMetrics(reg)
reg.MustRegister(collectors.NewBuildInfoCollector())
```
- A custom Prometheus registry (`reg`) is created.
- The `NewMetrics` function is called to register the custom metrics.
- The `NewBuildInfoCollector()` is also registered, which provides metadata such as Go version and build details.

### 5. Metrics Collection Goroutines
#### Sync Information Collector
```go
go func() {
	for {
		// todo error handling
		v, _ := z.Stats.SyncInfo()
		m.syncTargetHeight.Set(float64(v.TargetHeight))
		m.syncCurrentHeight.Set(float64(v.CurrentHeight))
		time.Sleep(10 * time.Second)
	}
}()
```
- A goroutine (`go func() { ... }()`) is used to collect synchronization information from the Zenon node every 10 seconds.
- `z.Stats.SyncInfo()` retrieves the sync information (`TargetHeight` and `CurrentHeight`) and updates the corresponding metrics.
- The `time.Sleep(10 * time.Second)` ensures the metrics are updated at regular intervals.
- Note that error handling is not implemented here (`// todo error handling`).

#### Network Info Collector
```go
go func() {
	for {
		v, _ := z.Stats.NetworkInfo()
		m.networkConnectedPeers.Set(float64(v.NumPeers))
		time.Sleep(10 * time.Second)
	}
}()
```
- Another goroutine is used to collect the network information, specifically the number of peers (`NumPeers`).
- This metric is updated every 10 seconds.

### 6. HTTP Metrics Endpoint
```go
http.Handle("/metrics", promhttp.HandlerFor(
	reg,
	promhttp.HandlerOpts{
		EnableOpenMetrics: true,
		Registry:          reg,
	},
))
log.Fatal(http.ListenAndServe(*addr, nil))
```
- The HTTP server is set up to handle `/metrics` endpoint requests.
- `promhttp.HandlerFor(reg, ...)` is used to serve the metrics collected by the custom registry (`reg`) in the OpenMetrics format.
- The server listens on the address provided by the `addr` flag (e.g., `:8080`).
- If there is an issue with starting the server, `log.Fatal` will log the error and stop the program.

### Summary
This code provides a Prometheus metrics exporter for monitoring the state of a Zenon node by collecting:
- **Sync Target Height**: The target block height for synchronization.
- **Sync Current Height**: The current block height of synchronization.
- **Connected Peers**: Number of peers connected to the network.

Two separate goroutines are used to periodically update these metrics from the Zenon node, and an HTTP server serves these metrics at `/metrics`, which can be scraped by Prometheus.

-------------------------

0x3639 | 2024-10-21 14:31:43 UTC | #2

@georgezgeorgez Should we track the rate at which blocks are produced in case one hangs and we need to trouble shoot it?

-------------------------

georgezgeorgez | 2024-10-21 16:31:24 UTC | #3

We can derive that metric by changes in targetHeight right?

-------------------------

0x3639 | 2024-10-21 16:48:42 UTC | #4

Right.  If this runs every 10 seconds it will get all of them and we can calculate the time.  For some reason I was thinking we could have 2 momentums in within 10 seconds (and miss one), but I assume that is impossible / unlikely.

-------------------------

georgezgeorgez | 2024-10-21 16:50:03 UTC | #5

Every 5 minutes, 5 * 60 = 300 seconds, 30 pillars are elected and assigned momentums to produce every 300/30 = 10 seconds.

-------------------------

