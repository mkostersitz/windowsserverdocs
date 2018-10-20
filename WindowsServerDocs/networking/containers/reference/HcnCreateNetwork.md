# HcnCreateNetwork

## Syntax
`HRESULT result = HcnCreateNetwork(Id, Settings, Network, ErrorRecord)`

### Parameters
|Parameter     |Description|
|---|---|---|---|---|---|---|---| 
|`Id`| **[In]** specifies a unique GUID string by which the network will be referenced|
|`Settings`| **[In]** JSON document specifying the settings of the new network|
|`Network`| **[Out]** Receives a handle to the newly created network|
|`ErrorRecord`| **[Out] [Optional]** Receives a JSON document on failure with extended result information|
|    |    | 



## Return Values
|Return | Description|
|---|---|
|`S_OK`|On success|
|HResult error code|Failure|
|     |     |

## Remarks

The caller must release any buffers created using CoTaskMemFree