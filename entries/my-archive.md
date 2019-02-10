I need to organize my files. My concerns are:
 - [Tagging them and retrieving them based on tags](#tagging)
 - [Uniqueness: deduplicating them](#uniqueness)
 - [Backup: Intelligent syncinc across volumes](#backup)
 

Requirements:
 
 * Cross-platform
 * Ideally command line and scriptable
 * Fast(-ish)
 * Modular
 * Free or cheap
 * Actively maintained
 
## Tagging


 * [TagSpaces](https://www.tagspaces.org/)
 
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

## Uniqueness


## Backup

 * [FreeFileSync](https://freefilesync.org/)
 
   Pros:
    * Cross-platform
    
   Note:
    * Does not seem to reliably detect files which have moved locations.
    
    
## Comments

I would like to delete duplicates. I would like to define where I want them gone or kept. For example, I have disk F: and disk G: and I would want to find duplicate across these two disks but then delete them on G:.

It would be nice to parse all files and record them into a (Sqlite) database with their hashes. This DB needs to be in sync.

This would make operations (searching, deduplication, organisation, tagging) faster, as there is no need to parse all the files again and re-calculate the hashes every time.
