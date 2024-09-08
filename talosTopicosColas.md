**LISTADO DE TOPICOS APPLICATION YML**
`t-cys-cli-talos-app-qa`
aws --endpoint-url=http://localhost:4566 sns create-topic --name t-cys-cli-talos-app-qa
aws --endpoint-url=http://localhost:4566 sns create-topic --name t-cys-cli-talos-app-qa --region us-east-2

`t-cys-cli-talos-error-qa`
aws --endpoint-url=http://localhost:4566 sns create-topic --name t-cys-cli-talos-error-qa

aws --endpoint-url=http://localhost:4566 sns create-topic --name t-cys-cli-talos-error-qa --region us-east-2


**LISTADO DE TOPICOS WORD**
- t-cys-cli-talos-app-qa
- t-cys-cli-talos-error-qa
- t-arqref-qa

**LISTADO DE COLAS DE APPLICATION YML**
`q-cys-cli-talos-execute-mechanism-qa`
aws --endpoint-url=http://localhost:4566 sqs create-queue --queue-name q-cys-cli-talos-execute-mechanism-qa


`q-cys-cli-talos-send-response-qa`
aws --endpoint-url=http://localhost:4566 sqs create-queue --queue-name q-cys-cli-talos-send-response-qa


`q-cys-cli-talos-request-completeness-qa`
aws --endpoint-url=http://localhost:4566 sqs create-queue --queue-name q-cys-cli-talos-request-completeness-qa


`q-talos-xxx-qa`
aws --endpoint-url=http://localhost:4566 sqs create-queue --queue-name q-talos-validate-qa


`q-cys-cli-talos-rule-process-qa`
aws --endpoint-url=http://localhost:4566 sqs create-queue --queue-name q-cys-cli-talos-rule-process-qa


`q-cys-cli-talos-validate-mechanism-qa`
aws --endpoint-url=http://localhost:4566 sqs create-queue --queue-name q-cys-cli-talos-validate-mechanism-qa


**LISTADO DE COLAS DE ARCHIVO WORD**

q-cys-cli-talos-validation-completeness-qa

q-cys-cli-talos-rule-process-qa 

q-cys-cli-talos-validate-qa 

q-cys-cli-talos-send-response-qa

q-cys-cli-talos-execute-mechanism-qa

q-cys-cli-talos-validate-splunk-qa



**SUSCRIPCIONES DE COLAS A TOPICOS**

aws --endpoint-url=http://localhost:4566 sns subscribe --topic-arn   arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa --protocol sqs --notification-endpoint arn:aws:sns:us-east-2:000000000000:q-cys-cli-talos-execute-mechanism-qa --attributes "{\"RawMessageDelivery\":\"true\"}"

aws --endpoint-url=http://localhost:4566 sns subscribe --topic-arn   arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa --protocol sqs --notification-endpoint arn:aws:sns:us-east-2:000000000000:q-cys-cli-talos-send-response-qa --attributes "{\"RawMessageDelivery\":\"true\"}" 

aws --endpoint-url=http://localhost:4566 sns subscribe --topic-arn   arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa --protocol sqs --notification-endpoint arn:aws:sns:us-east-2:000000000000:q-cys-cli-talos-request-completeness-qa --attributes "{\"RawMessageDelivery\":\"true\"}" 

aws --endpoint-url=http://localhost:4566 sns subscribe --topic-arn   arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa --protocol sqs --notification-endpoint arn:aws:sns:us-east-2:000000000000:q-cys-cli-talos-rule-process-qa --attributes "{\"RawMessageDelivery\":\"true\"}" 

aws --endpoint-url=http://localhost:4566 sns subscribe --topic-arn   arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa --protocol sqs --notification-endpoint arn:aws:sns:us-east-2:000000000000:q-cys-cli-talos-validate-mechanism-qa --attributes "{\"RawMessageDelivery\":\"true\"}" 


aws --endpoint-url=http://localhost:4566 sns subscribe --topic-arn   arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa --protocol sqs --notification-endpoint arn:aws:sns:us-east-2:000000000000:q-cys-cli-talos-validation-completeness-qa --attributes {"\"RawMessageDelivery\":\"true\"}"

aws --endpoint-url=http://localhost:4566 sns subscribe --topic-arn   arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa --protocol sqs --notification-endpoint arn:aws:sns:us-east-2:000000000000:q-cys-cli-talos-validate-splunk-qa  --attributes "{\"RawMessageDelivery\":\"true\"}"


**Listar Suscricpiones para obtener el nombre de la suscripcion**
[ListarSuscripciones]
aws --endpoint-url=http://localhost:4566 sns list-subscriptions



**Configurar Filter Policy**

1. "SubscriptionArn": "arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa:29d17950-1d7f-4cbc-a211-652856f3b1fa"

- Ver datos de la suscripcion
aws sns get-subscription-attributes --endpoint-url=http://localhost:4566 --subscription-arn arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa:b0bafde5-16f3-412a-8baf-81aeba235c02

2. "SubscriptionArn": "arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa:b613486f-67ff-403a-906c-6a79e7e80c27"

- Ver datos de la suscripcion
aws sns get-subscription-attributes --endpoint-url=http://localhost:4566 --subscription-arn arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa:b613486f-67ff-403a-906c-6a79e7e80c27

3. "SubscriptionArn": "arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa:a83c84a8-d1d6-43b0-b55d-a12fafdbed59"

- Ver datos de la suscripcion
aws sns get-subscription-attributes --endpoint-url=http://localhost:4566 --subscription-arn arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa:a83c84a8-d1d6-43b0-b55d-a12fafdbed59

4. "SubscriptionArn": "arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa:26c08a69-57fb-4e6f-9e07-a462aee9afac"


- Ver datos de la suscripcion
aws sns get-subscription-attributes --endpoint-url=http://localhost:4566 --subscription-arn arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa:26c08a69-57fb-4e6f-9e07-a462aee9afac

5. "SubscriptionArn":"arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa:afbb76cc-e0ef-464b-9670-23a8ca842631"

- Ver datos de la suscripcion
aws sns get-subscription-attributes --endpoint-url=http://localhost:4566 --subscription-arn arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa:afbb76cc-e0ef-464b-9670-23a8ca842631


6. SubscriptionArn": "arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa:160eccac-16b9-465e-832c-050902f2c851"

- Ver datos de la suscripcion
aws sns get-subscription-attributes --endpoint-url=http://localhost:4566 --subscription-arn arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa:160eccac-16b9-465e-832c-050902f2c851




FILTER POLICY

aws sns set-subscription-attributes --endpoint-url=http://localhost:4566 --subscription-arn arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa:f37e9ebf-5cd7-4d2f-bae0-c87af9da8f74 --attribute-name FilterPolicy --attribute-value '{"event":["executeMechanism"]}'

aws sns set-subscription-attributes --endpoint-url=http://localhost:4566 --subscription-arn arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa:e425a13f-d0df-47f1-b1fd-87332504922b --attribute-name FilterPolicy --attribute-value '{"event":["sendResponse"]}'

aws sns set-subscription-attributes --endpoint-url=http://localhost:4566 --subscription-arn arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa:ac84eed5-17ef-42e8-97a1-c2d3eda44815 --attribute-name FilterPolicy --attribute-value '{"event":["requestCompleteness"]}'

aws sns set-subscription-attributes --endpoint-url=http://localhost:4566 --subscription-arn arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa:cc3d4f46-b625-4d21-bbd0-48d29f47d6b2 --attribute-name FilterPolicy --attribute-value '{"event":["ruleProcess"]}'

aws sns set-subscription-attributes --endpoint-url=http://localhost:4566 --subscription-arn arn:aws:sns:us-east-2:000000000000:t-cys-cli-talos-app-qa:a8f044bc-ff62-4978-91a2-b6535cd9402e --attribute-name FilterPolicy --attribute-value '{"event":["validateMechanism"]}'




PURGAR COLAS
aws --endpoint-url=http://localhost:4566 sqs purge-queue --queue-url http://localhost:4566/queue/q-cys-cli-talos-rule-process-qa 

aws --endpoint-url=http://localhost:4566 sqs purge-queue --queue-url http://localhost:4566/queue/q-cys-cli-talos-validate-mechanism-qa 

aws --endpoint-url=http://localhost:4566 sqs purge-queue --queue-url http://localhost:4566/queue/q-talos-validate-qa

aws --endpoint-url=http://localhost:4566 sqs purge-queue --queue-url http://localhost:4566/queue/q-cys-cli-talos-execute-mechanism-qa 

aws --endpoint-url=http://localhost:4566 sqs purge-queue --queue-url http://localhost:4566/queue/q-cys-cli-talos-send-response-qa 

aws --endpoint-url=http://localhost:4566 sqs purge-queue --queue-url http://localhost:4566/queue/q-cys-cli-talos-request-completeness-qa 




VER MENSAJE COLA
aws --endpoint-url=http://localhost:4566 sqs receive-message --queue-url http://localhost:4566/queue/q-cys-cli-talos-execute-mechanism-qa 

aws --endpoint-url=http://localhost:4566 sqs receive-message --queue-url http://localhost:4566/000000000000q-cys-cli-talos-request-completeness-qa --region us-east-2 --output json