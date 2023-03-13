# NAISS-SENS, sensitive data and Bianca

!!! info "Objectives"
    - We'll briefly get an overview of kinds of sensitive data
    - ... and the **Bianca** system

Content (To remove later)

    - extended from intro course 
    - what is sensitive data?
    - puba & timelines
    - how to apply for projects
    - project management
    - LINK to extra material
    - contact persons




## Sensitive personal data

- Personal data: Traced to now living persons, e.g.
	- Name
	- Address
	- Food preference
	- Size of left nostril

- Sensitive personal data:
	- ethnic origin
	- political opinion
	- religious or philosophical beliefs
	- trade union membership
	- health
	- sex life
	- genetic data
	- biometric data that can uniquely identify a person
		- including some image or auditory recordings
    
- More about sensitive personal data
	- [IMY](https://www.imy.se/en/)
    - [GDPR](https://www.gdpr.eu/)
    - [Data protection](https://ec.europa.eu/info/law/law-topic/data-protection_en)
    - [Skydd av personuppgifter](https://ec.europa.eu/info/law/law-topic/data-protection_sv)
    - [SND](https://snd.gu.se/sv/hantera-data/planera/forskningsdata-med-personuppgifter)
  
- When in doubt, contact your university's [data protection officer](https://www.uppmax.uu.se/support/faq/general-miscellaneous-faq/sensitive+data+questions/).

- Other sensitive data:
	- Confidential information
		- e.g. IP from private industry
	- Secrets
		- sensitive environmental data, e.g. protected species		
	- National security
	
- A Data Protection Impact Assessment(DPIA) is legal requirement for any project with GDPR-data.

- If in doubt (especially with "new" data type), also do a information security evaluation to determine how you should handle the data.

## Pseudonymisation and anonymisation
- Anonymised: no theoretical way at all to determine an individual
- Pseudonymised: anything less

Pseudonymisation is a security mechanism that improves the security of sensitive personal data. *The data is still sensitive*.

But how do you know whether data is anonymised? 
	- "It depends..." 
	- Some data cannot be anonymised at all (e.g. whole genome sequence)
	- One metric for microdata is [K-anonymity](https://en.wikipedia.org/wiki/K-anonymity)

## Apply for project
- [Detailed instructions for project application](https://www.uppmax.uu.se/support/getting-started/applying-for-sens-project/)
[Open NAISS SENS Rounds](https://supr.naiss.se/round/open_type/?type=NAISS+SENS)
- Before GDPR-data will be transferred to UPPMAX, there must be a [Data Processing Agreement](https://www.uppmax.uu.se/support/faq/general-miscellaneous-faq/how-to-establish-a-puba-with-uu/) between UU and the data controlling organisation. These are currently specific to the PI (and sometimes project).

!!! note "Some definitions"
- Project: A collection of resource allocations and people, with an expiration date.
- Compute resources: CPU time used by submitted jobs.
- Storage resources: GB of disk space. /proj has backup, /proj/no-backup has no backup.
- Allocation: The amount of resources a project may consume before hitting a limit.

- Take home message: follow the above instructions, be as complete as detailed as you reasonably can. Submit requests early in the month. 


## Bianca
- Bianca is a great platform for computationally intensive research on sensitive personal data. It can also be useful for:
    - national and international collaboration on sensitive personal data (without a high compute need)
    - other types of sensitive data
    - making sensitive data accessible (on Bianca)
    	- [Swegen](https://snd.gu.se/en/catalogue/study/ext0285)
    	- [SIMPLER](https://www.simpler4health.se/)
- Bianca is not intended for:
    - storing (inactive) data

 
## Bianca's design

- Bianca was designed
	- for sensitive data from large-scale molecular experiments
		- but has since grown into new domains
    - to make accidental data leaks difficult
    - to make correct data management as easy as possible
    - to emulate the HPC cluster environment that SNIC/NAISS users were familiar with
    - to provide a maximum amount of resources
    - and to satisfy regulations.

!!! note "Some definitions"
— Node: A basic "computer", with processor, RAM memory, local disk, and network connection.
- Core: A *part* of a processor (CPU), capable of executing a thread of execution.
- Thread: A series of logical steps, executing a program.
- Multithreading: A program that runs with many threads in parallel. Each thread can occupy one core.


### Bianca has no Internet
... but we have “solutions”

![Image](./img/biancaorganisation-01.png)

- Bianca is only accessible from within Sunet (i.e. from university networks).
- Use VPN outside Sunet. [Link to VPN for UU](https://mp.uu.se/en/web/info/stod/it-telefoni/it-support/network-on-campus/vpn-service)
    - You can get VPN credentials from all Swedish universities.

<br>

- The whole Bianca cluster (blue) contains hundreds of virtual project clusters (green), each of which is isolated from each other and the Internet.
- Data can be transferred to or from a virtual project cluster through the Wharf, which is a special file area that is visible from the Internet.


(todo: 
- upplägg för projects using sensitive & nonsensitive data
- multiple projects or single projects?
- "I need more space/compute"
- )


!!! abstract "Keypoints"
    - Sensitive Personal data is data that could identify a person and that have implication
    - The workflow for a project is When doing your Data management plan, do a DPIA, apply for PUBA(if apropriate), apply for project, DO scicens , Transfer resulted data, close project.
