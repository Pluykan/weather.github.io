<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="style.css">
  <link rel='stylesheet prefetch' href='https://code.jquery.com/ui/1.11.4/themes/smoothness/jquery-ui.css'>
  <link rel='stylesheet prefetch' href='https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css'>
</head>
<body>
    <p class="text-center data-item" id="city-text"></p>
    <h3 class="text-center data-item" id="weather-text"></h3>
    <script src='https://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.3/jquery.min.js'></script>
    <script src='https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js'></script>
    <script src='https://code.jquery.com/ui/1.11.4/jquery-ui.js'></script>
    <script>
        
        function dataHandler(data) {
            if (data.weather) {
              $("#weather-text").html(data.weather[0].description);
            }
        }
        function getWeather(locdata) {
          console.log("getWeather has been called.")
          var lat = locdata.latitude;
          var lon = locdata.longitude;
          
          var apiURI = "https://api.openweathermap.org/data/2.5/weather?lat=" + lat + "&lon=" + lon + "&appid=5b58aee62c41eb64fcab16edce2e5cc1";
          if (locdata){
            $("#city-text").html(locdata.city );
          }
          return $.ajax({
            url: apiURI,
            dataType: "jsonp",
            type: "GET",
            async: "true",
          }).done(dataHandler);
        }
      
        function getLocation() {
          return $.ajax({
            url: "https://ipapi.co/jsonp/",
            dataType: "jsonp",
            type: "GET",
            async: "true",
          });
        }
        var updateInterval = setInterval(getLocation().done(getWeather), 300000);
        </script>
</body>
</html>