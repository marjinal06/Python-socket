import socket  # Ağ bağlantısı için gereken kütüphane



host = '127.0.0.1'  # Bağlanılacak sunucunun IP adresi
port = 50002        # Sunucunun dinlediği port



client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
# TCP soketi oluşturuluyor



client_socket.connect((host, port))
# Belirtilen IP ve port'a bağlan

message = input(">>  ")  # Kullanıcıdan komut al


while message.lower().strip() != "quit":
    # Kullanıcı 'quit' yazana kadar döngü devam etsin

    if message != "":
        client_socket.send(message.encode())  # Komutu sunucuya gönder
        data = client_socket.recv(1024).decode()  # Sunucudan cevabı al
        print("Response from Server: " + str(data))  # Ekrana yaz
       	message = input(">>  ")  # Yeni komut al
       	
       	client_socket.close()  # Bağlantıyı kapat

	
	
	

