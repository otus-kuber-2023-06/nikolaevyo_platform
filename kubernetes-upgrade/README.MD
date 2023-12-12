1. Устанавливаем питон и создаём виртуальную среду
    sudo apt install git python3 python3-pip python3.10-venv -y
    python3 -m venv k8s/
    source k8s/bin/activate 
2. Клонируем репу с kubespray
   git clone https://github.com/kubernetes-sigs/kubespray.git
3. Устанавливаем зависимости
   cd kubespray
   python3 -m pip install -r requirements.txt
4. Копируем конфиги
   cp inventory/sample inventory/mycluster
5. Заполняем перечисленные файлы. ЗЫ т.к. на виртуалках авторизуемся с помощью ключа, то ансибл будет так же авторизоваться. 
   nano ./inventory/mycluster/inventory.ini
   nano ./inventory/mycluster/group_vars/k8s_cluster/addons.yml
   nano ./inventory/mycluster/group_vars/k8s_cluster/k8s-cluster.yml
6. Запускаем установку кластера 
   ansible-playbook -i ./inventory/mycluster/inventory.ini cluster.yml -b -v --private-key=~/.ssh/private_key
   Ждём ...
7. Проверяем ноды
   sudo kubectl get nodes
   NAME      STATUS   ROLES           AGE     VERSION
master1   Ready    control-plane   4m49s   v1.28.4
master2   Ready    control-plane   4m24s   v1.28.4
master3   Ready    control-plane   4m20s   v1.28.4
node1     Ready    <none>          3m34s   v1.28.4
node2     Ready    <none>          3m34s   v1.28.4
