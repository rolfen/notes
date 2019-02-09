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
