# Императивный подход

```bash
kubectl create deployment first-deployment  --image=alex501020/lesson1:v0.3
```

```bash
kubectl apply -f deployment.yaml

kubectl get deployments

k get pod

k edit -f deployment.yaml
```

```txt
$ kubectl get deployments
NAME                     READY   UP-TO-DATE   AVAILABLE   AGE
declarative-deployment   1/1     1            1           2m34s
first-deployment         1/1     1            1           5m22s
$ kubectl get pod
NAME                                     READY   STATUS    RESTARTS       AGE
declarative-deployment-85c787c88-cqd9t   1/1     Running   0              2m4s
first-deployment-785b5cd868-6fh5n        1/1     Running   1 (5m3s ago)   5m25s
```

## Команды kubectl

Смена кластеров

Работа в нашем курсе идет с одним кластером Кубернетес, однако в реальных условиях кластеров будет несколько, для переключения между ними используйте команды:

```bash
kubectl config get-contexts                          # показать список контекстов
kubectl config current-context                       # показать текущий контекст (current-context)
kubectl config use-context my-cluster-name           # установить my-cluster-name как контекст по умолчанию
```

Создание объектов

```bash
kubectl apply -f ./my-manifest.yaml            # создать объект из файла
kubectl create deployment nginx --image=nginx  # запустить один экземпляр nginx
```

Просмотр информации

```bash
kubectl get pods -o wide                      # Вывести все поды и показать, на каких они нодах
kubectl describe pods my-pod                  # Просмотреть информацию о поде такую как время                                                                 # старта, количество и причины рестартов, QoS-класс и прочее
kubectl logs -f my-pod                        # Просмотр логов в режиме реального времени
kubectl top pods                              # Вывести информацию об утилизации ресурсов подами
```

Изменение объектов

```bash
kubectl edit pod my-pod                       # Изменение .yaml манифеста пода
```

Удаление объектов

```bash
kubectl delete pod my-pod                       # Удаление пода
```

Погружение в командную оболочку Пода (проваливаемся вовнутрь)

```bash
kubectl exec -it -n namespace-name podname sh   # На конце выбираем оболочку, если нет sh, ставим bash
```

Копируем файл в под

```bash
kubectl cp {{namespace}}/{{podname}}:path/to/directory /local/path  # Копирование файла из Пода
kubectl cp /local/path namespace/podname:path/to/directory          # Копирования файла в Под
```

Проброс портов

```bash
kubectl port-forward pods/mongo-75f59d57f4-4nd6q 28015:27017  # Проброс порта Пода
kubectl port-forward mongo-75f59d57f4-4nd6q 28015:27017       # Проброс порта Сервиса
```