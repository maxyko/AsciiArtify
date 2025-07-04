# Concept:
Порівняльний аналіз інструментів для
розгортання Kubernetes кластерів в локальному середовищі


## Вступ:

Для локального розгортання Kubernetes-кластеру існує цілий набір інструментів,
які дозволяють швидко створити середовище для розробки, тестування та демонстрації (POC) роботи застосунків.

Основні інструменти, які були розглянуті:

1. 🟩 ***Minikube***:

        офіційний проєкт CNCF для локального запуску Kubernetes.
        Найбільш популярний інструмент для локального запуску повноцінного (однонодового) Kubernetes-кластера.
        Працює з VirtualBox, Docker, Hyper-V тощо. Має вбудовані аддони.
        Підходить для навчання, тестування та розробки.

2. 🟩 ***Kind*** (Kubernetes IN Docker):

        дозволяє запускати Kubernetes-кластери у Docker контейнерах.
        Дуже легкий та швидкий. Часто використовується для CI/CD, автоматизованих тестів (інтеграційного тестування).

3. 🟩 ***k3s***:

        полегшена версія Kubernetes від Rancher (~100MB),
        проста у розгортанні. Підходить для вбудованих пристроїв, IoT, edge-розгортань,
        low-resource пристроях, а також для розробки.

4. 🟩 ***k3d***:

        легкий wrapper над k3s, для запуску lightweight Kubernetes в Docker-контейнерах.
        Дуже швидкий і легкий для локального девелопменту, multi-node підтримка.
        Підходить для розробки і тестування.

5. 🟩 ***k0s***:

        zero-friction Kubernetes дистрибутив від Mirantis.
        Все-в-одному, бінарник Kubernetes без зовнішніх залежностей.
        Працює без root-доступу. Оптимізований для хмар і edge.


6. 🟩 ***MicroK8s***:

        lightweight Kubernetes від Canonical з підтримкою додаткових модулів (add-ons).
        Snap-пакет із ядром Kubernetes від Canonical, простий в установці.
        Працює як одиночний вузол, але може масштабуватись.
        Має ізоляцію, аддони, кластеризацію, працює навіть на Raspberry Pi.

7. 🟩 ***Docker Desktop (з Kubernetes)***:

        має опцію вбудованого Kubernetes. Проста активація, але споживає багато ресурсів.
        Працює на macOS та Windows.

8. 🟩 ***Rancher Desktop***:

        open-source альтернатива Docker Desktop, GUI-додаток для розробників.
        Підтримка Kubernetes (k3s), containerd/moby, nerdctl.
        Кросплатформений. Має простий інтерфейс і налаштування.

9. 🟩 ***Vagrant + kubeadm***:

        ручне розгортання Kubernetes на віртуальних машинах через Vagrant.
        Гнучкий та схожий на продакшн, але складний у налаштуванні.

10. 🟩 ***CRC (CodeReady Containers)***:

        локальний кластер OpenShift (на базі Kubernetes) від Red Hat. Підходить для ознайомлення з OpenShift.


## Характеристики:
### Порівняльна таблиця характеристик


|  |Tool             |OS             |Architecture amd64/arm64/armv7|Automation CI/CD|Built-in applications       |need Docker                                            |Podman support|Usability |Production ready  |
|--|-----------------|---------------|------------------------------|----------------|----------------------------|------------------------------------------------------------------|---|----------|------------------|
|1 |Minikube         |Linux/macOS/Win|Yes/Yes(lim.)/No              |Limited         |Yes(Ingress, Dashboard)     |❌ Підтримує Docker,Podman,VirtualBox,KVM,HyperKit,etc.         |✅ Працює  з  '--driver=podman'. Деякі аддони можуть працювати нестабільно.|⭐⭐⭐⭐☆ |No                |
|2 |Kind             |Linux/macOS/Win|Yes/Yes/No                    |Yes             |No                          |✅ Потрібен Docker або Podman як backend (з певними обмеженнями)|⚠️ Частково   Може працювати з rootful Podman, але не стабільно; rootless – не підтримується.|⭐⭐⭐☆☆  |No                |
|3 |k3s              |Linux/macOS    |Yes/Yes/Yes                   |Yes             |Yes(Traefik, Helm CRD)      |❌ Має вбудований containerd, Docker не потрібен                |✅ Працює з будь-яким CRI. Для створення контейнерів можна використовувати Podman окремо.|⭐⭐⭐⭐☆ |Yes(edge)         |
|4 |k3d              |Linux/macOS/Win|Yes/Yes/No                    |Yes             |Yes(Traefik, opt. UI)       |✅ Працює виключно з Docker, бо запускає k3s у контейнерах      |❌ Ні. Використовує Docker socket API напряму — Podman не сумісний. |⭐⭐⭐⭐⭐|No(only dev/test) |
|5 |k0s              |Linux/macOS/Win|Yes/Yes/Yes                   |Yes             |No                          |❌ Має вбудований containerd, працює без Docker                 |✅ Контейнери створюються через вбудований containerd. Podman не потрібен, але сумісний з образом.|⭐⭐⭐☆☆  |Yes               |
|6 |MicroK8s         |Linux/macOS/Win|Yes/Yes/No                    |Yes             |Yes(Ingress,Dashboard,Istio)|❌ Вбудований containerd, Docker не потрібен                    |✅ Має власний containerd. Podman можна використовувати для побудови образів.|⭐⭐⭐⭐☆ |Yes               |
|7 |Docker Desktop   |Linux/macOS/Win|Yes/Yes(M1/M2)/No             |Limited         |Yes(Dashboard)              |✅ Має Docker + Kubernetes. Інше не підтримується               |❌ Це і є Docker. Podman не релевантний.|⭐⭐⭐⭐☆ |No                |
|8 |Rancher Desktop  |Linux/macOS/Win|Yes/Yes/No                    |Yes             |Yes(Ingress)                |❌ Має вбудований containerd або може працювати з nerdctl (Docker CLI-альтернатива)|✅ (опосередковано) Має підтримку nerdctl, який може замінити Docker CLI. Можна налаштувати на Podman, але складно.|⭐⭐⭐⭐☆ |No                |
|9 |Vagrant + kubeadm|Linux/macOS/Win|Yes/Yes/No                    |Yes             |N/A                         |❌ Використовує внутрішній CRI (можна встановити Docker, containerd або CRI-O вручну)|✅ Залежить від того, який CRI ти ставиш всередині (можна використовувати Podman).|⭐⭐☆☆☆   |Yes               |
|10|CRC              |Linux/macOS/Win|Yes/No/No                     |Limited         |Yes(Web UI,Ingress)         |❌ Вбудований CRI-O. Docker заборонено в OpenShift за замовчуванням|✅ (опосередковано) Використовує CRI-O. Образи можна створювати з Podman. Працює добре.|⭐⭐☆☆☆   |Limited(only eval)|


## Переваги та недоліки:

1. 🟩 Minikube

    Переваги:
    - Працює на всіх ОС
    - Підтримує багато драйверів (Docker, VirtualBox, KVM, etc.)
    - Має аддони: Ingress, Dashboard, Metrics Server
    - Проста CLI

    Недоліки:
    - Однонодовий за замовчуванням
    - Споживає більше ресурсів
    - Не підходить для продакшн

2. 🟩 Kind

    Переваги:
    - Дуже легкий і швидкий
    - Ідеальний для CI/CD
    - Підтримка multi-node
    - Повністю Kubernetes-стандарт (на базі kubeadm)

    Недоліки:
    - Немає UI або Ingress із коробки
    - Docker-залежність
    - Складніший нетворкінг у деяких сценаріях

3. 🟩 k3s

    Переваги:
    - Легка вага (~100MB)
    - Простий запуск (1 бінарник)
    - Вбудований Helm CRD, Traefik
    - Підходить для edge, ARM-пристроїв

    Недоліки:
    - Менш гнучкий у порівнянні з kubeadm
    - Потрібна додаткова робота для розширення функціоналу
    - Офіційно тільки для Linux

4. 🟩 k3d

    Переваги:
    - k3s-кластер у Docker — швидкий старт
    - Multi-node, простий CLI
    - Чудовий для dev та CI/CD
    - Вбудована інтеграція з Traefik

    Недоліки:
    - Потребує Docker
    - Не підходить для продакшн
    - Обмежена мережна гнучкість (порівняно з реальними кластерами)

5. 🟩 k0s

    Переваги:
    - Один бінарник, без залежностей
    - Без root-доступу (опціонально)
    - Підходить для edge/продакшн
    - Multi-node, підтримка HA

    Недоліки:
    - Менш популярний, менше спільноти
    - Потрібна ручна настройка аддонів
    - Відсутній UI "із коробки"

6. 🟩 MicroK8s

    Переваги:
    - Простий snap-інсталятор
    - Вбудовані аддони (Ingress, Istio, Prometheus, Knative)
    - Підтримує кластеризацію
    - ARM-сумісність

    Недоліки:
    - Офіційно лише Linux (інші ОС — з workarounds)
    - Важче дебажити
    - Більш "замкнута" архітектура

7. 🟩 Docker Desktop (з Kubernetes)

    Переваги:
    - Вбудовано в Docker Desktop
    - Простий GUI
    - Підтримка Windows/macOS

    Недоліки:
    - Дуже 'важкий'
    - Високе споживання ресурсів
    - Лише однонодовий кластер

8. 🟩 Rancher Desktop

    Переваги:
    - Альтернатива Docker Desktop
    - Вбудований Kubernetes (k3s), UI
    - Підтримка containerd, nerdctl, Podman
    - Кросплатформений

    Недоліки:
    - Молодий проєкт — ще не стабільний на 100%
    - Немає multi-node
    - Обмежений контроль над конфігурацією

9. 🟩 Vagrant + kubeadm

    Переваги:
    - Найбільш близький до продакшн-сценаріїв
    - Повний контроль над кластерами
    - Сумісний із Helm, monitoring, etc.

    Недоліки:
    - Ручна конфігурація
    - Повільний запуск
    - Велика 'вага' (VM), ресурсоємний

10. 🟩 CRC (CodeReady Containers)

    Переваги:
    - Повноцінний OpenShift у локальному середовищі
    - Має web UI, operator framework
    - Придатний для навчання OpenShift

    Недоліки:
    - Важкий, запускається повільно
    - Високі системні вимоги
    - Тільки для ознайомлення, не продакшн


## Демонстрація:

Рекомендований вибір: ***k3d***

Він ідеально підходить для PoC стартапу AsciiArtify, де важлива швидкість, легкість та простота автоматизації.
За потреби можна інтегрувати його у CI/CD pipeline або легко перенести розгортання у повноцінне хмарне середовище.

![Image](../.data/week4_task4.gif)

1. Встановлення ***k3d***
```
curl -s https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash
```

2. Створення кластеру
```
k3d cluster create hello-cluster
```

3. Деплой
```
kubectl apply -f hello-deploy.yaml
```
```
kubectl apply -f  hello-service.yaml
```
**hello-deploy.yaml**
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: hello
  template:
    metadata:
      labels:
        app: hello
    spec:
      containers:
      - name: hello-container
        image: hashicorp/http-echo
        args:
        - "-text=Hello, World!"
        ports:
        - containerPort: 5678
```

**hello-service.yaml**
```
apiVersion: v1
kind: Service
metadata:
  name: hello-service
spec:
  type: ClusterIP
  selector:
    app: hello
  ports:
    - protocol: TCP
      port: 80
      targetPort: 5678
```

4. Port-forwaring
```
kubectl port-forward svc/hello-service 8080:80 &
```

5. Перевірка
```
curl 127.0.0.1:8080
```
```
kubectl logs -f $(kubectl get pods -l app=hello -o name)
```

6. Видалити кластер
```
k3d cluster delete hello-cluster
```

### Додаток

#### Minikube
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
chmod +x minikube && sudo mv minikube /usr/local/bin
minikube start
...
minikube delete
```

#### Kind
```
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.23.0/kind-linux-amd64
chmod +x kind && sudo mv kind /usr/local/bin
kind create cluster --name asciiartify
...
kind delete cluster --name asciiartify
```

## Висновки:

PoC у стартапі зазвичай:
- потребує швидкого результату,
- обмежений у ресурсах (ноутбук/один сервер),
- повинен мати інфраструктуру, схожу на продакшн, хоча б частково,
- має інтегруватись у CI/CD,
- потребує мінімального технічного боргу.

Тому для POC рекомендується використовувати ***k3d*** так, як він забезпечує: миттєвий запуск, мінімум конфігурації,
відмінний для розробки, тестів, CI :


| Інструмент            | Використання в PoC | Рекомендація                                                                                                               |
| --------------------- | ------------------ | -------------------------------------------------------------------------------------------------------------------------- |
| **k3d**               | ⭐⭐⭐⭐⭐              | **Топ-вибір**: миттєвий запуск, мінімум конфігурації, відмінний для розробки, тестів, CI. Дуже підходить для стартапів.    |
| **Kind**              | ⭐⭐⭐⭐☆              | Ідеальний для CI/CD і PoC без UI. Якщо потрібен контроль через YAML і легкий перенос у кластер — чудовий вибір.            |
| **k3s**               | ⭐⭐⭐⭐☆              | Добре підходить для більш “серйозного” PoC — якщо потрібен ближчий до продакшн-режиму кластер (на сервері, edge).          |
| **MicroK8s**          | ⭐⭐⭐⭐☆              | Зручний локально, має аддони (Ingress, Istio), швидкий старт. Але важче інтегрувати в CI/CD. Підійде для desktop-розробки. |
| **Minikube**          | ⭐⭐⭐☆☆              | Старий добрий варіант, стабільний і надійний, але дещо громіздкий. Добре як локальний PoC, не для CI.                      |
| **Rancher Desktop**   | ⭐⭐⭐☆☆              | Гарний UX для новачків, GUI, Kubernetes + nerdctl. Якщо команда не має DevOps — може стати рятівником.                     |
| **Docker Desktop**    | ⭐⭐☆☆☆              | Мінімальна конфігурація, але обмежений і важкий. Рекомендовано лише якщо вже встановлений.                                 |
| **k0s**               | ⭐⭐☆☆☆              | Потужний, але потребує ручного налаштування. Підійде для PoC, що ближче до edge або продакшн.                              |
| **Vagrant + kubeadm** | ⭐☆☆☆☆              | Максимальний контроль, але складно і повільно. Не рекомендується для стартапів, хіба що для навчання DevOps.               |
| **CRC (OpenShift)**   | ⭐☆☆☆☆              | Дуже важкий. Варто використовувати лише якщо ціль — OpenShift. Для звичайного PoC — ні.                                    |

