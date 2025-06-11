# Concept:
Порівняльний аналіз інструментів для
розгортання Kubernetes кластерів в локальному середовищі

#Minikube  #Kind  #k3d  #MicroK8s  #k3s  #RancherDesktop

### Вступ

Для локального розгортання Kubernetes-кластеру існує кілька популярних інструментів,
які дозволяють швидко створити середовище для розробки, тестування та демонстрації роботи застосунків.

Основні інструменти, які були розглянуті:

1. ***Minikube***:

        офіційний проєкт CNCF для локального запуску Kubernetes.
        Найбільш популярний інструмент для локального запуску повноцінного (однонодового) Kubernetes-кластера.
        Працює з VirtualBox, Docker, Hyper-V тощо. Має вбудовані аддони.
        Підходить для навчання, тестування та розробки.

2. ***Kind*** (Kubernetes IN Docker):

        дозволяє запускати Kubernetes-кластери у Docker контейнерах.
        Дуже легкий та швидкий. Часто використовується для CI/CD, автоматизованих тестів (інтеграційного тестування).

3. ***k3s***:

        полегшена версія Kubernetes від Rancher (~100MB),
        проста у розгортанні. Підходить для вбудованих пристроїв, IoT, edge-розгортань,
        low-resource пристроях, а також для розробки.

4. ***k3d***:

        легкий wrapper над k3s, для запуску lightweight Kubernetes в Docker-контейнерах.
        Дуже швидкий і легкий для локального девелопменту, multi-node підтримка.
        Підходить для розробки і тестування.

5. ***k0s***:

        zero-friction Kubernetes дистрибутив від Mirantis.
        Все-в-одному, бінарник Kubernetes без зовнішніх залежностей.
        Працює без root-доступу. Оптимізований для хмар і edge.


6. ***MicroK8s***:

        lightweight Kubernetes від Canonical з підтримкою додаткових модулів (add-ons).
        Snap-пакет із ядром Kubernetes від Canonical, простий в установці.
        Працює як одиночний вузол, але може масштабуватись.
        Має ізоляцію, аддони, кластеризацію, працює навіть на Raspberry Pi.

7. ***Docker Desktop (з Kubernetes)***:

        має опцію вбудованого Kubernetes. Проста активація, але споживає багато ресурсів.
        Працює на macOS та Windows.

8. ***Rancher Desktop***:

        open-source альтернатива Docker Desktop, GUI-додаток для розробників.
        Підтримка Kubernetes (k3s), containerd/moby, nerdctl.
        Кросплатформений. Має простий інтерфейс і налаштування.

9. ***Vagrant + kubeadm***:

        ручне розгортання Kubernetes на віртуальних машинах через Vagrant.
        Гнучкий та схожий на продакшн, але складний у налаштуванні.

10. ***CRC (CodeReady Containers)***:

        локальний кластер OpenShift (на базі Kubernetes) від Red Hat. Підходить для ознайомлення з OpenShift.

### Характеристики
#### Порівняльна таблиця характеристик

|    |                   |                           | x86_64(amd64) | ARM64 (aarch64) | ARMv7 (32-bit ARM) |

|    | Tool              | OS                        |       | Architecture |     |
| -- | ----------------- | ------------------------- | ----- | ---------- | ----- |
|    |                   |                           | amd64 | arm64      | armv7 |
| 1  | Minikube          | Linux/macOS/Win           | Yes   | Yes(part.) | No    |
| 2  | Kind              | Linux/macOS/Win           | Yes   | Yes        | No    | 
| 3  | k3s               | Linux/macOS               | Yes   | Yes        | Yes   |
| 4  | k3d               | Linux/macOS/Win           | Yes   | Yes        | No    |
| 5  | k0s               | Linux/macOS/Win           | Yes   | Yes        | Yes   |
| 6  | MicroK8s          | Linux/macOS/Win           | Yes   | Yes        | No    |
| 7  | Docker Desktop    | Linux/macOS/Win           | Yes   | Yes(M1/M2  | No    |
| 8  | Rancher Desktop   | Linux/macOS/Win           | Yes   | Yes        | No    |
| 9  | Vagrant + kubeadm | Linux/macOS/Win           | Yes   | Yes        | No    |
| 10 | CRC               | Linux/macOS/Win           | Yes   | No         | No    |

        
