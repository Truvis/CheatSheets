# Setup
## Initial Setup after ISO install 
- Comment out these lines in /usr/share/rock/roles/elasticsearch/templates/es-jvm.options.j2
- a. #-XX: +UseConcMarkSweepGC
- b. #-XX:CMSInitiatingOccupancyFraction=75
- c. #=XX: +UseCMSInitiatingOccupancyOnly
