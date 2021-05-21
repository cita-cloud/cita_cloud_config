# cita_cloud_config

创建链的配置文件。

### 依赖

* python 3
* [syncthing](https://syncthing.net)
* [kms_sm](https://github.com/cita-cloud/kms_sm) 或者 [kms_eth](https://github.com/cita-cloud/kms_eth)

安装依赖包:

```
pip install -r requirements.txt
```

### 用法

```
$ ./cita_cloud_config.py -h
usage: cita_cloud_config.py [-h] {init,increase,decrease,clean} ...

optional arguments:
  -h, --help            show this help message and exit

subcommands:
  {init,increase,decrease,clean}
                        additional help
    init                Init a chain.
    increase            Increase one node.
    decrease            Decrease one node.
    clean               Clean a chain.
```

### 初始化链

```
$ ./cita_cloud_config.py init -h
usage: cita_cloud_config.py init [-h] [--work_dir WORK_DIR] [--timestamp TIMESTAMP] [--block_delay_number BLOCK_DELAY_NUMBER]
                                 [--chain_name CHAIN_NAME] [--peers_count PEERS_COUNT] [--kms_password KMS_PASSWORD]
                                 [--enable_tls ENABLE_TLS] [--is_stdout IS_STDOUT] [--log_level LOG_LEVEL] [--is_bft IS_BFT]

optional arguments:
  -h, --help            show this help message and exit
  --work_dir WORK_DIR   The output director of node config files.
  --timestamp TIMESTAMP
                        Timestamp of genesis block.
  --block_delay_number BLOCK_DELAY_NUMBER
                        The block delay number of chain.
  --chain_name CHAIN_NAME
                        The name of chain.
  --peers_count PEERS_COUNT
                        Count of peers.
  --kms_password KMS_PASSWORD
                        Password of kms.
  --enable_tls ENABLE_TLS
                        Is enable tls
  --is_stdout IS_STDOUT
                        Is output to stdout
  --log_level LOG_LEVEL
                        log level: warn/info/debug/trace
  --is_bft IS_BFT       Is bft
```

#### 例子

```
$ ./cita_cloud_config.py init --work_dir /tmp/test --peers_count 3 --kms_password 123456
args: Namespace(subcmd='init', work_dir='/tmp/test', timestamp=None, block_delay_number=0, chain_name='test-chain', peers_count=3, kms_password='123456', enable_tls=True, is_stdout=False, log_level='info', is_bft=False)
peers: [{'ip': 'test-chain-0.test-chain-headless-service', 'port': 40000}, {'ip': 'test-chain-1.test-chain-headless-service', 'port': 40000}, {'ip': 'test-chain-2.test-chain-headless-service', 'port': 40000}]
net_config_list: [{'enable_tls': True, 'port': 40000, 'peers': [{'ip': 'test-chain-1.test-chain-headless-service', 'port': 40000}, {'ip': 'test-chain-2.test-chain-headless-service', 'port': 40000}]}, {'enable_tls': True, 'port': 40000, 'peers': [{'ip': 'test-chain-0.test-chain-headless-service', 'port': 40000}, {'ip': 'test-chain-2.test-chain-headless-service', 'port': 40000}]}, {'enable_tls': True, 'port': 40000, 'peers': [{'ip': 'test-chain-0.test-chain-headless-service', 'port': 40000}, {'ip': 'test-chain-1.test-chain-headless-service', 'port': 40000}]}]
kms create output: key_id:1,address:0x5d1157a2f6f5bd1bb92f1bab6ff1577c142df38b
kms create output: key_id:1,address:0x6015b54fd6c8e183b5e1d444bcf963fea3a1aeee
kms create output: key_id:1,address:0x69ae396a774f49f01158c02fb200eef497fcd35c
kms create output: key_id:1,address:0x9a1d2cc0ffd3c52a4a07e1339bcb844cb670dc59
device_id: OWTLO5M-ODHVLU3-FRWFGUG-BLLPKIV-S5D7STE-XUC2YRR-3ZKXJ2H-WLJR5QO
device_id: 2EO7RNI-4ZHHUR5-SF3Y6KT-VX4RK7U-P7HT6TT-QL64HZA-3H6LMRN-3N6Z2QI
device_id: KKO5QQL-FDKRFAB-N3DRPX4-RXETGKR-JMQEI4Z-ZUVTRFA-65WQWRI-GZF2QAF
sync_peers: [{'ip': 'test-chain-0.test-chain-headless-service', 'port': 22000, 'device_id': 'OWTLO5M-ODHVLU3-FRWFGUG-BLLPKIV-S5D7STE-XUC2YRR-3ZKXJ2H-WLJR5QO'}, {'ip': 'test-chain-1.test-chain-headless-service', 'port': 22000, 'device_id': '2EO7RNI-4ZHHUR5-SF3Y6KT-VX4RK7U-P7HT6TT-QL64HZA-3H6LMRN-3N6Z2QI'}, {'ip': 'test-chain-2.test-chain-headless-service', 'port': 22000, 'device_id': 'KKO5QQL-FDKRFAB-N3DRPX4-RXETGKR-JMQEI4Z-ZUVTRFA-65WQWRI-GZF2QAF'}]
Done!!!
```

#### 生成的文件

```
$ cd /tmp/test 
$ ls
test-chain  test-chain-0  test-chain-1  test-chain-2  test-chain.complete  test-chain.lock

$ ls test-chain
0x5d1157a2f6f5bd1bb92f1bab6ff1577c142df38b  2EO7RNI-4ZHHUR5-SF3Y6KT-VX4RK7U-P7HT6TT-QL64HZA-3H6LMRN-3N6Z2QI
0x6015b54fd6c8e183b5e1d444bcf963fea3a1aeee  KKO5QQL-FDKRFAB-N3DRPX4-RXETGKR-JMQEI4Z-ZUVTRFA-65WQWRI-GZF2QAF
0x69ae396a774f49f01158c02fb200eef497fcd35c  OWTLO5M-ODHVLU3-FRWFGUG-BLLPKIV-S5D7STE-XUC2YRR-3ZKXJ2H-WLJR5QO
0x9a1d2cc0ffd3c52a4a07e1339bcb844cb670dc59

$ ls test-chain-0 
config                 controller-config.toml  genesis.toml          kms.db               network_key          storage-log4rs.yaml
consensus-config.toml  controller-log4rs.yaml  init_sys_config.toml  kms-log4rs.yaml      network-log4rs.yaml  tx_infos
consensus-log4rs.yaml  executor-log4rs.yaml    key_id                network-config.toml  node_address
```

### 增加节点

```
$ ./cita_cloud_config.py increase -h                                                    
usage: cita_cloud_config.py increase [-h] [--work_dir WORK_DIR] [--chain_name CHAIN_NAME] [--kms_password KMS_PASSWORD]
                                     [--is_bft IS_BFT] [--enable_tls ENABLE_TLS]

optional arguments:
  -h, --help            show this help message and exit
  --work_dir WORK_DIR   The output director of node config files.
  --chain_name CHAIN_NAME
                        The name of chain.
  --kms_password KMS_PASSWORD
                        Password of kms.
  --is_bft IS_BFT       Is bft
  --enable_tls ENABLE_TLS
                        Is enable tls
```

注意： 参数的值一定要与初始化链时相应的参数保持一致。

##### 例子

```
$ ./cita_cloud_config.py increase --work_dir /tmp/test --kms_password 123456
args: Namespace(subcmd='increase', work_dir='/tmp/test', chain_name='test-chain', kms_password='123456', is_bft=False, enable_tls=True)
found 3 nodes
will add node 3, new peers_count is 4
peers: [{'ip': 'test-chain-0.test-chain-headless-service', 'port': 40000}, {'ip': 'test-chain-1.test-chain-headless-service', 'port': 40000}, {'ip': 'test-chain-2.test-chain-headless-service', 'port': 40000}, {'ip': 'test-chain-3.test-chain-headless-service', 'port': 40000}]
net_config_list: [{'enable_tls': True, 'port': 40000, 'peers': [{'ip': 'test-chain-1.test-chain-headless-service', 'port': 40000}, {'ip': 'test-chain-2.test-chain-headless-service', 'port': 40000}, {'ip': 'test-chain-3.test-chain-headless-service', 'port': 40000}]}, {'enable_tls': True, 'port': 40000, 'peers': [{'ip': 'test-chain-0.test-chain-headless-service', 'port': 40000}, {'ip': 'test-chain-2.test-chain-headless-service', 'port': 40000}, {'ip': 'test-chain-3.test-chain-headless-service', 'port': 40000}]}, {'enable_tls': True, 'port': 40000, 'peers': [{'ip': 'test-chain-0.test-chain-headless-service', 'port': 40000}, {'ip': 'test-chain-1.test-chain-headless-service', 'port': 40000}, {'ip': 'test-chain-3.test-chain-headless-service', 'port': 40000}]}, {'enable_tls': True, 'port': 40000, 'peers': [{'ip': 'test-chain-0.test-chain-headless-service', 'port': 40000}, {'ip': 'test-chain-1.test-chain-headless-service', 'port': 40000}, {'ip': 'test-chain-2.test-chain-headless-service', 'port': 40000}]}]
device_id: XX5SUN5-64LSWHY-OMNJFZG-UYJDNFI-TAEESJO-BGBULFW-VDSNMKT-L7QCUQV
device_id: 6XBA4SE-RO2GI4V-C7NKYCF-XF4FULX-2SXFIGS-SEFJKRZ-L4BG6VY-4RBW5AR
device_id: AXXNBHG-DOMKB3Y-J3H53G7-AW5QL6D-FQNWJVX-QER5ZIV-CYMISOG-LIWAFAI
device_id: K7ZPI46-BNGI2N4-TNNT6EC-CJUR5LK-5FK5D5E-Y5W62NX-7X3LCSE-K6ER4QC
sync_peers: [{'ip': 'test-chain-0.test-chain-headless-service', 'port': 22000, 'device_id': 'XX5SUN5-64LSWHY-OMNJFZG-UYJDNFI-TAEESJO-BGBULFW-VDSNMKT-L7QCUQV'}, {'ip': 'test-chain-1.test-chain-headless-service', 'port': 22000, 'device_id': '6XBA4SE-RO2GI4V-C7NKYCF-XF4FULX-2SXFIGS-SEFJKRZ-L4BG6VY-4RBW5AR'}, {'ip': 'test-chain-2.test-chain-headless-service', 'port': 22000, 'device_id': 'AXXNBHG-DOMKB3Y-J3H53G7-AW5QL6D-FQNWJVX-QER5ZIV-CYMISOG-LIWAFAI'}, {'ip': 'test-chain-3.test-chain-headless-service', 'port': 22000, 'device_id': 'K7ZPI46-BNGI2N4-TNNT6EC-CJUR5LK-5FK5D5E-Y5W62NX-7X3LCSE-K6ER4QC'}]
kms create output: key_id:1,address:0xd6565fc4f7f5b97abeb1deffbbbe0a463816a5e2
new node address 0xd6565fc4f7f5b97abeb1deffbbbe0a463816a5e2
```

#### 生成的文件

```
$ ls
test-chain  test-chain-0  test-chain-1  test-chain-2  test-chain-3  test-chain.complete  test-chain.lock
```
多了节点文件夹`test-chain-3`。

```
$ ls test-chain-3 
config                 controller-config.toml  genesis.toml          kms.db               network_key          storage-log4rs.yaml
consensus-config.toml  controller-log4rs.yaml  init_sys_config.toml  kms-log4rs.yaml      network-log4rs.yaml  tx_infos
consensus-log4rs.yaml  executor-log4rs.yaml    key_id                network-config.toml  node_address
```

### 减少节点

```
$ ./cita_cloud_config.py decrease -h                  
usage: cita_cloud_config.py decrease [-h] [--work_dir WORK_DIR] [--chain_name CHAIN_NAME] [--enable_tls ENABLE_TLS]

optional arguments:
  -h, --help            show this help message and exit
  --work_dir WORK_DIR   The output director of node config files.
  --chain_name CHAIN_NAME
                        The name of chain.
  --enable_tls ENABLE_TLS
                        Is enable tls
```

注意： 参数的值一定要与初始化链时相应的参数保持一致。

#### 例子

```
$ ./cita_cloud_config.py decrease --work_dir /tmp/test
args: Namespace(subcmd='decrease', work_dir='/tmp/test', chain_name='test-chain', enable_tls=True)
found 4 nodes
will delete node 3, new peers_count is 3
peers: [{'ip': 'test-chain-0.test-chain-headless-service', 'port': 40000}, {'ip': 'test-chain-1.test-chain-headless-service', 'port': 40000}, {'ip': 'test-chain-2.test-chain-headless-service', 'port': 40000}]
net_config_list: [{'enable_tls': True, 'port': 40000, 'peers': [{'ip': 'test-chain-1.test-chain-headless-service', 'port': 40000}, {'ip': 'test-chain-2.test-chain-headless-service', 'port': 40000}]}, {'enable_tls': True, 'port': 40000, 'peers': [{'ip': 'test-chain-0.test-chain-headless-service', 'port': 40000}, {'ip': 'test-chain-2.test-chain-headless-service', 'port': 40000}]}, {'enable_tls': True, 'port': 40000, 'peers': [{'ip': 'test-chain-0.test-chain-headless-service', 'port': 40000}, {'ip': 'test-chain-1.test-chain-headless-service', 'port': 40000}]}]
device_id: 2O6QGD3-432OO4V-XHTKZEE-ZS75YIV-JUDKPEM-IVH5W7Y-GXJBI2U-TTPMNAR
device_id: D6VNEC5-AMZLEWE-DL6BJ54-2RK7EI6-2RHQ7PD-YBWJQ2Y-RUQAWNH-FVFRBQT
device_id: 6VWJIEY-RSHN3OS-D2QUNYV-Q62JNI5-TDMRONP-BSV5SG2-6PT4I64-QIF34AQ
sync_peers: [{'ip': 'test-chain-0.test-chain-headless-service', 'port': 22000, 'device_id': '2O6QGD3-432OO4V-XHTKZEE-ZS75YIV-JUDKPEM-IVH5W7Y-GXJBI2U-TTPMNAR'}, {'ip': 'test-chain-1.test-chain-headless-service', 'port': 22000, 'device_id': 'D6VNEC5-AMZLEWE-DL6BJ54-2RK7EI6-2RHQ7PD-YBWJQ2Y-RUQAWNH-FVFRBQT'}, {'ip': 'test-chain-2.test-chain-headless-service', 'port': 22000, 'device_id': '6VWJIEY-RSHN3OS-D2QUNYV-Q62JNI5-TDMRONP-BSV5SG2-6PT4I64-QIF34AQ'}]
```

##### 文件变化

```
$ ls
test-chain  test-chain-0  test-chain-1  test-chain-2  test-chain.complete  test-chain.lock
```

少了节点文件夹`test-chain-3`。

### 清除链

```
$ ./cita_cloud_config.py clean -h
usage: cita_cloud_config.py clean [-h] [--work_dir WORK_DIR] [--chain_name CHAIN_NAME]

optional arguments:
  -h, --help            show this help message and exit
  --work_dir WORK_DIR   The output director of node config files.
  --chain_name CHAIN_NAME
                        The name of chain.
```

#### 例子

```
$ ./cita_cloud_config.py clean --work_dir /tmp/test
args: Namespace(subcmd='clean', work_dir='/tmp/test', chain_name='test-chain')
chain test-chain has clean!
```

##### 文件变化

```
$ ls


```

链相关文件全部被清除。