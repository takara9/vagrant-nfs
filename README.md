# vagrant-nfs

この Vagrant と Ansible のコードは、仮想サーバーに　NFSサーバーを構築して、Kuberentes クラスタのポッドからマウントして利用できるようにするものです。この仮想サーバーのIPアドレスは、仮想サーバーに割り当てられる内部通信用のIPアドレスです。

1. nfsserver 172.20.1.10

[https://github.com/takara9/vagrant-kubernetes](https://github.com/takara9/vagrant-kubernetes)や[takara9/vagrant-minikube](https://github.com/takara9/vagrant-minikube)で構築するKubernetesクラスタと組み合わせて、永続ストレージのマニュアルのプロビジョニング環境のミニチュア版を構築できます。


## このクラスタを起動するために必要なソフトウェア

このコードを利用するためには、次のソフトウェアをインストールしていなければなりません。

* Vagrant (https://www.vagrantup.com/)
* VirtualBox (https://www.virtualbox.org/)
* kubectl (https://kubernetes.io/docs/tasks/tools/install-kubectl/)
* git (https://kubernetes.io/docs/tasks/tools/install-kubectl/)


## 仮想マシンのホスト環境

Vagrant と VirtualBox が動作するOSが必要です。

* Windows10　
* MacOS
* Linux

推奨ハードウェアと言えるか、このコードの筆者の環境は以下のとおりです。

* RAM: 8GB 以上
* ストレージ: 空き領域 5GB 以上
* CPU: Intel Core i5 以上



## NFSサーバーの開始

次のコマンドで、仮想サーバーがVirtualBoxのLAN上に起動します。

```
$ git clone https://github.com/takara9/vagrant-nfs
$ vagrant up
```


## Kubernetes の ポッドからの利用

Kubernetesクラスタからテストするには、k8s-yaml マニフェストを適用します。

```
kubectl apply -f nfs-pv.yml (NFSサーバーと接続)
kubectl apply -f nfs-pvc.yml (Persistent Volume Claim で NFSの抽象化PVと接続)
kubectl apply -f nfs-client.yml (NFSをマウントするポッドを２つ起動)
```


## 一時停止と起動

vagrant halt でクラスタの仮想サーバーをシャットダウン、vagrant up で再び起動します。



## クリーンナップ

全て削除するときは、次のコマンドを実行する。データも失われるので実行するときは注意ねがいます。

```
$ vagrant destroy
```
