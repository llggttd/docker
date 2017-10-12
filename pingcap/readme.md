docker run -d --name pd1 -p 2371:2379 -p 2381:2380 -v /data:/data pingcap/pd:latest --name="pd1" --data-dir="/data/pd1" --client-urls="http://0.0.0.0:2379" --advertise-client-urls="http://192.168.1.78:2371" --peer-urls="http://0.0.0.0:2380" --advertise-peer-urls="http://192.168.1.78:2381" --initial-cluster="pd1=http://192.168.1.78:2381,pd2=http://192.168.1.78:2382,pd3=http://192.168.1.78:2383"

docker run -d --name pd2 -p 2372:2379 -p 2382:2380 -v /data:/data pingcap/pd:latest --name="pd2" --data-dir="/data/pd2" --client-urls="http://0.0.0.0:2379" --advertise-client-urls="http://192.168.1.78:2372" --peer-urls="http://0.0.0.0:2380" --advertise-peer-urls="http://192.168.1.78:2382" --initial-cluster="pd1=http://192.168.1.78:2381,pd2=http://192.168.1.78:2382,pd3=http://192.168.1.78:2383"

docker run -d --name pd3 -p 2373:2379 -p 2383:2380 -v /data:/data pingcap/pd:latest --name="pd3" --data-dir="/data/pd3" --client-urls="http://0.0.0.0:2379" --advertise-client-urls="http://192.168.1.78:2373" --peer-urls="http://0.0.0.0:2380" --advertise-peer-urls="http://192.168.1.78:2383" --initial-cluster="pd1=http://192.168.1.78:2381,pd2=http://192.168.1.78:2382,pd3=http://192.168.1.78:2383"

docker run -d --name tikv1 -p 20161:20160 --ulimit nofile=1000000:1000000 -v /data:/data pingcap/tikv:latest --addr="0.0.0.0:20160" --advertise-addr="192.168.1.78:20161" --data-dir="/data/tikv1" --pd="192.168.1.78:2371,192.168.1.78:2372,192.168.1.78:2373"

docker run -d --name tikv2 -p 20162:20160 --ulimit nofile=1000000:1000000 -v /data:/data pingcap/tikv:latest --addr="0.0.0.0:20160" --advertise-addr="192.168.1.78:20162" --data-dir="/data/tikv2" --pd="192.168.1.78:2371,192.168.1.78:2372,192.168.1.78:2373"

docker run -d --name tikv3 -p 20163:20160 --ulimit nofile=1000000:1000000 -v /data:/data pingcap/tikv:latest --addr="0.0.0.0:20160" --advertise-addr="192.168.1.78:20163" --data-dir="/data/tikv3" --pd="192.168.1.78:2371,192.168.1.78:2372,192.168.1.78:2373"

docker run -d --name tidb -p 4000:4000 -p 10080:10080 pingcap/tidb:latest --store=tikv --path="192.168.1.78:2371,192.168.1.78:2372,192.168.1.78:2373"