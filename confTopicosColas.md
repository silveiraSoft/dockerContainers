# TOPICOS Y COLAS

docker exec -it redis bash
docker exec -it redis redis-cli

aws configure set aws_access_key_id "dummy" --profile test-profile
aws configure set aws_secret_access_key "dummy" --profile test-profile
aws configure set region "us-east-1" --profile test-profile
aws configure set output "table" --profile test-profile

## CREAR CONTENEDOR CON IMAGEN DE LOCALSTACK

### DOCKER COMPOSE
Crear un contenedor docker compose con la siguiente estructura y nombre y en la raiz del fichero ejecutar en la terminal el comando
`docker-compose up`
[docker-compose.yml]
``` YML
services:
  localstack:
    image: localstack/localstack:0.11.2
    container_name: localstack_dllo
    ports:
      - '4563-4599:4563-4599'
      - '8055:8080'
    environment:
      - AWS_DEFAULT_REGION=us-east-1
      - SERVICES=s3,sns,sqs,dynamodb
      - DEBUG=1
      - DATA_DIR=/tmp/localstack/data
    volumes:
      - './.localstack:/tmp/localstack'
      - '/var/run/docker.sock:/var/run/docker.sock'
```
### Uso de CLI-TERMINAL
- Abrir la terminal cli dentro del contenedor de local stack y configurar aws
- Escribir dentro de la terminal 
  `aws configure`

### ESTRUCTURA TOPICOS Y COLAS

`Ejemplo nombre topicos y colas`
- t-topico1-dev
- q-cola1-dev


[CrearTopicos]
```cli contenedor localstack
aws --endpoint-url=http://localhost:4566 sns create-topic --name t-topico1-dev
```

[CrearColas]
```cli contenedor localstack
aws --endpoint-url=http://localhost:4566 sqs create-queue --queue-name q-cola1-dev
```

[SuscribirTopicoACola]
``` cli contenedor localstack
aws --endpoint-url=http://localhost:4566 sns subscribe --topic-arn   arn:aws:sns:us-east-1:000000000000:t-topico1-dev --profile test-profile --protocol sqs --notification-endpoint http://localstack:4566/000000000000/q-cola1-dev
```

[SuscribirTopicoAColaConAtributos]
``` cli contenedor localstack
aws --endpoint-url=http://localhost:4566 sns subscribe --topic-arn   arn:aws:sns:us-east-2:000000000000:t-topico1-dev --protocol sqs --notification-endpoint arn:aws:sns:us-east-2:000000000000:q-cola1-dev --attributes "{\"RawMessageDelivery\":\"true\"}" 
```

`--attributes "{\"RawMessageDelivery\":\"true\"}"`
Con esta configuracion se recibe el mensaje de la suscripcion sin datos adicionales de hora o fecha


[RecibirEventosEnColas]
aws --endpoint-url=http://localhost:4566 sqs receive-message --queue-url http://localhost:4566/000000000000/q-cola1-dev --profile test-profile --region us-east-2 --output json | cat

[EnviarEventosATopicos]

aws sns publish --endpoint-url=http://localhost:4566 --topic-arn arn:aws:sns:us-east-1:000000000000:t-topico1-dev --message "Hello World" --profile test-profile --region us-east-1 --output json | cat

[BorrarCola]
aws --endpoint-url=http://localhost:4566 sqs delete-queue --queue-url http://localhost:4566/000000000000/q-cola1-dev

[ListarColas]
aws --endpoint-url=http://localhost:4566 sqs list-queues

[ListarTopicos]
aws --endpoint-url=http://localhost:4566 sns list-topics

[ListarSuscripciones]
aws --endpoint-url=http://localhost:4566 sns list-subscriptions
[ListarAtributosDeSuscripcion]
aws sns get-subscription-attributes --subscription-arn arn:aws:sns: ...




///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

### Datos tomados de los archivos de configuracion application.yml

**configuration/executemechanism**

```YML
messaging:
    subscribe-destination: q-cys-cli-talos-execute-mechanism-qa
    publish-destination: t-cys-cli-talos-app-qa
 messaging-error:
    publish-destination: t-cys-cli-talos-error-qa
```



**configuration/poc_withoutcredentials**
```YML
  messaging:
    subscribe-destination: q-cys-cli-talos-send-response-qa
    publish-destination: t-cys-cli-talos-app-qa
```


**configuration/recognizecache**
```YML
  messaging:
    splunk:
      publish-destination: t-cys-cli-talos-app-qa
      error-destination: t-cys-cli-talos-app-qa
```


**configuration/requestcompletion**
```YML
  messaging:
    #q-cys-cli-talos-request-completeness-qa
    subscribe-destination: ${TALOS_MESSAGING_SUBSCRIBE}
    #t-cys-cli-talos-app-qa
    publish-destination: ${TALOS_MESSAGING_COMPLETE_DESTINATION}

  messaging-error:
    #t-cys-cli-talos-app-qa
    publish-destination: ${TALOS_MESSAGING_ERROR_DESTINATION}

  messaging-rest-splunk:
    #t-cys-cli-talos-app-qa
    publish-destination: ${TALOS_MESSAGING_SPLUNK_DESTINATION}
```


**configuration/restrequest**
```YML
  messaging:
    #t-cys-cli-talos-app-qa
    publish-destination: ${TALOS_MESSAGING_PUBLISH_DESTINATION}
    #t-cys-cli-talos-app-qa
    error-destination: ${TALOS_MESSAGING_ERROR_DESTINATION}
    subscribe-destination: q-talos-xxx-qa
```

**configuration/ruleprocessor**
```YML
  messaging:
    subscribe-destination: q-cys-cli-talos-rule-process-qa
    publish-destination: t-cys-cli-talos-app-qa

  messaging-error:
    publish-destination: t-cys-cli-talos-app-qa

  messaging-rest-splunk:
    #t-cys-cli-talos-app-qa
    publish-destination: t-cys-cli-talos-app-qa
```


**configuration/sendresponse**
```YML
  messaging:
    publish-destination: ${TALOS_MESSAGING_PUBLISH_DESTINATION}
    error-destination: ${TALOS_MESSAGING_ERROR_DESTINATION}

    messaging-error:
      publish-destination: t-cys-cli-talos-error-qa

  queue:
    name: ${TALOS_MESSAGING_SUBSCRIBE}
```

**configuration/validatemechanism**
```YML
  messaging:
    subscribe-destination: q-cys-cli-talos-validate-mechanism-qa
    publish-destination: t-cys-cli-talos-app-qa

  messaging-error:
    publish-destination: t-cys-cli-talos-app-qa
```

**Dentro de los archivos application.yml configurar end-point**
```YML
cloud:
  aws:
    stack:
      auto: xxxxx
    credentials:
      accessKey: xxxxxx
      secretKey: xxxxxx
    end-point:
      url: http://localhost:4566
```


### Referencias
https://medium.com/@anchan.ashwithabg95/using-localstack-sns-and-sqs-for-devbox-testing-fa09de5e3bbb

https://onexlab-io.medium.com/localstack-sns-sqs-1f48bae55cae

https://onexlab-io.medium.com/localstack-sqs-a0c36fd13108

////////////////////////////PARA PROBAR////////////////////////////

elastic cache 
``` 
aws --endpoint-url=http://localhost:4566  elasticache create-cache-cluster --cache-cluster-id i1

///////////////////////////////////////////////////////////////////////

en la sub q-cys-cli-talos-validate-mechanism-qa:

{
  "event": [
    "validateMechanism"
  ]
}



q-cys-cli-talos-request-completeness-qa

{
  "event": [
    "requestCompleteness"
  ]
}



q-cys-cli-talos-rule-process-qa

{
  "event": [
    "ruleProcess"
  ]
}



q-cys-cli-talos-send-response-qa

{
  "event": [
    "sendResponse"
  ]
}



q-cys-cli-talos-execute-mechanism-qa

{
  "event": [
    "executeMechanism"
  ]
}



aws --endpoint-url=http://localhost:4566 sqs receive-message --queue-url http://localhost:4566/queue/q-cys-cli-talos-send-response-qa --attribute-names All --message-attribute-names All --max-number-of-messages 10