# otus-sa-hw2
Helm-chart для разворачивания demo-сервиса. Имеет в зафисимостях postgres chart из bitnami repo. 
Java-сервис с sql-миграциями на Flyway, поэтому время старта заложено в 2 минуты. 

## Обновление зависимостей
```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
helm dependencies update ./otus-demo-chart/
```

## Старт приложения
```helm install otus-demo ./otus-demo-chart -f values/values.yaml```

## Тест
```curl http://arch.homework/otusapp/vtimoshenko/health```
 
## Api-тесты из Postman 
Хост в user_api_postman_collection.json указан как arch.homework  

```newman run tests/user_api_postman_collection.json```

  
## Проблемы 

### Ingress
При старте выдает следующую ошибку:
```
Error: Internal error occurred: failed calling webhook "validate.nginx.ingress.kubernetes.io": an error on the server ("") has prevented the request from succeeding
```
Как легкое решение:
```
kubectl delete -A ValidatingWebhookConfiguration ingress-nginx-admission

```
