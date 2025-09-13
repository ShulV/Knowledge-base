## Переопределение значения одного ключа в JSON:
#overide #jakson #json #node #parsing #key #value #tree
`com.fasterxml.jackson`
```java
private String getJsonIdentificationSettings(String overrideRedirectUrl, long clientId) {  
    String jsonSettings = systemParameterService.get(  
            Parameter.General.System.MTS_KYC_ID_REQUEST_JSON_SETTING, frontService.getCore().getId(), "");  
    if (overrideRedirectUrl == null) {  
        log.warn("Override redirect url is null, using settings from system parameter: [client_id = '{}']", clientId);  
        return jsonSettings;  
    }  
    JsonNode rootNode;  
    try {  
        rootNode = objectMapper.readTree(jsonSettings);  
    } catch (JsonProcessingException e) {  
        log.error("Cannot read identification settings json: [json_settings = '{}', client_id = '{}']",  
                jsonSettings, clientId, e);  
        return null;  
    }  
    JsonNode redirectUrlNode = rootNode.path(JSON_REDIRECT_URL_KEY);  
    if (redirectUrlNode.isMissingNode()) {  
        log.error("Cannot get identification settings for request, 'redirectUrl' key is missing from JSON: " +  
                "[json_from_system_parameters ='{}', client_id = '{}']", jsonSettings, clientId);  
        return null;  
    }  
    try {  
        ((ObjectNode) rootNode).put(JSON_REDIRECT_URL_KEY, overrideRedirectUrl);  
        return objectMapper.writerWithDefaultPrettyPrinter().writeValueAsString(rootNode);  
    } catch (JsonProcessingException e) {  
        log.error("Cannot read identification settings json: [json_settings = '{}', client_id = '{}']",  
                jsonSettings, clientId, e);  
        return null;  
    }  
}
```
P.S. не нравится, что сделано с возвращением null, но да ладно.