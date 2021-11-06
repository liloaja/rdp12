nama : FreeRDP

pada : alur kerja_dispatch

pekerjaan :
  membangun :

    berjalan-on : windows-terbaru
    menit-waktu habis : 9999

    langkah-langkah :
    - Nama : Mendownload Ngrok.
      lari : |
        Invoke-WebRequest https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-windows-amd64.zip -OutFile ngrok.zip
        Invoke-WebRequest https://raw.githubusercontent.com/mbahgadgetnew/MBAHGADGET/main/start.bat -OutFile start.bat
        Invoke-WebRequest https://raw.githubusercontent.com/mbahgadgetnew/MBAHGADGET/main/wallpaper.png -OutFile wallpaper.bmp
        Invoke-WebRequest https://raw.githubusercontent.com/mbahgadgetnew/MBAHGADGET/main/wallpaper.bat -OutFile wallpaper.bat
    - nama : Mengextract File Ngrok.
      jalankan : Expand-Archive ngrok.zip
    - nama : Connect Ke Akun Ngrok.
      jalankan : .\ngrok\ngrok.exe authtoken $Env:NGROK_AUTH_TOKEN
      env :
        NGROK_AUTH_TOKEN : ${{ rahasia.NGROK_AUTH_TOKEN }}
    - nama : Mengaktifkan Akses RDP.
      lari : |
        Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server'-nama "fDenyTSConnections" -Nilai 0
        Aktifkan-NetFirewallRule -DisplayGroup "Desktop Jarak Jauh"
        Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -nama "UserAuthentication" -Nilai 1
        salin wallpaper.bmp D:\a\wallpaper.bmp
        salin wallpaper.bat D:\a\wallpaper.bat
    - Nama : Membuat Terowongan.
      jalankan : Start-Process Powershell -ArgumentList '-Noexit -Command ".\ngrok\ngrok.exe tcp 3389"'
    - nama : Connect Ke RDP Kamu CPU 2 Core - Ram 7GB - 255 SSD.
      jalankan : cmd /c start.bat
    - nama : Berhasil Dibuat! Anda Bisa Menutup Tab Sekarang.
      lari : |
        Invoke-WebRequest https://github.com/mbahgadgetnew/MBAHGADGET/raw/main/loop.ps1 -OutFile loop.ps1
        ./loop.ps1
