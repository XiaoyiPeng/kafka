#### 这个分支的代码，包含我对代码的注释，算是我阅读kafka（版本0.8.2）的心得体会吧。


#### 注意点：

1. controller 重启后，发送UpdateMetadata给所有broker，broker的元信息才会更新，这样 client，比如 producer获取的broker信息，才是最新元信息
   如果集群中有 broker 下线，一定要重启 controller，否则producer的元信息中有 已下线的broker信息，会往其上发送消息;
2. broker/controller 重启后, controller 发送LeaderAndIsrRequest 告诉 每个broker,你上面的replica 应该切换成leader， 还是follower.
   replica，partition的选举是在 controller 端完成的，由PartitionStateMachine，ReplicaStateMachine完成。
