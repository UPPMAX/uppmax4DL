# Transfering files to/from Bianca
    - wharf, transit server, ...
    - pros/cons of different solutions
    - stress throughout the day that is it important to keep the entire chain of transfering the data secure
    - rsync, scp/sftp

!!! info "Objectives" 

    - We'll go through the methods to tranfer files
       - wharf
       - transit server
       - rsync, scp/sftp
       - pros/cons of different solutions
       
 !!! warning
 
     It is important to keep the entire chain of transfering the data secure

## How does it work?

![Bianca](./img/biancaorganisation-01.png)

### The Wharf

!!! info "Wharf is a harbour dock"

    - The Wharf area can be reached from both Bianca and any other place on Bianca.
    - Therefore it serves as a bridge between Internet and Bianca.
    
 

## Data transfers:
- <https://www.uppmax.uu.se/support/user-guides/bianca-user-guide/> 
    - section 3: Transfer files to and from Bianca

a.	First step is on Bianca
b.	Second step is from a computer outside of Bianca. 
c.	Using standard sftp client
d.	Some other sftp client
e.	Mounting the sftp-server with sshfs
f.	Bulk recursive transfer with only standard sftp client
g.	Transit Server

## Transit

- To facilitate secure data transfers to, from and within the system for computing on sensitive data (bianca/castor) a service is available via ssh at transit.uppmax.uu.se.
- You can connect to transit via ssh. Once connected, you should see a short help message. The most important thing there is the
mount_wharf command
which you can use to mount a project from the bianca wharf


## NGI Deliver 

- Not covered here but 
- https://www.uppmax.uu.se/support/user-guides/deliver-user-guide/
- https://www.uppmax.uu.se/support/user-guides/grus-user-guide/

!!! abstract "keypoints"
    - The "WHARF" works like a dock at the harbour.
    - There are several ways to use the wharf to tranfer files
        - copy
        - transit server
        - rsync, scp/sftp

