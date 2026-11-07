---
title: "Advanced usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/zk_advanced_usage"
---

The following is a simple Java example that demonstrates how to establish a ZK connection and list the nodes in ZK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">As a reminder: To ensure cluster stability, it is not recommended to program directly against ZK.</div>


```java
public class ZkTest {
    public static void main(String[] args) throws IOException {
        String hostPort = "localhost:2181";
        List<String> zooChildren = new ArrayList<String>();
        ZooKeeper zk = new ZooKeeper(hostPort, 2000, null);
        if (zk != null) {
            try {
                String zpath = "/";
                zooChildren = zk.getChildren(zpath, false);
                System.out.println("Znodes of '/': ");
                for (String child : zooChildren) {
                    System.out.println(child);
                }
            }  catch (Exception e) {
                e.printStackTrace();
            }
        }
    }
}
```


For other operations, refer to the methods provided by the Zookeeper class and invoke them as needed.
