Ansible을 공부하면서 NFS 서버 및 클라이언트를 구성하는 playbook sample code를 작성한다.

```
# nfs-ansible-playbook.yaml


---
- name: nfs server setup
  hosts: server
  gather_facts: no
  become: yes
  
  tasks:
    - name: make directory (nfs_shared)
      file:
        path: /home/vagrant/nfs_shared
        state: directory
        mode: 0777
        
    - name: /etc/exports configuration
      lineinfile:
        path: /etc/exports
        line: /home/vagrant/nfs_shared xxx.xxx.xxx.xxx/24(rw,sync)
        # client IP 대역 작성
    
    - name: nfs service restart
      service:
        name: nfs
        state: restarted
    


- name: nfs client setup
  hosts: client
  gather_facts: no
  become: yes
  
  tasks:
    - name: make directory_nfs
      file:
        path: /home/vagrant/nfs
        state: directory
        
    - name: make mountpoint
      mount:
        path: /home/vagrant/nfs
        src: xxx.xxx.xxx.xxx:/home/vagrant/nfs_shared
        # 소스 IP 작성
        fstype: nfs
        state: mounted
  
```
