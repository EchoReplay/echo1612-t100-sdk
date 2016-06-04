# t100sdk

API calls

*Requires T100 Update and Custom iOS App*

/api/rightview/baseball/v1/start
/api/rightview/baseball/v1/stop
/api/rightview/baseball/v1/clips

*API for current iOS App*

/api/hsfb/v1/start
/api/hsfb/v1/stop
/api/hsfb/v1/toggle
/status
/deleteVideos

---------------------------------------------------------


C# Send Command
*This Code will perform one of the API calls*

using System.Net;

string t100ipAddress = "192.168.3.1";
string apiCall = "/api/rightview/baseball/v1/start";

using (WebClient wc = new WebClient())
{
  string url = "http://" + t100ipAddress + ":1612" + apiCall;
  var json = wc.DownloadString(url);
}

---------------------------------------------------------


Javascript Discover T100 (Node JS)
*This Code will return the IP Address of any T100 on the same local network*

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

---------------------------------------------------------


Javascript Send Command (jQuery)
*This Code will perform one of the API calls*

<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.2/jquery.min.js"></script>

<script>

  var t100ipAddress = "192.168.3.1";
  var apiCall = "/api/rightview/baseball/v1/start";

  $.ajax({
    url: "http://" + t100ipAddress + ":1612" + apiCall,
    context: document.body
  }).done(function() {
    //Your Code here
  });

</script>
