# Proposed LPWAN REST API Changes

- GET /api/networkProtocolHandlers


  - Change returned data:
    [
        { 
            "protocolHandlerName": "LoraOpenSource",
            "oauthUrl": "<see notes below>",
            "protocolHandlerNetworkFields": [
                {
                   {
                       "fieldName": "",
                       "fieldDesc": "",
                       "fieldHelp": "",
                       "fieldType": "",
                       "displayWithQueryParameter": ""
                   },...
                },...
            ]
        },...
    ]
    
    where:
        oauthUrl: [optional] Indicates OAuth handling for this network.
                  URL includes placeholders for other fields based on 
                  fieldName - e.g., %clientId%.  Required to include the 
                  redirect URL placeholder %redirect%, which the UI uses 
                  to provision a return URL once Oath completes.
        protocolHandlerNetworkFields:
                  Fields required by the protocol handler.  These will be 
                  placed in the securityData for the network.  If not provided,
                  defaults to username/password.
        fieldName: The name of the field in the json securityData
        fieldDesc: The label text to display on the UI
        fieldHelp: [optional] A help string displayed under the field
        fieldType: The data type, one of "string", "password", "integer",
                   "number", "boolean", (more?)
        displayWithQueryParameter: [optional] a string that, if matching a
                   query parameter name from the URL, causes this field to
                   display, pre-populated with the data as specified by the
                   query parameter.  In an update screen, if the data is in
                   the securityData, it is also displayed.  Field is read-only.

- GET /api/networktypes
  - Add a query parameter "additionalFields=<type>"
  - Causes REST Server to find the additional fields needed for the network
    based on the networkProtocol assigned to that network.  Same format as
    above (exclude OAuth handling?)  For example,
    "additionalFields=applications" would return additional fields required
    for the Application UI for the Network type.  For example,
    
    GET /api/networktypes?companyid=xx&additionalFields=applications might 
    return something like:
    [
        { 
            "networkTypeName": "LoraOpenSource",
            .
            .
            .
            "fields": [
                {
                   {
                       "fieldName": "loriotAppId",
                       "fieldDesc": "Loriot Application ID",
                       "fieldHelp": "The Application ID provided by the Loriot network.  Loriot requires pre-creation of applications by the user.  If not provided, device data seen by the Loriot network cannot be returned.",
                       "fieldType": "string"
                   },...
                },...
            ]
        },...
    ]

    
    
