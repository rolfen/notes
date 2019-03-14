
List all manually installed unstable packages  
`aptitude versions '?archive(testing)!?archive(stable)?installed!?automatic'`

Purge abandoned config files
`sudo aptitude purge '?config-files'`
