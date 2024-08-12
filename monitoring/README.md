# Мониторинг

### 1. Установка Prometheus с помощью Helm

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus prometheus-community/prometheus
```

### 2. Установка Grafana с помощью Helm

Используем официальный Helm chart для установки Grafana.

```bash
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
helm install grafana grafana/grafana
```

### 3. Установка Loki с помощью Helm

Для установки Loki также используем Helm chart.

```bash
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
helm install loki grafana/loki-stack
```

### 4. Настройка Grafana для работы с Prometheus и Loki

После установки необходимо настроить Grafana для использования Prometheus и Loki в качестве источников данных.

#### Получение пароля для Grafana:

```bash
kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```

#### Доступ к Grafana:

Запустите порт-форвардинг, чтобы получить доступ к интерфейсу Grafana:

```bash
kubectl port-forward service/grafana 3000:80
```

Откройте браузер и перейдите по адресу `http://localhost:3000`. Войдите в систему, используя имя пользователя `admin` и
пароль, который вы получили ранее.

#### Добавление источников данных в Grafana:

1. Зайдите в интерфейс Grafana.
2. Перейдите в `Configuration` -> `Data Sources`.
3. Нажмите `Add data source`.
4. Добавьте Prometheus, указав URL `http://prometheus-server`.

Повторите процесс для Loki, указав URL `http://loki:3100`.

### 6. Проверка работы

Теперь все компоненты должны быть развернуты и настроены. Вы можете создавать дашборды в Grafana, чтобы визуализировать
метрики и логи из Prometheus и Loki.

### Дополнительно

Если вам требуется кастомизация конфигураций или дополнительные настройки, обратитесь к официальной документации Helm
charts:

- [Prometheus Helm Chart](https://github.com/prometheus-community/helm-charts/tree/main/charts/prometheus)
- [Grafana Helm Chart](https://github.com/grafana/helm-charts/tree/main/charts/grafana)
- [Loki Helm Chart](https://github.com/grafana/helm-charts/tree/main/charts/loki)