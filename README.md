### 8.1 Введение в Ansible
#### 1. Попробуйте запустить playbook на окружении из test.yml, зафиксируйте какое значение имеет факт some_fact для указанного хоста при выполнении playbook'a.
![1](imgs/1.png)
#### 2. Найдите файл с переменными (group_vars) в котором задаётся найденное в первом пункте значение и поменяйте его на 'all default fact'.
![2](imgs/2.png)
#### 3. Воспользуйтесь подготовленным (используется docker) или создайте собственное окружение для проведения дальнейших испытаний.
docker run --name centos7 -d pycontribs/centos:7 sleep 36000000
<br>docker run --name ubuntu -d pycontribs/ubuntu sleep 65000000
#### 4. Проведите запуск playbook на окружении из prod.yml. Зафиксируйте полученные значения some_fact для каждого из managed host.
![4](imgs/4.png)
###### 5. Добавьте факты в group_vars каждой из групп хостов так, чтобы для some_fact получились следующие значения: для deb - 'deb default fact', для el - 'el default fact'.
#### 6. Повторите запуск playbook на окружении prod.yml. Убедитесь, что выдаются корректные значения для всех хостов.
![5](imgs/5.png)
#### 7. При помощи ansible-vault зашифруйте факты в group_vars/deb и group_vars/el с паролем netology.
![7](imgs/7.png)
#### 8. Запустите playbook на окружении prod.yml. При запуске ansible должен запросить у вас пароль. Убедитесь в работоспособности.
![8](imgs/8.png)
#### 9. Посмотрите при помощи ansible-doc список плагинов для подключения. Выберите подходящий для работы на control node.
 ansible-doc -t connection -l
 <br>Подойдет плагин <b>local</b>
###### 10. В prod.yml добавьте новую группу хостов с именем local, в ней разместите localhost с необходимым типом подключения.
#### 11. Запустите playbook на окружении prod.yml. При запуске ansible должен запросить у вас пароль. Убедитесь что факты some_fact для каждого из хостов определены из верных group_vars.
![11_1](imgs/11_1.png)
![11_2](imgs/11_2.png)
### Самоконтроль выполнения задания
#### 1. Где расположен файл с some_fact из второго пункта задания?
group_vars/all/examp.yml
#### 2. Какая команда нужна для запуска вашего playbook на окружении test.yml?
ansible-playbook -i inventory/test.yml site.yml
#### 3. Какой командой можно зашифровать файл?
ansible-vault encrypt group_vars/el/examp.yml
#### 4. Какой командой можно расшифровать файл?
ansible-vault decrypt group_vars/el/examp.yml
#### 5. Можно ли посмотреть содержимое зашифрованного файла без команды расшифровки файла? Если можно, то как?
ansible-vault view group_vars/el/examp.yml
#### 6. Как выглядит команда запуска playbook, если переменные зашифрованы?
ansible-playbook -i inventory/prod.yml site.yml --ask-vault-pass
#### 7. Как называется модуль подключения к host на windows?
winrm
#### 8. Приведите полный текст команды для поиска информации в документации ansible для модуля подключений ssh
ansible-doc -t connection ssh
#### 9. Какой параметр из модуля подключения ssh необходим для того, чтобы определить пользователя, под которым необходимо совершать подключение?
remote_user
