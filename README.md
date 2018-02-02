# Attacking the Nintendo 3DS Boot ROMs

## [View PDF](https://github.com/Plailect/bootroms/blob/master/bootroms.pdf)

### Abstract

We demonstrate attacks on the boot ROMs of the Nintendo 3DS in order to exfiltrate secret information from normally protected areas of memory and gain persistent early code execution on devices which have not previously been compromised. The attack utilizes flaws in the RSA signature verification implementation of one of the boot ROMs in order to overflow ASN.1 length fields and cause invalid firmware images to appear valid to the signature parser. This is then used to load a custom firmware image which overwrites the data-abort vector with a custom data abort handler, then induces a data-abort exception in order to reliably redirect boot ROM code flow at boot time. This executes a payload which, due to its reliable early execution by a privileged processor, is able to function as a persistent exploit of the system in order to exfiltrate secret information (such as encryption keys) from normally protected areas of memory.

### Background

Information in this article (especially the code execution vulnerability) is original, independent work unless cited otherwise. Note that the code execution vulnerability detailed here is the same one documented publicly as "boot9strap" by much of this team including "SciresM" on sites such as [3DBrew](https://www.3dbrew.org). Additionally, note that the RSA signature parsing vulnerability detailed here is a different implementation of the concept documented publicly as "sighax" by "derrek" and "nedwill" and "naehrwert" at the [2016 33c3 conference](https://media.ccc.de/v/33c3-8344-nintendo_hacking_2016).