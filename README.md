**Recursive DNS Resolver**   
An implementation of a recursive DNS resolver in Python.    
The resolver handles various DNS record types (A, CNAME, MX, TXT, NS) and implements proper DNS recursion with caching.    

**Overview**  
The recursive DNS resolver is capable of:  
  - Resolving various DNS record types (A, CNAME, MX, TXT, NS)  
  - Serving an auhoritative domain   
  - Recursive resolution through the DNS hierarchy  
  - Caching DNS responses with proper TTL handling    
  - Implementing bailiwick checking for security    
  - Proper handling of CNAME record chains    

**Requirements**      
- Python v3    
- dnslib package     

Install dnslib with,      
pip3 install dnslib    

**Project Structure**    

recursive_dns: The main DNS resolver implementation    
run: The test harness for validating the resolver by sending requests to the server   
configs/: Various test configurations     

**Running the DNS Resolver**    
The DNS resolver can be run directly with:     
./recursive_dns [root_ip] [zone_file] [--port PORT]     

or by using tests against a reference implementation by running:     
./run configs/1-local-a.conf     

Different configurations can test different aspects of the resolver:

- Basic DNS resolution  
- Caching behavior  
- Handling of different record types  
- Edge cases and error conditions  

**Configuration Files**    
The config files in the configs/ directory specify test parameters, including:     

- Root server IP address   
- Reference server to compare against   
- Number of test clients and requests   
- Types of queries to test   
- Test duration   

Example config format:  
json{  
  "root": "root.server.ip",   
  "reference": "reference.server.ip:port",   
  "simulator": {   
    "lifetime": 10,   
    "clients": 1,   
    "requests": 5,   
    "level": 1,      
    "zone": "path/to/zone/file",    
    "tags": ["type-A"]    
  }     
}     

Implementation Details -      
The resolver uses the following approach:     

- Parse incoming DNS requests     
- Check the local cache for a response     
- If not found, recursively query the DNS hierarchy starting from the root     
- Apply proper bailiwick checking for security     
- Cache responses for future queries     
- Assemble and return the DNS response     
