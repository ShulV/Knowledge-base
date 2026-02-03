## Генерация ObjectFactory для маршалера JAXB
#xjc #marshal #unmarshal #jaxb #xsd #xml #util

```bash
~/.jdks/jdk-8/bin/xjc -p ru.spotic.lib.util.jaxb.entity.external_processing ./external_processing.xsd
```

P.S. генерит не в тот пакет, но хотя бы генерит. Не стал разбираться почему

пример генерации по xml схеме и wsdl
```sh
#!/bin/sh  
# Полный путь к JDK, этих утилит нет в стандартном наборе после 8 версии. При выполнении указать свой путь до JDK с java 8  
JDK_8_BIN="$HOME/.jdks/jdk-8/bin"  
  
WSIMPORT="${JDK_8_BIN}/wsimport"  
XJC="${JDK_8_BIN}/xjc"  
  
JAVA_FOLDER_PATH="$HOME/IdeaProjects/application/some-api/src/main/java"  
  
${WSIMPORT} -extension -keep -Xnocompile -d "${JAVA_FOLDER_PATH}" -p ru.company.some.api.service.fns.model.some_integration SmzIntegrationService_1.wsdl  
${XJC} -no-header -extension -d "${JAVA_FOLDER_PATH}" -p ru.company.some.api.service.fns.model.some_integration.messages scheme-v0_35_190126.xsd.xml  
  
# При генерации ломаются импорты, т.к. java старая, нужно вручную менять javax -> jakarta  
# (или найти инструменту современную альтернативу)
```