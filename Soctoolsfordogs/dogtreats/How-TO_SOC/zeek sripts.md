## Port scan
```zeek
@load policy/frameworks/conn/protocols/tcp.zeek

# Define the threshold for port scan detection.
redef Scan::max_ports = 10;

# Track the number of connection attempts for each source IP and destination IP.
global port_counter: table[addr, addr] of count = {};

event connection_state_changed(c: connection, old_state: state, new_state: state)
{
    if (new_state == S3 && old_state == S2)
    {
        # Increment the port scan counter.
        port_counter[c$id$orig_h, c$id$resp_h]++;
        
        if (port_counter[c$id$orig_h, c$id$resp_h] >= Scan::max_ports)
        {
            print fmt("%s may be conducting a port scan against %s",
                      c$id$orig_h, c$id$resp_h);
        }
    }
```

To Run

```
zeek -r /path/to/your/pcap/file.pcap port_scan_detection.zeek
```


## Arp scan
```zeek
@load protocols/arp

# Define the threshold for ARP scan detection.
redef Scan::arp_max_requests = 10;

event arp_request(r: arp_request)
{
    local requestor = r$sender_p$addr;

    # Track the number of ARP requests from the same sender.
    Scan::arp_request_counter[requestor]++;
    
    if (Scan::arp_request_counter[requestor] >= Scan::arp_max_requests)
    {
        print fmt("%s may be conducting an ARP scan.", requestor);
    }
}
```

```
zeek -r /path/to/your/pcap/file.pcap arp_scan_detection.zeek
```

## Brute script
```zeek
@load base/protocols/ssh
@load base/protocols/ftp
@load base/protocols/ftp/detect
@load base/protocols/ftp/consts

# Define threshold values for detecting brute force attempts.
redef Scan::login_attempts_threshold = 5;
redef Scan::interval_threshold = 300 secs;

# Track login attempts using a dictionary.
global login_attempts: table[addr, string] of interval &default = 0;

event ssh_login_attempt(c: connection, username: string, success: bool)
{
    if (!success)
    {
        local src_ip = c$id$orig_h;
        login_attempts[src_ip, "ssh"] += 1;
        
        if (login_attempts[src_ip, "ssh"] >= Scan::login_attempts_threshold)
        {
            if (login_attempts[src_ip, "ssh"] == Scan::login_attempts_threshold)
            {
                print fmt("Potential SSH brute force attack from %s", src_ip);
            }
            else if (login_attempts[src_ip, "ssh"] > Scan::login_attempts_threshold)
            {
                print fmt("Continued SSH brute force attack from %s", src_ip);
            }
        }
    }
}

event ftp_login_attempt(c: connection, user: string, password: string)
{
    local src_ip = c$id$orig_h;
    login_attempts[src_ip, "ftp"] += 1;

    if (login_attempts[src_ip, "ftp"] >= Scan::login_attempts_threshold)
    {
        if (login_attempts[src_ip, "ftp"] == Scan::login_attempts_threshold)
        {
            print fmt("Potential FTP brute force attack from %s", src_ip);
        }
        else if (login_attempts[src_ip, "ftp"] > Scan::login_attempts_threshold)
        {
            print fmt("Continued FTP brute force attack from %s", src_ip);
        }
    }
}
```

Run
```bash
zeek -r /path/to/your/pcap/file.pcap brute_force_detection.zeek
```