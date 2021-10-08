# Scanner   para acessar o video https://www.youtube.com/watch?v=YU8YCYMC4rc
trabalho python  de port scanning
# 1°TDCF cybersecurity
# nome dos integrantes Ariel Levi RM87502 // Rafael Del Padre 86851
import socket
from IPy import IP
# #def Scan(target) = definir os  alvos Converted_ip = check_ip (ver o IP ou URL),1,1000 = ver portas de 1-1000
with open('ScannerNmap.txt','w')as Scanner:
    def scan(target):
        converted_ip = check_ip(target)
        print('\n' + '[-_0 Scanning Target] ' + str(target))
        for port in range(1,1000):
            scan_port(converted_ip, port)
            
#Def check_ip Ao colocar IP se for o correto ele retorna IP. Caso contrário ele dará erro
   def check_ip(ip):
        try:
            IP(ip)
            return(ip)
        except ValueError:
            return socket.gethostbyname(ip)

    def get_banner(s):
        return s.recv(1024)
# Socket usado para ter resposta dos ips, Settimeout 0.2 para que não demore pra ter a resposta, Sock.connect usado para conectar o IP e a porta
    def scan_port(ipaddress, port):
        try:
            sock = socket.socket()
            sock.settimeout(0.2)
            sock.connect((ipaddress, port))
            try:
                banner = get_banner(sock)
                print('[+] Open Port ' + str(port) + ' : ' + str(banner.decode().strip('\n')))
            except:
                print('[+] Open Port ' + str(port))
        except:
            pass
# esta ultima parte ira o alvo definitivo ou IP ou web 
    targets = input('[+] Enter target/s to Scan(split multiple targets with , ): ')
    if ',' in targets:
        for ip_add in targets.split(','):
            scan(ip_add.strip(' '))
    else:
        scan(targets)
    Scanner.write('ScannerNmap.txt')
