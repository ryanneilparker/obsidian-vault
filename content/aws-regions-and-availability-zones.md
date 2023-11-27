## AWS Regions & Availability Zones

### AWS Regions

- **Definition**: Geographical areas housing multiple AWS data centers.
- **Naming**: Identified by geographical location (e.g., `us-east-1`, `af-south-1`).
- **Considerations**:
    - _Compliance_: Ensures adherence to data governance and legal requirements.
    - _Proximity_: Impact on latency for end users (closer proximity reduces latency).
    - _Service Availability_: Not all regions offer the same services at the same time.
    - _Pricing Variability_: Costs can vary between regions.

### AWS Availability Zones (AZs)

- **Definition**: Independent data center groups within a region.
- **Number per Region**: Ranges from 3 to 6 AZs.
- **Interconnection**: High-speed, low-latency networking links AZs to form a region.
- **Identification**: AZs labeled with letters at the end of region names (e.g., `us-east-1a`, `as-south-1b`).