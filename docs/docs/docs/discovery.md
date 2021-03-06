# TPLinkDiscovery Class
<small>Namespace: TPLinkSmartDevices</small><br/><br/>
handles discovery of new smart devices and connection of factory new devices to a network

## Properties

### `DiscoveredDevices`
: Returns a list of [`TPLinkSmartDevice`](devices/device.md)'s from the latest call of [`.Discover()`](discovery.md#discover). This property is read-only.
``` csharp
public List<TPLinkSmartDevice> DiscoveredDevices { get; private set; }
```

## Methods

### `Discover(int, int)`
: Discovers smart devices within the network of the host via UDP broadcast. Returns a list of [`TPLinkSmartDevice`](devices/device.md)'s.
  ``` csharp
  public async Task<List<TPLinkSmartDevice>> Discover(int port=9999, int timeout=5000)
  ```

    __Parameters__
    : * `#!csharp int port`: Listen to broadcast responses on this port, defaults to `9999`
      * `#!csharp int timeout`: Timespan after which the discovery finishes, defaults to `5000`(5 seconds)

!!! tip "Method is awaitable" 

### `Associate(string, string, int)`
: Makes smart device connect to specified network credentials
  ``` csharp
  public async Task Associate(string ssid, string password, int type = 3)
  ```

    __Parameters__
    : * `#!csharp string ssid`: _Service Set Identifier_ (name) of network to connect to
      * `#!csharp string password`: password of network to connect to
      * `#!csharp int type`: network protection level, defaults to `3` indicating WPA2

!!! caution 
    Host who runs the application needs to be connected to the open configuration network! (TP-Link_Smart Plug_XXXX or similar)

!!! tip "Method is awaitable" 

## Events

### `DeviceFound`
: Triggers when smart device is found during discovery process, granting access to all system properties of that device via the event args 
  ``` csharp
  public event EventHandler<DeviceFoundEventArgs> DeviceFound;
  ```

    __EventArgs__
    : * `#!csharp DeviceFoundEventArgs e`

    __Example__
    : 
    ``` csharp
    new TPLinkDiscovery().DeviceFound += (s, e) {
        ...
        Console.WriteLine($"Device found: {e.Device.Alias}");
        ...
    };
    ``` 