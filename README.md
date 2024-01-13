# docker_ascp3 

Aspera Connect (ascp) 3.9.5 itself can run on CentOS 7, but to compare it with docker_ascp4, I created an apptainer (Singularity) container.

## Installation

Place the container image in an appropriate location within your home directory on the National Institute of Genetics supercomputer as follows:

```
cd $HOME
wget https://raw.githubusercontent.com/nig-sc/docker_ascp3/main/ascp3_ubuntu22.sif
```

Aspera Connect's installer needs to be run with user privileges and is installed under $HOME/.aspera, so the first time requires an installation process. The following command will install the ascp command:

```
$ apptainer exec ascp3_ubuntu22.sif bash ibm-aspera-connect-3.9.5.172984-linux-g2.12-64.sh

Installing IBM Aspera Connect

Install complete.
```

You can execute the ascp command as follows:

```
$ apptainer exec ascp3_ubuntu22.sif $HOME/.aspera/connect/bin/ascp --help
Usage: ascp [OPTION] SRC... DEST
          SRC to DEST, or multiple SRC to DEST dir
          SRC, DEST format: [[user@]host:]PATH
  -h,--help                       Display usage
  -A,--version                    Display version.
  -T                              Disable encryption
  -d                              Create target directory, implied for file/file-pair lists
  -p                              Preserve file timestamp
  -q                              Disable progress display
  -v                              Verbose mode
(continued below)
```

For example, executing the example from https://ena-docs.readthedocs.io/en/latest/retrieval/file-download.html#using-aspera will result in the following:

```
$ apptainer exec ascp3_ubuntu22.sif ~/.aspera/connect/bin/ascp -T -l 300m -P 33001 \
 -i ~/.aspera/connect/etc/asperaweb_id_dsa.openssh \
 era-fasp@fasp.sra.ebi.ac.uk:vol1/fastq/ERR164/ERR164407/ERR164407.fastq.gz ./
ERR164407.fastq.gz                                                                  100%  72MB 37.7Mb/s   01:58
Completed: 74523K bytes transferred in 118 seconds
 (5132K bits/sec), in 1 file.
$
```

---

# docker_ascp3
Aspera Connect ascp3.9.5 in Ubuntu 22.04

aspera connect (ascp) 3.9.5 自体は CentOS 7 で動作しますが、
docker_ascp4 との比較のために apptainer (Singularity)コンテナを作成しました。


## Installation

以下のようにしてコンテナイメージを遺伝研スパコンのホームディレクトリ中の適当な場所に置きます。

```
cd $HOME
wget  https://raw.githubusercontent.com/nig-sc/docker_ascp3/main/ascp3_ubuntu22.sif
```

Aspera Connect のインストーラはユーザ権限で実行する必要があり、$HOME/.aspera の下にインストールされるので、
最初の一回はインストール作業が必要です。以下のコマンドにより ascp コマンドがインストールされます。

```
$ apptainer exec ascp3_ubuntu22.sif bash ibm-aspera-connect-3.9.5.172984-linux-g2.12-64.sh

Installing IBM Aspera Connect

Install complete.
```

以下のようにすると ascp コマンドを実行することができます。

```
$ apptainer exec ascp3_ubuntu22.sif  $HOME/.aspera/connect/bin/ascp --help
Usage: ascp [OPTION] SRC... DEST
          SRC to DEST, or multiple SRC to DEST dir
          SRC, DEST format: [[user@]host:]PATH
  -h,--help                       Display usage
  -A,--version                    Display version.
  -T                              Disable encryption
  -d                              Create target directory, implied for file/file-pair lists
  -p                              Preserve file timestamp
  -q                              Disable progress display
  -v                              Verbose mode
(以下略)
```


例えば https://ena-docs.readthedocs.io/en/latest/retrieval/file-download.html#using-aspera の例を実行すると以下のようになります。

```
$ apptainer exec ascp3_ubuntu22.sif ~/.aspera/connect/bin/ascp -T -l 300m -P 33001 \
 -i ~/.aspera/connect/etc/asperaweb_id_dsa.openssh \
 era-fasp@fasp.sra.ebi.ac.uk:vol1/fastq/ERR164/ERR164407/ERR164407.fastq.gz ./
ERR164407.fastq.gz                                                                  100%  72MB 37.7Mb/s   01:58
Completed: 74523K bytes transferred in 118 seconds
 (5132K bits/sec), in 1 file.
$
```
