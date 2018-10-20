# HCN JSON Document Body Schema

## HCN Network Schema

// Network
{
    "Id" : <string>,
    "Owner" : <string>,
    "SchemaVersion" : {
        "Major" : <uint32>,
        "Minor" : <uint32>
    },
    "Flags" : <enum bit mask>, 
         // AsString; Values: 
         // "None" (0),
         // "EnableDnsProxy" (1),
         // "EnableDhcpServer" (2),
         // "IsolateVSwitch" (8)
    "Type"  : <enum>, 
         // AsString; Values: 
         // "NAT" (0), 
         // "ICS" (1), 
         // "Transparent" (2)
    "Ipams" : [ {
         "Type" : <enum>, 
             // AsString; Values: 
             // "Static" (0), 
             // "Dhcp" (1)
         "Subnets" : [ {
                "IpAddressPrefix" : <ip prefix in CIDR>,
                "Policies" : [ {
                        "Type" : <enum>, 
                            // AsString; Values: 
                            // "VLAN" (0)
                        "Data" : <any>
                 } ],
                "Routes" : [ {
                       "NextHop" : <ip address of the next hop gateway>,
                       "DestinationPrefix" : <ip prefix in cidr>,
                       "Metric" : <route metric in uint8>,
                 } ],
          } ],
     } ],
    "Policies" : [{
         "Type" : <enum>, 
              // AsString; Values: 
              // "NetAdapterName" (1), 
              // "InterfaceConstraint" (2)
         "Data" : <any>
    }],
    "Dns" : {
        "Suffix" : <local connection specific suffix>,
        "Search" : [<list of additional suffixes>],
        "ServerList" : [<string>],
        "Options" : [<string>],
    },
    "MacPool" : {
        "Ranges" : [ {
              "StartMacAddress" : <string>,
              "EndMacAddress" : <string>
         } ],
    },
}

## HCN Endpoint Schema

// Endpoint 
{
    "Id" : <string>,
    "Owner" : <string>,
    "SchemaVersion" : {
        "Major" : <uint32>,
        "Minor" : <uint32>
    },
    "Flags" : <enum bit mask>, 
         // AsString; Values: 
         // "None" (0),
         // "DisableInterComputeCommunication" (2)
    "HostComputeNetwork" : <string>,
    "MacAddress" : <string>,
    "Policies" : [ {
         "Type" : <enum>, 
              // AsString; Values: 
              // "PortMapping" (0), 
              // "ACL" (1)
         "Data" : <any>
    } ],
    "Dns" : {
        "Suffix" : <local connection specific suffix>,
        "Search" : [<list of additional suffixes>],
        "ServerList" : [<string>],
        "Options" : [<string>],
    },
    "IPConfigurations" : [ {
        "IPAddress" : <ip address>,
        "PrefixLength" : <prefix length uint16>,
    } ],
    "Routes" : [ {
        "NextHop" : <ip address of the next hop gateway>,
        "DestinationPrefix" : <ip prefix in cidr>,
        "Metric" : <route metric in uint8>,

    } ],
}

## HCN Policiy Schemas

### HCN VLAN Policy Schema

// VlanPolicy
{
    "Type" : "VLAN",
    "IsolationId" : <uint32>,
}

### HCN Port Mapping Policy Schema

// PortMappingPolicy
{
    "Type" : "PortMapping",
    "Protocol" : <enum>,
         // AsString; Values: 
         // "TCP" (0),
         // "UDP" (1),
         // "ICMPv4" (2),
         // "ICMPv6" (3),
         // "IGMP" (4),
    "InternalPort" : <uint16>,
    "ExternalPort" : <uint16>,
}

## HCN Load Balancer Schema

// Host Compute LoadBalancer
{
    "Id" : <string>,
    "Owner" : <string>,
    "SchemaVersion" : {
        "Major" : <uint32>,
        "Minor" : <uint32>
    },
    "Flags" : <enum bit mask>, 
         // AsString; Values: 
         // "None" (0),
         // "EnableDirectServerReturn" (1)
         // "EnableInternalLoadBalancer" (2)
    "HostComputeEndpoints" : [<Host compute Endpoint id>],
    "VirtualIPs" : [<Virtual IpAddress>],
    "PortMappings" : [ {
        "Type" : "PortMapping",
        "Protocol" : <enum>,
             // AsString; Values: 
             // "TCP" (0),
             // "UDP" (1),
             // "ICMPv4" (2),
             // "ICMPv6" (3),
             // "IGMP" (4),
        "InternalPort" : <uint16>,
        "ExternalPort" : <uint16>,
    } ],
    "Policies" : [ {
         "Type" : <enum>, 
              // AsString; Values: 
              // "SourceVirtualIp" (0), 
         "Data" : <any>
    } ],
}

## HCN Network Namespace Schema

// Namespace
{
    "Id" : <string>,
    "Owner" : <string>,
    "SchemaVersion" : {
        "Major" : <uint32>,
        "Minor" : <uint32>
    },
    "NamespaceId" : <uint32>,
    "NamespaceGuid" : <guid>,
    "Type"  : <enum>,
              // AsString; Values: 
              // "Host" (0), 
              // "HostDefault" (1), 
              // "Guest" (2), 
              // "GuestDefault" (3)
    "Resources" : [ {
          "Type"  : <enum>,
              // AsString; Values: 
              // "Container" (0), 
              // "Endpoint" (1)
          "Data"  : <any>
    } ],
}


## HCN Notification Schema

// Notification
{
    "ID" : Guid,
    "Flags" : <uint32>,
}

## HCN Result Error Record Schema

// ErrorSchema
{
    "ErrorCode" : <uint32>,
    "Error" : <string>,
    "Success" : <bool>,
}