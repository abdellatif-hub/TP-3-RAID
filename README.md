# 📄 Rapport TP : Mise en place d'un RAID 1 logiciel sous ubuntu

## ✅ Introduction

Dans ce travail pratique, nous avons mis en place un système RAID 1 logiciel sur une machine virtuelle Linux afin d'assurer la tolérance aux pannes et garantir la continuité de fonctionnement même en cas de défaillance d'un disque.

Le but principal est de comprendre le fonctionnement du RAID logiciel, sa configuration, ainsi que le comportement du système lors d'une panne simulée.

---

## 🎯 Objectif du TP

* Mettre en place un RAID 1 logiciel sous ubuntu
* Ajouter et configurer deux disques virtuels
* Créer un RAID 1 avec `mdadm`
* Vérifier son fonctionnement
* Simuler une panne d'un disque
* Observer la tolérance aux pannes
* Reconstruire le RAID

---

## 🛠️ Matériel et environnement

* VirtualBox
* Ubuntu
* 1 disque système
* 2 disques virtuels de 1 Go chacun
* Outil `mdadm`

---

## ✅ Étapes de réalisation

### 🔹 Ajout des disques virtuels

Deux disques virtuels de 1 Go ont été ajoutés à la machine virtuelle.

<img width="1602" height="930" alt="image" src="https://github.com/user-attachments/assets/f71d57b1-bd5e-45c8-af8f-62ccda7f5385" />


---

### 🔹 Vérification des disques

Commande exécutée :

```
sudo fdisk -l
```

<img width="1251" height="1021" alt="image" src="https://github.com/user-attachments/assets/246eb33c-e0b5-4211-9770-810a40aebeff" />


---

### 🔹 Partitionnement des disques

Chaque disque a reçu une partition de type RAID (fd) via `fdisk`.

<img width="1150" height="652" alt="image" src="https://github.com/user-attachments/assets/ffad55d9-8eaa-4f2e-9e57-acf6e6c91dac" />


---

### 🔹 Création du RAID 1

Commande utilisée :

```
sudo mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdb1 /dev/sdc1
```

<img width="1202" height="204" alt="image" src="https://github.com/user-attachments/assets/0adea245-3a07-4502-b0b1-a7fcc010ad87" />


---

### 🔹 Formatage et montage du RAID

```
sudo mkfs.ext4 /dev/md0
sudo mkdir /mnt/raid1
sudo mount /dev/md0 /mnt/raid1
```

<img width="1255" height="309" alt="image" src="https://github.com/user-attachments/assets/05d4cbf5-83c6-4e15-9f97-7533b8065df3" />


---

### 🔹 Test de panne

Panne simulée :

```
sudo mdadm --fail /dev/md0 /dev/sdb1
sudo mdadm --remove /dev/md0 /dev/sdb1
```

<img width="1260" height="90" alt="image" src="https://github.com/user-attachments/assets/8a54d13a-bcb0-40d9-a201-817b997033fe" />


---

### 🔹 Reconstruction du RAID

```
sudo mdadm --add /dev/md0 /dev/sdb1
```

<img width="1265" height="184" alt="image" src="https://github.com/user-attachments/assets/fa9a692b-c3ca-4602-988d-a31a6b9d22cd" />


---

## ✅ Conclusion

Ce TP nous a permis d'apprendre à configurer un RAID 1 logiciel sous Linux, d'observer son comportement lors d'une panne et de constater sa capacité à se reconstruire automatiquement.

Le système a continué à fonctionner même après la défaillance simulée d'un disque, démontrant la tolérance aux pannes du RAID 1.

---

## 📁 Fichiers de configuration importants

```
/etc/mdadm/mdadm.conf
```

---

## ✅ Résultat final

✅ RAID 1 opérationnel
✅ Données protégées
✅ Reconstruction réussie
✅ TP terminé avec succès

