## Описание проекта

Этот проект содержит руководство по выполнению практического задания, связанного с развертыванием Minikube и работой с манифестами Kubernetes. В ходе выполнения задания вы научитесь развертывать Minikube, работать с pod манифестами и управлять pod'ами с помощью командной строки `kubectl`.

## Требования

- Рабочий компьютер или виртуальная машина с установленной операционной системой Linux, macOS или Windows.
- Установленный [Minikube](https://minikube.sigs.k8s.io/docs/start/).
- Установленный [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

## Шаги выполнения

### 1. Развертывание Minikube

1. Установите Minikube, следуя [официальной инструкции](https://minikube.sigs.k8s.io/docs/start/).
2. Запустите Minikube с помощью команды:

   ```sh
   minikube start
   ```

### 2. Создание pod.yaml файла

1. Создайте файл `pod.yaml` и скопируйте в него следующий манифест:

   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: my-nginx
   spec:
     containers:
     - name: nginx-container
       image: nginx:1.10
   ```

2. Попробуйте создать pod из этого манифеста с помощью команды:

   ```sh
   kubectl create -f pod.yaml
   ```

3. Если `kubectl` не может применить yaml-файл, проверьте структуру файла на наличие ошибок.

### 3. Запуск pod'а redis

1. Запустите pod redis в кластере с помощью команды:

   ```sh
   kubectl run redis --image=redis:5.0 -n default
   ```

2. Проверьте, что redis запустился и находится в статусе Running:

   ```sh
   kubectl get pods -n default
   ```

3. Удостоверьтесь, что версия docker image — redis:5.0:

   ```sh
   kubectl get pod redis -n default -o jsonpath="{..image}"
   ```

4. Отредактируйте pod redis, чтобы версия docker image стала redis:6.0:

   ```sh
   kubectl edit pod redis -n default
   ```

   Примечание: вы можете изменить текстовый редактор, используемый командой `kubectl edit` по умолчанию, с помощью переменной окружения `KUBE_EDITOR` — например:

   ```sh
   export KUBE_EDITOR=nano
   ```

   или

   ```sh
   export KUBE_EDITOR=vim
   ```

5. Сохраните изменения и проверьте логи контейнера:

   ```sh
   kubectl logs redis -n default
   ```

