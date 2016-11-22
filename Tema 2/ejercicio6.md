# Gestión de infraestructuras virtuales

## Ejercicio 6

### Desplegar la aplicación que se haya usado anteriormente con todos los módulos necesarios usando un playbook de Ansible.

El playbook sería:

	---
    - hosts: server
      sudo: yes
      tasks:
        - name: Update Apt cache
          apt: update_cache=yes

        - name: Install g++
          apt: pkg=g++ state=present

        - name: Install make
          apt: pkg=make state=present

        - name: Install sparsehash
          apt: pkg=libsparsehash-dev state=present

        - name: Install mysql-server
          apt: pkg=mysql-server state=present

        - name: Install libmysqlclient-dev
          apt: pkg=libmysqlclient-dev state=present

        - name: Install libmysql++-dev
          apt: pkg=libmysql++-dev state=present

        - name: Compilar código
          shell: 'cd /home/ubuntu/app/ && make && cd ~'

        - name: Ejecutar
          shell: '/home/ubuntu/app/Server /home/ubuntu/app/fingers &'

Y ejecutamos con:

    ansible-playbook ./ansible/app.yml


![Resultado de ansible](https://github.com/JPPorcel/CC-Ejercicios/blob/master/Tema%202/images/ej_6.png?raw=true)