### Редактирование генератора на примере nancyfx
- скорректировать файлы в `/swagger-codegen/modules/swagger-codegen/src/main/resources/nancyfx`
- скорректировать файлы в `swagger-codegen/modules/swagger-codegen/src/main/java/io/swagger/codegen/languages/NancyFXServerCodegen.java`
- собрать генератор `./run-in-docker.sh mvn package`

### Генерация сервера nancyfx в консоли
```bash
./run-in-docker.sh generate -i sporadic-oas2.yaml -l nancyfx -o /gen/out/nancy-sporadic -DasyncServer=true -Dimmutable=false -DuseDateTimeOffset=true \
-DpackageContext=Host -DpackageName=EA.Sporadic
```

### Генерация сервера через UI
- Положить в папку `tmp` файл `swagger-codegen-2.4.42-SNAPSHOT.jar` из `/swagger-codegen/modules/swagger-codegen/target`
- Поднять сервер с подключением `tmp`
```bash
docker run -e "JAVA_MEM=1024m" -e "HTTP_PORT=80" -p 80:80 --name swagger-generator-v3 -v ./tmp:/jetty_home/lib/shared swaggerapi/swagger-generator-v3
 ```
- Сгенерировать в `http://localhost/ui/` метод `POST http://localhost/api/generate` в "spec" вставить openApi в фромате json
```json
{
  "lang": "nancyfx",
  "spec": {},
  "type": "SERVER",
  "codegenVersion": "V2",
  "options": {
    "additionalProperties": {
      "asyncServer": "true",
      "useDateTimeOffset": "true",
      "packageContext": "Host",
      "interfacePrefix": "I",
      "immutable": "false",
      "packageName": "Inform.Sporadic"
    }
  }
}
```
