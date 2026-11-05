# Домашнее задание к занятию «Хранение в K8s»

## Задание 1. Volume: обмен данными между контейнерами в поде

**Задача**

Создать Deployment приложения, состоящего из двух контейнеров, обменивающихся данными.

**Решение**

[containers-data-exchange](containers-data-exchange.yaml)

![task1](screenshots/task1.png)

[kubectl_describe_pods_data-exchange](kubectl_describe_pods_data-exchange.txt)

## Задание 2. PV, PVC

**Задача**

Создать Deployment приложения, использующего локальный PV, созданный вручную.

**Решение**

Создать PV и PVC для подключения папки на локальной ноде, которая будет использована в поде.

[pv-pvc](pv-pvc.yaml)

![task2_1](screenshots/task2_1.png)

Продемонстрировать, что контейнер multitool может читать данные из файла в смонтированной директории, в который busybox записывает данные каждые 5 секунд.

![task2_2](screenshots/task2_2.png)

![task2_3](screenshots/task2_3.png)

Удалить Deployment и PVC. Продемонстрировать, что после этого произошло с PV. Пояснить, почему. (Используйте команду kubectl describe pv).

![task2_4](screenshots/task2_4.png)

Установлена политика `Reclaim Policy: Retain` это означает, что при удалении PVC кластер не удаляет PersistentVolume и данные на нём — том переходит в фазу Released. 

Продемонстрировать, что файл сохранился на локальном диске ноды. Удалить PV. Продемонстрировать, что произошло с файлом после удаления PV. Пояснить, почему.

![task2_5](screenshots/task2_5.png)

![task2_6](screenshots/task2_6.png)

Файл сохранился, потому что удаление PV — это удаление только объекта в etcd (API кластера). Директория hostPath — обычная папка на диске ноды, и политика Retain не предусматривает никакой очистки данных: всё остаётся до ручного вмешательства.

## Задание 3. StorageClass

Создать Deployment приложения, использующего PVC, созданный на основе StorageClass.

**Решение**

[sc](sc.yaml)

![task3_1](screenshots/task3_1.png)

![task3_2](screenshots/task3_2.png)

![task3_3](screenshots/task3_3.png)