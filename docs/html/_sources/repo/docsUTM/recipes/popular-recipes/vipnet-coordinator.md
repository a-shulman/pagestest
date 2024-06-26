# Рекомендации по настройке NGFW для работы совместно с ViPNet-координатором

ViPNet-координатор используется для шифрования трафика подсети, в которой он является шлюзом. Шифрование позволяет обеспечить конфиденциальность информации, передаваемой по незащищенному каналу.

Схема совместной работы Ideco NGFW с ViPNet-координатором:

![](/.gitbook/assets/vipnet-coordinator1.png)

## Настройка Ideco NGFW и ViPNet-координатора

Для корректной работы Координатора совместно с NGFW выполните действия:

1\. Настройте проброс порта udp 55777 на IP адрес координатора в разделе **Файрвол -> DNAT (перенаправление портов)**. \
2\. Переведите Координатор в режим **Со статической трансляцией адресов**.

Работа Координатора в режиме динамической трансляции адресов совместно с Ideco NGFW не гарантируется.

Более подробно о настройке ViPNet можно узнать в [статье](https://infotecs.ru/press-center/publications/printsipy-marshrutizatsii-i-preobrazovaniya-ip-trafika-v-vpn-seti-sozdannoy-s-ispolzovaniem-tekhnolo/).
