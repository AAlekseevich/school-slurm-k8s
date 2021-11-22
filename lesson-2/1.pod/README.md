# Pod

### 1. Создаем Pod

Для этого выполним команду:

```bash
kubectl apply --context mcs.slurm.io -f lesson-2/1.pod/pod.yml
```

Проверим результат, для чего выполним команду:

```bash
kubectl --context mcs.slurm.io get pod
```

Результат должен быть примерно следующим:

```bash
NAME      READY     STATUS              RESTARTS   AGE
my-pod    0/1       ContainerCreating   0          2s
```

Через какое-то время Pod должен перейти в состояние `Running`
и вывод команды `kubectl --context mcs.slurm.io get pod` станет таким:

```bash
NAME      READY     STATUS    RESTARTS   AGE
my-pod    1/1       Running   0          59s
```

### 2. Скейлим приложение

Открываем файл pod.yaml редактором и заменяем там строку:

```diff
-  name: my-pod
+  name: my-pod-1
```

Сохраняем и выходим.

Применяем изменения, для этого выполним команду:

```bash
kubectl apply --context mcs.slurm.io -f lesson-2/1.pod/pod.yml
```

Проверяем результат, для этого выполним команду:

```bash
kubectl --context mcs.slurm.io get pod
```

Результат должен быть примерно следующим:

```bash
NAME      READY     STATUS    RESTARTS   AGE
my-pod    1/1       Running   0          10m
my-pod-1  1/1       Running   0          59s
```


Посмотрим описание, для чего выполним команду:

```bash
kubectl --context mcs.slurm.io describe pod my-pod
```

### 3. Чистим за собой кластер

Для этого выполним команду:

```bash
kubectl --context mcs.slurm.io delete pod --all
```
---
Использование контекста опционально, если у Вас запущен миникуб или нет в конфиге больше кластеров, то можно его не использовать