## Развертывание с помощью Helm

Helm упрощает развертывание и управление приложениями в Kubernetes, используя шаблоны и чарты. Для развертывания
приложения Momo Store с помощью Helm следуйте этим шагам:

1. **Настройка Helm**:
    - Убедитесь, что Helm установлен и настроен. Если Helm не установлен, следуйте инструкциям
      из [документации Helm](https://helm.sh/docs/intro/install/).

2. **Добавление репозитория Helm**:
    - Добавьте репозиторий Helm, где хранятся чарты вашего приложения:
      ```bash
      helm repo add momo-store https://nexus.example.com/repository/helm-charts/
      helm repo update
      ```

3. **Установка приложения с помощью Helm**:
    - Установите чарт для развертывания приложения Momo Store. Убедитесь, что вы используете правильный чарт и версию:
      ```bash
      helm install momo-store momo-store/momo-store-chart --namespace <namespace> --create-namespace
      ```
      Замените `<namespace>` на нужный вам namespace в Kubernetes.

4. **Обновление релиза Helm**:
    - Если вам нужно обновить развертывание, используйте команду `helm upgrade`:
      ```bash
      helm upgrade momo-store momo-store/momo-store-chart --namespace <namespace>
      ```

5. **Удаление релиза Helm**:
    - Для удаления развертывания используйте команду `helm uninstall`:
      ```bash
      helm uninstall momo-store --namespace <namespace>
      ```

6. **Проверка развертывания**:
    - Убедитесь, что все ресурсы развернуты успешно и приложение функционирует корректно. Проверьте статус релиза с
      помощью команды:
      ```bash
      helm status momo-store --namespace <namespace>
      ```