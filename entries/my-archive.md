
# The Archive

I need to organize my files. My core concerns are:
 - [Tagging them and retrieving them based on tags](#tagging)
 - [Uniqueness: deduplicating them](#uniqueness)
 - [Redundancy:](#redundancy) The data has to be redundant.
 

General Requirements for tools:
 
 * Cross-platform
 * Ideally command line and scriptable
 * Fast(-ish)
 * Modular
 * Free or cheap
 * Actively maintained
 
## Core Concerns
 
### Tagging


 * **Potential** solution: [TagSpaces](https://www.tagspaces.org/)
 
   Pros:
    * Cross-platform
    * Decentralized - no need for a DB
    * GUI-driven: ease of use
    * Free and open source
   
   Cons:
    * Rewrites file name - how much of an issue is that?
    * Limitations pertaning to storing tags in filenames: lenght and encoding
    * GUI-driven: flexibility and script-ability
    
  * Extending [catcli](https://github.com/rolfen/catcli) to provide taging functionality
    To be accessible we would also need simple shell extensions (contextual menu, etc.) for quick tagging.
  * Custom solution based on SQLite

### Uniqueness

#### Tested solutions
 * CloneSpy (Windows)
 
   Pros:
    * Nice GUI
    * Can generate checksum file for faster compare
    * Possible deletion options including generating a batch file

   Cons:
    * Refuses to deduplicate purely from checksum files, so deduplication is always a slow operation
    * No user-friendly way to inspect duplicates
    * No way to update checksum files. They have to be re-generated after adding files, which can take hours.
    
#### Potential solutions

 * Extending `catcli` to provide deduplication. This thing should accept plugins!
 * Custom solution based on SQLite

### Redundancy

#### Intelligent syncinc across volumes

 * [FreeFileSync](https://freefilesync.org/) Will sync/mirror your files
 
   Pros:
    * Cross-platform
    * Open-source code
    
   Note:
    * Does not seem to reliably detect files which have moved locations.
    * Not sure how easy it is to extend
    * Contribution model: not hosted on github


## Misc


### Directory Organization

[For Photos and Videos](https://gist.github.com/rolfen/244c691660839c27941cd371683039ba), folders are created based on EXIF date.

    
### Comments

I would like to delete duplicates. I would like to define where I want them gone or kept. For example, I have disk F: and disk G: and I would want to find duplicate across these two disks but then delete them on G:.

It would be nice to parse all files and record them into a (Sqlite) database with their hashes. This DB needs to be in sync.

This would make operations (searching, deduplication, organisation, tagging) faster, as there is no need to parse all the files again and re-calculate the hashes every time.
