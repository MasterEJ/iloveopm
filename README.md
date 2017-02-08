// Original - http://linge-ma.ws/update-listeners-track-on-a-website-using-icecast-jsonp-and-jquery/
// Modified by Fuzzy Mannerz to include fallback autoDJ stream.
function radioTitle() {
 
// This is the URL of the json.xml file located on your radio server.
    var url = '112.211.168.127:8000/json.xsl';
 
$.ajax({
   type: 'GET',
    url: url,
    async: true,
    jsonpCallback: 'parseMusic',
    contentType: "application/json",
    dataType: 'jsonp',
    success: function(json) {
        // These are the elements we're updating that will hold the track title.
        // Change "/LiveStreamMountPoint" and "/FallbackStreamMountPoint" accordingly.
$('#track-title').text(json['/stream']['title']);
if ($('#track-title').is(':empty')){
$('#track-title').text(json['/stream']['title']);
}    
    },
    error: function(e) {
       console.log(e.message);
    }
});
 
}
 
$(document).ready(function(){
 
  setTimeout(function(){radioTitle();}, 2000);
  setInterval(function(){radioTitle();}, 15000); // We're going to update our html elements / player every 15 seconds
 
});
