---
tags:
  - Asp_Net_Core
---

# Kestrel and Other Servers
---

![[10.png]]

![[11.png]]

![[12.png]]

## Reverse Proxy Server

- **Purpose:** Acts as an intermediary between clients and backend servers. **Functions:**
- **Functions:**
	- **Load balancing** (Distributes traffic across multiple servers to improve response times and prevent server overload)
		
	- **Security** (Hiding backend servers)
		-  Authentication
			
		- SSL termination
			
		- Decryption of SSL Certificates
		
	- **Performance** (Optimizes delivery)
		- Compression
			
		- Decompression
			
		- Caching
		
	- **Request Modification** (Alters requests)
		- URL Rewriting
		
	- **Traffic Management** (Monitors and logs network activity for analysis and troubleshooting)
		- Monitoring
		- logging
		  
	- **Examples**
		- Nginx
		- HAProxy
		- Apache (with `mod_proxy`)
		- IIS (with ARR)

- **IIS express**
	
	- HTTP access logs
	    
	- Port sharing
	    
	- Windows authentication
	    
	- Management console
	    
	- Process activation
	    
	- Configuration API
	    
	- Request filters
	    
	- HTTP redirect rules

## Application Server

- **Purpose:** Hosts and runs web applications, handling business logic and generating dynamic content. **Functions:**
- **Functions:**
	- Hosting applications
	- Executing business logic
	- Resource management
	- Session management
	- Integration with backend services **Examples:** Apache Tomcat, Microsoft IIS, JBoss

## How They Work Together

- The reverse proxy sits in front of application servers, distributing requests, handling security, and improving performance through load balancing and caching.
- The application server processes the business logic and dynamic content generation.

## Additional Note

- **Apache and IIS**: Both can function as reverse proxy servers. Apache uses the `mod_proxy` module, and IIS uses the Application Request Routing (ARR) module to provide reverse proxy capabilities, including load balancing, SSL termination, and caching.
















