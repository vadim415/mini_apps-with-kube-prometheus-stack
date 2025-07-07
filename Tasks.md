### Цель

Развернуть локальный Kubernetes-кластер в Minikube, задеплоить готовое приложение с Ingress, мониторингом и настроить CI/CD (GitHub Actions).

---

### 🔧 Что нужно сделать

#### 1. Kubernetes кластер (Minikube)

* Установи Minikube на своей машине (VirtualBox / Docker / Hyperkit — по выбору).
* Настрой кластер:

  * включи `ingress`-аддон (`minikube addons enable ingress`);
  * установи Helm;
  * подними kube-prometheus-stack через Helm.

#### 2. Приложение

* Используй готовый контейнер:
  nginxdemos/hello
  [DockerHub](https://hub.docker.com/r/nginxdemos/hello)
  Функциональность:

  * GET / → hostname, IP
  * поддерживает X-Real-IP

* Задеплой:

  * Deployment
  * Service
  * Ingress

#### 3. CI/CD

* Настрой GitHub Actions workflow:

  * запуск Minikube (на своей машине — CI может быть только для проверки деплоя);
  * деплой приложения через Helm;
  * workflow должен быть воспроизводим (документация обязательна).

> Важно: CI может не запускать Minikube, но должен имитировать полноценный деплой (`kubectl apply`, helm install, использование secrets и т.п.)

#### 4. Ingress

* Настрой Ingress-контроллер:

  * приложение должно быть доступно по адресу вида:
    http://<minikube_ip>/ (или через hosts-файл)
  * X-Real-IP должен пробрасываться внутрь приложения.

#### 5. Мониторинг

* Установи kube-prometheus-stack через Helm.
* Убедись, что приложение скрейпится Prometheus'ом:

  * Target отображается как UP
  * Метрики можно посмотреть через /metrics

#### 6. README

* Подробная инструкция:

  * Установка Minikube
  * Деплой приложения и мониторинга
  * Проверка /, /metrics, Ingress
  * Архитектурная схема (ASCII или Mermaid)

---

### Критерии оценки

| Критерий                          | Обязателен |
| --------------------------------- | ---------- |
| Minikube развёрнут                | ✅          |
| Приложение доступно через Ingress | ✅          |
| CI/CD workflow воспроизводим      | ✅          |
| Метрики видны в Prometheus        | ✅          |
| README полное и понятное          | ✅          |

---

### Инструменты

* Minikube (Docker/VirtualBox backend)
* Helm
* GitHub Actions
* Prometheus, Grafana (`kube-prometheus-stack`)
* nginxdemos/hello
