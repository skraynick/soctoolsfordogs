Steps Prep:

1. Create folder on linux for working. includes zeeklogs, suricatalogs, and tcpdump
2. Run suricata ----- sudo suricata -r <file>  -c /etc/suricata/suricata.yaml
3. run zeek logs ---- zeek -r <file>
4. run tcp dump. ---- tcpdump -r <inputfile> -w <output> -C <file size (in mb)> -- better strategy then by filter. Try to break up in larger, but usable chungs. Largest should be 200mb. FILE > MERGE to merge pcaps from within wireshark.
5.

###  steps of analysis.
1.  Find critical needed info. 
	1. Ip of host -- look in zeek logs and suricata. Highest connections. 
	2. Ip of baddie
	3. Host names most frequent hosts 
zeek-cut -d -f http.log uri | sort | uniq -c | sort -rn
	4. Count connections
zeek-cut -d -f conn.log id.orig_h id.orig_p id.resp_h id.resp_p | sort | uniq -c | sort -rn

	5. 
1. Look for scans (recon) - xmas, port, sweeps 
[[Recognizing scans and attacks in wireshark.]]
3.  Check files - check zeek command inclass notes.
	Wireshark, file - extract files
 4. Go through logs to find anomolies. FTP. EMAIL details, logins. 
		
	
	 

	

