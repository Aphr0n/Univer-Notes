	# 1 Базова конфігурація
## Hostname
Для конфігурації hostname треба використовувати команду
```
hostname <ім'я хосту>
```

## Пароль для входу в привілейований режим(Nešifrované heslo do privilegovaného režimu)
Для конфігурації паролю для входу в привілейований режим треба використовувати команду 
```
enable password <пароль>
```

## Пароль для доступу через консоль(Heslo do konzoly)
Для налаштування даного паролю треба використовувати наступні команди:
```
line console 0
password <пароль>
login
```

# DHCP
1. Спочатку нам треба виключити всі пристрої у яких є статична ip адреса(зазвичай підписана на топології), щоб не було конфліктів ip адрес за допомогою:
```
ip dhcp excluded-address <адреса>
```
2. Потім треба створити пул для мережі використовуючи:
```
ip dhcp pool <Назва пулу>
```
3. Задати шлюз(роутер(той для якого й просять налаштувати dhcp)) за замовчуванням командою:
```
default-router <адреса>
```
4. Увімкнути роздачу адрес командою:
```
network <адреса> <маска>
```

# SSH
1. Задати ім'я домену командою:
```cisco
ip domain-name <ім'я>
```
2. Створити користувача з зашифрованим паролем
```cisco
username <ім'я користувача> secret <пароль>
```
3. Налаштувати віртуальний інтерфейс VLAN1
```cisco
interface vlan 1
	ip address <адреса свічу> <маска>
	no shutdown
```
4. Згенерувати RSA ключ(мінімум 1024 для SSH v2):
```
crypto key generate rsa 
1024
```
5. Увімкнути SSH v2:
```
ip ssh version 2
```
6. Налаштувати VTY лінії:
```cisco
line vty 0 15 
	login local 
	transport input ssh
```
7. Зберегти зміни:
```cisco
end 
write memory
```

# VLAN
## Switch 1
1. Створити VLAN:
```
vlan <номер>
name VLAN<номер>
vlan <номер2>
name VLAN<номер2>
```
2. Виставляємо acces port-и для комп'ютерів
```
interface FastEthernet<порт>
	switchport mode access
	switchport access vlan <номер відповідного vlan>
```
3. Налаштування trunk-порту
```
interface FasEthernet<порт>
	switchport mode trunk
	switchport trunk allowed vlan <номер 1-го vlan>,<номер 2-го vlan>
```
4. Зберігаємо зміни
```
end
write memory
```
## Router 1
1. Піднімаємо інтерфейс
```
interface GigabitEthernet<порт>
	no shutdown
```
2. Піднімаємо інтерфейси для кожного vlan
```
interface GigabitEthernet<порт>.<останній октет адреси vlan>
	encapsulation dot1Q <номер vlan>
	ip address <ip адреса vlan>.<остання частина адреси роутеру(біля роутеру написано .число)> <маска>
	no shutdown
```
3. Зберегти зміни
```
end
write memory
```

# Комп'ютери
1. Налаштувати IP 
2. Налаштувати маску
3. Налаштувати шлюз

# HSRP
## Router 1
```
interface GigabitEthernet <порт>
ip address <адреса роутеру> <маска>
standby ip <резервна адреса(брати з умови)>
no shutdown
```

## Router 2
```
interface GigabitEthernet <порт>
ip address <адреса роутеру> <маска>
standby ip <резервна адреса(брати з умови)>
no shutdown
```

# Static routing
## next-hop ip
1. вирахувати next-hop ip
	1. знайти розмір блоку за формулою: $2^{(32-маска)}$
	2. знайти всі адреси починаючи з адреси яка задана в умові
	3. прибрати з списку адресу мережі(з умови), адресу роутеру, broadcast-адресу
2. Задати адресу за командою
```
ip route 0.0.0.0 0.0.0.0 <next-hop ip>
```

## Вихідний інтерфейс
```
ip route 0.0.0.0 0.0.0.0 <порт>
```


# Port-Security
```cisco
enable
configure terminal

interface range FastEthernet0/1 - 24
 switchport mode access
 switchport port-security -- увімкнути port security
 switchport port-security maximum 2 -- встановити ліміт на 2
 switchport port-security violation restrict -- встановити обмеження
exit

end
write memory
```