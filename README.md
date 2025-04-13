# Tracker
GPS Tracker via Browser
<!DOCTYPE html>
<html>
<head>
  <title>GPS Tracker via Link</title>
  <style>
    body { font-family: Arial, sans-serif; text-align: center; margin-top: 50px; }
    #location { margin-top: 20px; }
    a { color: blue; }
  </style>
</head>
<body>
  <h1>GPS Tracker</h1>
  <p>Klik tombol di bawah untuk mendapatkan lokasi Anda:</p>
  <button onclick="getLocation()">Dapatkan Lokasi</button>

  <div id="location"></div>

  <script>
    function getLocation() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(showPosition, showError);
      } else {
        document.getElementById("location").innerHTML = "Geolocation tidak didukung browser ini.";
      }
    }

    function showPosition(position) {
      const lat = position.coords.latitude;
      const lon = position.coords.longitude;
      const link = `https://www.google.com/maps?q=${lat},${lon}`;
      document.getElementById("location").innerHTML =
        `<p>Latitude: ${lat}<br>Longitude: ${lon}</p>
         <p><a href="${link}" target="_blank">Lihat di Google Maps</a></p>`;
    }

    function showError(error) {
      let message = "";
      switch (error.code) {
        case error.PERMISSION_DENIED:
          message = "Izin lokasi ditolak.";
          break;
        case error.POSITION_UNAVAILABLE:
          message = "Informasi lokasi tidak tersedia.";
          break;
        case error.TIMEOUT:
          message = "Permintaan lokasi habis waktu.";
          break;
        case error.UNKNOWN_ERROR:
          message = "Terjadi kesalahan yang tidak diketahui.";
          break;
      }
      document.getElementById("location").innerHTML = `<p>${message}</p>`;
    }
  </script>
</body>
</html>
