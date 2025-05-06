							server.py
			

import socket      # Ağ bağlantısı kurmak için gerekli kütüphane
import subprocess  # Komut satırı komutlarını çalıştırmak için


host = '127.0.0.1'  # Sunucunun IP adresi (localhost = sadece bu bilgisayar)
port = 50002        # Dinlenecek port numarası


server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
# TCP bağlantısı kurmak için soket oluşturuluyor (IPv4 + TCP)


server_socket.bind((host, port))  # Sunucuyu belirtilen IP ve port'a bağla
server_socket.listen()            # Bağlantıları dinlemeye başla


conn, addr = server_socket.accept()
# İlk gelen bağlantıyı kabul et. conn: bağlantı kanalı, addr: bağlanan IP/port
print("Connected from:", addr)  # Kimin bağlandığını yazdır


while True:
    data = conn.recv(1024).decode()  # İstemciden 1024 baytlık veri al, çöz
    if not data:                     # Hiç veri yoksa (bağlantı kapandıysa)
        break                        # Döngüyü kır, sunucuyu kapat

    print("Received command:", data)  # İstemciden gelen komutu yazdır


    result = subprocess.run(data, stdout=subprocess.PIPE, stderr=subprocess.PIPE, shell=True)
    # Gelen komutu işletim sisteminde çalıştır.
    # stdout: komutun çıktısı, stderr: hata varsa

    if result.stdout:  # Çıktı varsa onu gönder
        response_data = result.stdout
    elif result.stderr:  # Hata varsa onu gönder
        response_data = result.stderr
    else:  # Ne çıktı ne hata varsa...
        response_data = b"Command executed, no output."
        
        
    conn.send(response_data)  # Komut sonucunu istemciye gönder
    conn.close()  # Bağlantıyı kapat (istemciyle iş bitince)

