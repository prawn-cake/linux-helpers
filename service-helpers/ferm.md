Easy port forwarding
====================

Implement *tcp/udp* proxy (also called port-mapping, port-forwarding) with 
iptables/ferm.


Solution
--------
We consider that *ferm* is installed.

Define a ferm function to reuse it. 

    def &FORWARD_PORT_LAN($proto, $sport, $daddr, $dport) = {
        table filter chain FORWARD interface $DEV_LAN outerface $DEV_LAN daddr $daddr proto $proto dport $dport ACCEPT;
        table nat chain PREROUTING interface $DEV_LAN proto $proto dport $sport DNAT to "$daddr:$dport";
    }
    
    # Example
    &FORWARD_PORT_LAN((tcp udp), 8080, 192.168.1.207, 5959);
    
    
**NOTE:** For sure you need to define `$DEV_LAN` variable.

**NOTE:** Better to store it in separate configuration files and include it 
with `@include 'conf.d/';` in the *ferm.conf*