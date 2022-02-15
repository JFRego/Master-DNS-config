#Master DNS server debian based


- start from installing bind9;

        apt install bind9
        
- then open /etc/bind/named.conf.options and uncomment the following block;

        forwarders {
                0.0.0.0;
        };
        
- now open /etc/bind/named.conf.default-zones, copy the following block and paste it inside /etc/bind/named.conf.local;

        zone "localhost" {
        type master;
        file "/etc/bind/db.local";
        };
        
- change localhost to your server domain and you might change /etc/bind/db.local to the path of your forward zone configuration file;

        zone "inova.pt" {
        type master;
        file "/etc/bind/db.local";
        };
        
- after that edit your forward zone file;

        ;
        ; BIND data file for local loopback interface
        ;
        $TTL    604800
        @       IN      SOA     inova.pt. root.inova.pt. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
        ;
        @       IN      NS      inova.pt.
        @       IN      A       172.31.9.208
        @       IN      A       172.29.9.208
        www     IN      A       172.31.96.11
        www     IN      A       172.29.96.11
        central IN      A       172.31.128.11
        central IN      A       172.29.128.11
        wazuh   IN      A       172.31.128.12
        wazuh   IN      A       172.29.128.12
        sales   IN      A       172.31.128.13
        sales   IN      A       172.29.128.13
        marketing       IN      A       172.31.128.14
        marketing       IN      A       172.29.128.14
        control IN      A       172.31.9.208
        control IN      A       172.29.9.208
        
- then restart bind9 and check status;

        systemctl restart bind9.service 
        systemctl status bind9.service
        
- and its done;


