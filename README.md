# T100 API V1

## API calls
```
/api/hsfb/v1/start
/api/hsfb/v1/stop
/api/hsfb/v1/toggle
/status
/deleteVideos
```

---------------------------------------------------------

## C# Send Command

Import
```c#
using System.Net;
```

Send Function
```c#
string t100ipAddress = "192.168.3.1";
string apiCall = "/api/hsfb/v1/toggle";

using (WebClient wc = new WebClient())
{
  string url = "http://" + t100ipAddress + ":1612" + apiCall;
  var json = wc.DownloadString(url);
}
```

## Javascript Send Command
```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.2/jquery.min.js"></script>

<script>

  var t100ipAddress = "192.168.3.1";
  var apiCall = "/api/hsfb/v1/toggle";

  $.ajax({
    url: "http://" + t100ipAddress + ":1612" + apiCall,
    context: document.body
  }).done(function() {
    //Your Code here
  });

</script>
```

---------------------------------------------------------


## Javascript Discover T100 (Node JS)

*This Code will return the IP Address of any T100 on the same local network*
```javascript
var dgram = require('dgram');
var udp = dgram.createSocket('udp4');
udp.bind(1612, function() {
  udp.addMembership('224.0.0.1');
});
udp.on('message', function(msg, rinfo) {
  try {
    var t100ipAddress = JSON.parse(msg).server;
    console.log(t100ipAddress);
    //Your Code here

  } catch (error) {
    err = error;
    return console.log("Bad Multicast Packet, skipping");
  }
});
```

