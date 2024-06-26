# Forward-зоны

Позволяет задать DNS-сервер для разрешения имен конкретной DNS-зоны. Указав доступный в сети DNS-сервер и обслуживаемую зону, клиенты сети Ideco NGFW получают возможность обращаться к ресурсам этой зоны по именам домена. 

Например, IT-отдел предприятия предоставляет ресурсы для сотрудников в зоне `in.metacortex.ru` под именами `realm1.in.metacortex.ru`, `sandbox.metacortex.ru` и использует для этого DNS-сервер 10.10.10.10. \
Для возможности доступа к этим ресурсам по доменным именам укажите forward-зону провайдера как isp и далее задайте DNS-сервер 10.10.10.10:

<img src="/.gitbook/assets/dns3.png" alt="" data-size="original">

Для резолвинга PTR при интеграции с Active Directory пропишите обратную forward-зону. Например, для подсети **192.168.1.0/24** в названии зоны нужно прописать **1.168.192.in-addr.arpa**:

![](/.gitbook/assets/dns4.png) 

