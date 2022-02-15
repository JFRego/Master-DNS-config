#Master DNS server redhat based


- start from installing bind;

        yum install bind
        
- then open /etc/named.conf and set the following lines to any;

        options {
                listen-on port 53 { any; };
                listen-on-v6 port 53 { any; };
                ...
                allow-query     { any; };
                
- and add to the bottom the following block, changing localhost to your server domain and seting the path of your forward zone file;

        zone "enta.pt" {
        type master;
        file "/var/named/db.local";
        };
               
- now edit your forward zone file;

        ;
        ; BIND data file for local loopback interface
        ;
        $TTL    604800
        @       IN      SOA     enta.pt. root.enta.pt. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
        ;
        @       IN      NS      enta.pt.
        @       IN      A       172.31.2.196
        @       IN      A       172.30.2.196
        www     IN      A       172.31.96.11
        www     IN      A       172.30.96.11
        central IN      A       172.31.128.11
        central IN      A       172.30.128.11
        wazuh   IN      A       172.31.128.12
        wazuh   IN      A       172.30.128.12
        sales   IN      A       172.31.128.13
        sales   IN      A       172.30.128.13
        marketing       IN      A       172.31.128.14
        marketing       IN      A       172.30.128.14
        control IN      A       172.31.2.196
        control IN      A       172.30.2.196       
        
- after that restart named.service and check status;

        systemctl restart named.service 
        systemctl status named.service   
        
- and thats its;        
        
        
        

