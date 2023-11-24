# AWS Regions & Availability Zones
## AWS Regions
- An AWS region is a geographical area where Amazon Web Services (AWS) has built and operates multiple data centers.
- Regions are named according to their geographical location e.g. `us-east-1` or `af-south-1`.
- Consider the following when choosing a region:
	- Compliance with data governance and legal requirements (data can never leave a region by itself).
	- Proximity to end users (closer proximity reduces latency).
	- Availability of services (newer services aren't always available in all regions).
	- Pricing (pricing can vary from region to region).
## AWS Availability Zones (AZs)
-  Availability zones are groups of one or more independent data centers within a region.
- Each region has a minimum of 3 and maximum of 6 availability zones.
- Availability zones are linked together by high-bandwidth, ultra-low-latency networking to form a region.
- Availability zones are identified by letters at the end of the region name e.g. `us-east-1a` or `as-south-1b`.