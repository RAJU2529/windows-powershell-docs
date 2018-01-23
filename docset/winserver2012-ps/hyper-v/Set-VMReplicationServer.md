---
external help file: Hyper-V_Cmdlets.xml
online version: 
schema: 2.0.0
---

# Set-VMReplicationServer

## SYNOPSIS
Configures a host as a Replica server.

## SYNTAX

### UNNAMED_PARAMETER_SET_1
```
Set-VMReplicationServer [[-ReplicationEnabled] <Boolean>]
 [[-AllowedAuthenticationType] <RecoveryAuthenticationType>] [[-ReplicationAllowedFromAnyServer] <Boolean>]
 [-CertificateAuthenticationPort <Int32>] [-CertificateThumbprint <String>] [-ComputerName <String[]>]
 [-DefaultStorageLocation <String>] [-Force] [-KerberosAuthenticationPort <Int32>]
 [-MonitoringInterval <TimeSpan>] [-MonitoringStartTime <TimeSpan>] [-PassThru] [-Confirm] [-WhatIf]
```

### UNNAMED_PARAMETER_SET_2
```
Set-VMReplicationServer [[-ReplicationEnabled] <Boolean>]
 [[-AllowedAuthenticationType] <RecoveryAuthenticationType>] [[-ReplicationAllowedFromAnyServer] <Boolean>]
 [-CertificateAuthenticationPortMapping <Hashtable>] [-CertificateThumbprint <String>]
 [-ComputerName <String[]>] [-DefaultStorageLocation <String>] [-Force]
 [-KerberosAuthenticationPortMapping <Hashtable>] [-MonitoringInterval <TimeSpan>]
 [-MonitoringStartTime <TimeSpan>] [-PassThru] [-Confirm] [-WhatIf]
```

## DESCRIPTION
The **Set-VMReplicationServer** cmdlet configures a host as a Replica server and enables you to specify the types of authentication and ports to use for incoming replication traffic.

To restrict the replication traffic that the Replica server will accept by allowing it only from specific servers, use the New-VMReplicationAuthorizationEntry cmdlet.

## EXAMPLES

### Example 1
```
PS C:\> Set-VMReplicationServer $true -AllowedAuthenticationType Kerberos
```

This example configures the local host as a Replica server and specifies Kerberos for authentication.

### Example 2
```
PS C:\> Set-VMReplicationServer -ReplicationEnabled $true AllowedAuthenticationType -ReplicationAllowedFromAnyServer $true -DefaultStorageLocation d:\DefaultReplicaStorage
```

This example configures a Replica server that accepts replication from all authenticated servers and uses a default storage location of d:\DefaultReplicaStorage.

### Example 3
```
PS C:\> Set-VMReplicationServer -MonitoringInterval "12:00:00" -MonitoringStartTime "17:00:00"
```

This example configures the Replica server with a monitoring interval of 12 hours starting at 17:00 hours.

### Example 4
```
PS C:\> $portmapping = @{"Server1.contoso.com" = 82; "Server2.contoso.com" = 81; "Broker.contoso.com" = 80}
PS C:\> Set-VMReplicationServer -KerberosAuthenticationPortMapping $portmapping
```

This example configures the nodes of the cluster to receive replication on different ports.
The first command declares a variable named portmapping and uses it to store the server names of the nodes and the port to use on each node.
The second command configures each node of the cluster to use port mapping for Kerberos authentication using the values stored in the portmapping variable.

## PARAMETERS

### -AllowedAuthenticationType
Specifies which authentication types the Replica server will use.
Allowed values are Kerberos, Certificate, or CertificateAndKerberos.

```yaml
Type: RecoveryAuthenticationType
Parameter Sets: (All)
Aliases: AuthType

Required: False
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -CertificateAuthenticationPort
Specifies the port on which the Replica server will receive replication data using certificate-based authentication.
This parameter can be set only when the value of the AllowedAuthType parameter is Certificate or CertificateAndKerberos.

```yaml
Type: Int32
Parameter Sets: UNNAMED_PARAMETER_SET_1
Aliases: CertAuthPort

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -CertificateAuthenticationPortMapping
When using Hyper-V Replica with failover clustering and certificate-based authorization, you can use this parameter to specify a different port for each node of the cluster to receive replication.
We recommend that you specify a unique port for each node of the cluster, and one unique port for the Hyper-V Replica Broker.
This parameter can be set only when the Replica server is configured with an authentication type of Certificate or CertificateAndKerberos.

```yaml
Type: Hashtable
Parameter Sets: UNNAMED_PARAMETER_SET_2
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -CertificateThumbprint
Specifies the certificate to use for mutual authentication of the replication data.
This parameter is required only when Certificate is specified as the type of authentication.
Specify the thumbprint of a valid computer certificate from the Personal store.

--The certificate must have all of the following properties to be valid:
--It must not be expired.
--It must include both client and server authentication extensions for extended key usage (EKU), and an associated private key.
--It must terminate at a valid root certificate.
--Meet the requirements for the subject common name (CN):

For servers that are not clustered, the subject common name (CN) must be equal to, or subject alternative name (DNS Name) should contain, the FQDN of the host.

For servers that are clustered, each node must have two certificates - one in which the subject common name (CN) or subject alternative name (DNS Name) is the name of the node, and the other in which subject common name (CN) or subject alternative name (DNS Name) is FQDN of the Hyper-V Replica Broker.

To display a list of certificates in the computer's My store and the thumbprint of each certificate, type the following:

`PS C:\\\> cd cert:\LocalMachine\My`

`PS C:\\\> dir | format-list`

For more information about certificate stores, see http://technet.microsoft.com//library/cc757138.aspxhttp://technet.microsoft.com//library/cc757138.aspx.

```yaml
Type: String
Parameter Sets: (All)
Aliases: Thumbprint

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -ComputerName
Configures Replica server settings for one or more Hyper-V hosts.
NetBIOS names, IP addresses, and fully-qualified domain names are allowable.
The default is the local computer - use "localhost" or a dot (".") to specify the local computer explicitly.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: .
Accept pipeline input: False
Accept wildcard characters: False
```

### -DefaultStorageLocation
Specifies the default location to store the virtual hard disk files when a Replica virtual machine is created.
You must specify this parameter when ReplicationAllowedFromAnyServer is True.

```yaml
Type: String
Parameter Sets: (All)
Aliases: StorageLoc

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Force
Specifies whether the command runs without requiring confirmation.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -KerberosAuthenticationPort


```yaml
Type: Int32
Parameter Sets: UNNAMED_PARAMETER_SET_1
Aliases: KerbAuthPort

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -KerberosAuthenticationPortMapping
When using Hyper-V Replica with failover clustering and Kerberos authorization, you can use this parameter to specify a different port for each node of the cluster to receive replication.
We recommend that you specify a unique port for each node of the cluster, and one unique port for the Hyper-V Replica Broker.
This parameter can be set only when the Replica server is configured with an authentication type of either Kerberos or CertificateAndKerberos.

```yaml
Type: Hashtable
Parameter Sets: UNNAMED_PARAMETER_SET_2
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -MonitoringInterval
Specifies how often (the monitoring interval) replication statistics are computed.
Valid values are: 1 hour, 2 hours, 3 hours, 4 hours, 6 hours, 8 hours, 12 hours, 24 hours, 2 days, 3 days, 4 days, 5 days, 6 days, 7 days.
Specify in the format days:hours:minutes:seconds, such as 01:00:00 for 1 hour, or 1.00:00:00 for 1 day.

```yaml
Type: TimeSpan
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: 24
Accept pipeline input: False
Accept wildcard characters: False
```

### -MonitoringStartTime
Specifies when the monitoring interval starts.

```yaml
Type: TimeSpan
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: 9 AM
Accept pipeline input: False
Accept wildcard characters: False
```

### -PassThru
Specifies that a **VMReplicationServer** object is to be passed through to the pipeline representing the replication settings of the Replica server.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ReplicationAllowedFromAnyServer
Specifies whether to accept replication requests from any server.
When specified as **true**, DefaultStorageLocation must also be specified.
The default storage location and DEFAULT trust group tag are used for virtual machine replicas.

```yaml
Type: Boolean
Parameter Sets: (All)
Aliases: AllowAnyServer

Required: False
Position: 3
Default value: True
Accept pipeline input: False
Accept wildcard characters: False
```

### -ReplicationEnabled
Specifies whether the host is enabled as a Replica server.

```yaml
Type: Boolean
Parameter Sets: (All)
Aliases: RepEnabled

Required: False
Position: 1
Default value: True
Accept pipeline input: False
Accept wildcard characters: False
```

### -Confirm
Prompts you for confirmation before running the cmdlet.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -WhatIf
Shows what would happen if the cmdlet runs.
The cmdlet is not run.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

## OUTPUTS

### 
None by default; **VMRecoveryServer** if **-PassThru** is specified.

## NOTES

## RELATED LINKS

[00000000-0000-0000-0000-000000000000](00000000-0000-0000-0000-000000000000)
