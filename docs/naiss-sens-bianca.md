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

- <https://www.snic.se/allocations/snic-sens/>
- Traced to now living persons, e.g.
    - human genomic data
    - images/videos containing persons
    - health registry (health data records from healthcare providers)
- More about sensitive data
    - [GDPR](https://gdpr.eu/)
    - [Data protection](https://ec.europa.eu/info/law/law-topic/data-protection_en)
    - [Skydd av personuppgifter](https://ec.europa.eu/info/law/law-topic/data-protection_sv)
  
- When in doubt, contact your university's [data protection officer](https://www.uppmax.uu.se/support/faq/general-miscellaneous-faq/sensitive+data+questions/).
- Generally, there must be a [Data Processing Agreement](https://www.uppmax.uu.se/support/faq/general-miscellaneous-faq/how-to-establish-a-puba-with-uu/) between UU and the data controlling university.

## Apply for project
[Open NAISS SENS Rounds](https://supr.naiss.se/round/open_type/?type=NAISS+SENS)

## Bianca
- Bianca is a great platform for computationally intensive research on sensitive personal data. It can also be useful for:
    - national and international collaboration on sensitive personal data (without a high compute need)
    - other types of sensitive data
- Bianca is not good for:
    - storing data
    - publishing data
        - unless the dataset is very popular among Bianca users, e.g. [Swegen](https://snd.gu.se/en/catalogue/study/ext0285), [SIMPLER](https://www.simpler4health.se/)

 
## Bianca's design

- Bianca was designed
    - to make accidental data leaks difficult
    - to make correct data management as easy as possible
    - to emulate the HPC cluster environment that SNIC/NAISS users were familiar with
    - to provide a maximum amount of resources
    - and to satisfy regulations.

### Bianca has no Internet
... but we have “solutions”

![Image](./img/biancaorganisation-01.png)

- Bianca is only accessible from within Sunet (i.e. from university networks).
- Use VPN outside Sunet. [Link to VPN for UU](https://mp.uu.se/en/web/info/stod/it-telefoni/it-support/network-on-campus/vpn-service)
    - You can get VPN credentials from all Swedish universities.

<br>

- The whole Bianca cluster (blue) contains hundreds of virtual project clusters (green), each of which is isolated from each other and the Internet.
- Data can be transferred to or from a virtual project cluster through the Wharf, which is a special file area that is visible from the Internet.



!!! abstract "keypoints"
    - bullet 1
    - bullet 2
