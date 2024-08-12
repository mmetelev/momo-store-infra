# Установка сертификата для TLS (SSL) в Kubernetes с использованием Ingress

Для настройки TLS (SSL) сертификатов в Kubernetes и обеспечения безопасного соединения для ваших доменов выполните
следующие шаги:

## Шаг 1: Получение сертификатов

**Использование Let's Encrypt с Cert-Manager:**

1. **Установите `cert-manager` в ваш кластер Kubernetes.** `cert-manager` автоматизирует процесс получения и обновления
   сертификатов от Let's Encrypt. Выполните команду:

   ```bash
   kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.11.0/cert-manager.yaml
   ```

2. **Примените манифесты для `ClusterIssuer` и `Certificate`.** Убедитесь, что у вас есть созданные
   манифесты `ClusterIssuer` и `Certificate`. Примените их с помощью команд:

   ```bash
   kubectl apply -f clusterissuer.yaml
   kubectl apply -f certificate.yaml
   ```

## Шаг 2: Создание Kubernetes Secret

Если вы используете сертификаты, полученные другим способом, создайте `Secret`, упаковывая ваш сертификат и ключ:

```bash
kubectl create secret tls example-tls --cert=path/to/tls.crt --key=path/to/tls.key
```

## Шаг 3: Проверка статуса

1. **Проверьте статус сертификатов.** Убедитесь, что `cert-manager` работает и сертификаты успешно созданы:

   ```bash
   kubectl get certificates
   kubectl describe certificate example-certificate
   ```

2. **Проверьте, что Ingress правильно ссылается на Secret и сертификаты применяются корректно (если применимо):**

   ```bash
   kubectl describe ingress frontend
   ```

### ВАЖНО! Не забудьте обновить ingress.yaml