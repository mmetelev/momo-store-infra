## Развертывание с помощью Kubernetes

Директория `kubernetes` в репозитории содержит все необходимые манифесты для развертывания приложения Momo Store.
Следуйте этим шагам для успешного развертывания приложения в Kubernetes:

1. **Обновление Ingress и доменного имени**:
    - Убедитесь, что ваши Ingress ресурсы настроены правильно и доменное имя указывает на ваш Ingress Controller.

2. **Применение манифестов Kubernetes**:
    - Примените манифесты Kubernetes для развертывания приложения с помощью команды `kubectl`. Используйте следующие
      команды для применения манифестов:
      ```bash
      kubectl apply -f /kubernetes
      kubectl apply -f /kubernetes/backend
      kubectl apply -f /kubernetes/frontend
      ```

3. **Проверка развертывания**:
    - Убедитесь, что все ресурсы развернуты успешно и приложение функционирует корректно. Для диагностики возможных
      проблем проверьте логи и описание ресурсов в Kubernetes с помощью следующих команд:
      ```bash
      kubectl get pods
      kubectl logs <pod-name>
      kubectl describe <resource-type> <resource-name>
      ```
