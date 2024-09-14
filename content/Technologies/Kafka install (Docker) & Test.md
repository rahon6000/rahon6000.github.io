
# 설치

일반적인 도커 이미지 설치과정을 거치면 아래처럼 실행 실패하는 걸 볼 수 있다.

 ```sh
 docker images; 
REPOSITORY      TAG       IMAGE ID       CREATED      SIZE
bitnami/kafka   latest    316c66731791   2 days ago   648MB

 docker container ls 
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

 docker run bitnami/kafka:latest
kafka 06:58:14.55 INFO  ==> 
kafka 06:58:14.55 INFO  ==> Welcome to the Bitnami kafka container
kafka 06:58:14.56 INFO  ==> Subscribe to project updates by watching https://github.com/bitnami/containers
kafka 06:58:14.56 INFO  ==> Submit issues and feature requests at https://github.com/bitnami/containers/issues
kafka 06:58:14.56 INFO  ==> Upgrade to Tanzu Application Catalog for production environments to access custom-configured and pre-packaged software components. Gain enhanced features, including Software Bill of Materials (SBOM), CVE scan result reports, and VEX documents. To learn more, visit https://bitnami.com/enterprise
kafka 06:58:14.56 INFO  ==> 
kafka 06:58:14.56 INFO  ==> ** Starting Kafka setup **
kafka 06:58:14.59 ERROR ==> Kafka haven't been configured to work in either Raft or Zookeper mode. Please make sure at least one of the modes is configured.
/opt/bitnami/scripts/libkafka.sh: line 377: KAFKA_CFG_LISTENER_SECURITY_PROTOCOL_MAP: unbound variable
kafka 06:58:14.59 WARN  ==> Kafka has been configured with a PLAINTEXT listener, this setting is not recommended for production environments.
```

카프카는 메타데이터 관리, 클러스터 관리를 위해 주키퍼나 Kraft 를 사용하는데, 관련 구성이 없다는 것임.

실행할 때 옵션을 주면 해결될 것 같았다. docker-compose 는 [여기](https://docs.docker.com/compose/install/linux/#install-the-plugin-manually)를 참고해 설치함. (root 로 설치해야 했는데, user 에게 주는게 더 복잡해 보였다.)

bitnami/kafka 의 docker-compose.yml 을 그대로 사용해서 compose up 해봤다. (Kraft 사용)

```sh
 sudo docker compose up
[+] Running 1/0
 ✔ Container docker-kafka-1  Created                                                           0.0s 
Attaching to kafka-1
kafka-1  | kafka 07:41:15.37 INFO  ==> 
kafka-1  | kafka 07:41:15.37 INFO  ==> Welcome to the Bitnami kafka container
kafka-1  | kafka 07:41:15.38 INFO  ==> Subscribe to project updates by watching https://github.com/bitnami/containers
kafka-1  | kafka 07:41:15.38 INFO  ==> Submit issues and feature requests at https://github.com/bitnami/containers/issues
kafka-1  | kafka 07:41:15.38 INFO  ==> Upgrade to Tanzu Application Catalog for production environments to access custom-configured and pre-packaged software components. Gain enhanced features, including Software Bill of Materials (SBOM), CVE scan result reports, and VEX documents. To learn more, visit https://bitnami.com/enterprise
kafka-1  | kafka 07:41:15.38 INFO  ==> 
kafka-1  | kafka 07:41:15.38 INFO  ==> ** Starting Kafka setup **
kafka-1  | kafka 07:41:15.41 INFO  ==> Initializing KRaft storage metadata
kafka-1  | kafka 07:41:15.42 INFO  ==> Formatting storage directories to add metadata...
kafka-1  | metaPropertiesEnsemble=MetaPropertiesEnsemble(metadataLogDir=Optional.empty, dirs={/bitnami/kafka/data: MetaProperties(version=1, clusterId=Pc0lj7PNSkiH_QU6w44YYQ, nodeId=0, directoryId=HyCjphIex5ZBIzvhgimqaw)})
kafka-1  | All of the log directories are already formatted.
kafka-1  | kafka 07:41:16.32 INFO  ==> ** Kafka setup finished! **
kafka-1  | 
kafka-1  | kafka 07:41:16.34 INFO  ==> ** Starting Kafka **
kafka-1  | [2024-06-09 07:41:16,868] INFO Registered kafka:type=kafka.Log4jController MBean (kafka.utils.Log4jControllerRegistration$)
kafka-1  | [2024-06-09 07:41:17,032] INFO Setting -D jdk.tls.rejectClientInitiatedRenegotiation=true to disable client-initiated TLS renegotiation (org.apache.zookeeper.common.X509Util)
kafka-1  | [2024-06-09 07:41:17,119] INFO Registered signal handlers for TERM, INT, HUP (org.apache.kafka.common.utils.LoggingSignalHandler)
kafka-1  | [2024-06-09 07:41:17,121] INFO [ControllerServer id=0] Starting controller (kafka.server.ControllerServer)
kafka-1  | [2024-06-09 07:41:17,338] INFO Updated connection-accept-rate max connection creation rate to 2147483647 (kafka.network.ConnectionQuotas)
kafka-1  | [2024-06-09 07:41:17,360] INFO [SocketServer listenerType=CONTROLLER, nodeId=0] Created data-plane acceptor and processors for endpoint : ListenerName(CONTROLLER) (kafka.network.SocketServer)
kafka-1  | [2024-06-09 07:41:17,362] INFO CONTROLLER: resolved wildcard host to 0868aaa976bd (org.apache.kafka.metadata.ListenerInfo)
kafka-1  | [2024-06-09 07:41:17,365] INFO authorizerStart completed for endpoint CONTROLLER. Endpoint is now READY. (org.apache.kafka.server.network.EndpointReadyFutures)
kafka-1  | [2024-06-09 07:41:17,365] INFO [SharedServer id=0] Starting SharedServer (kafka.server.SharedServer)
kafka-1  | [2024-06-09 07:41:17,399] INFO [LogLoader partition=__cluster_metadata-0, dir=/bitnami/kafka/data] Recovering unflushed segment 0. 0/1 recovered for __cluster_metadata-0. (kafka.log.LogLoader)
kafka-1  | [2024-06-09 07:41:17,400] INFO [LogLoader partition=__cluster_metadata-0, dir=/bitnami/kafka/data] Loading producer state till offset 0 with message format version 2 (kafka.log.UnifiedLog$)
kafka-1  | [2024-06-09 07:41:17,400] INFO [LogLoader partition=__cluster_metadata-0, dir=/bitnami/kafka/data] Reloading from producer snapshot and rebuilding producer state from offset 0 (kafka.log.UnifiedLog$)
kafka-1  | [2024-06-09 07:41:17,401] INFO Deleted producer state snapshot /bitnami/kafka/data/__cluster_metadata-0/00000000000000000028.snapshot (org.apache.kafka.storage.internals.log.SnapshotFile)
kafka-1  | [2024-06-09 07:41:17,401] INFO [LogLoader partition=__cluster_metadata-0, dir=/bitnami/kafka/data] Producer state recovery took 0ms for snapshot load and 0ms for segment recovery from offset 0 (kafka.log.UnifiedLog$)
kafka-1  | [2024-06-09 07:41:17,427] INFO [ProducerStateManager partition=__cluster_metadata-0] Wrote producer snapshot at offset 28 with 0 producer ids in 20 ms. (org.apache.kafka.storage.internals.log.ProducerStateManager)
kafka-1  | [2024-06-09 07:41:17,434] INFO [LogLoader partition=__cluster_metadata-0, dir=/bitnami/kafka/data] Loading producer state till offset 28 with message format version 2 (kafka.log.UnifiedLog$)
kafka-1  | [2024-06-09 07:41:17,434] INFO [LogLoader partition=__cluster_metadata-0, dir=/bitnami/kafka/data] Reloading from producer snapshot and rebuilding producer state from offset 28 (kafka.log.UnifiedLog$)
kafka-1  | [2024-06-09 07:41:17,434] INFO [ProducerStateManager partition=__cluster_metadata-0] Loading producer state from snapshot file 'SnapshotFile(offset=28, file=/bitnami/kafka/data/__cluster_metadata-0/00000000000000000028.snapshot)' (org.apache.kafka.storage.internals.log.ProducerStateManager)
kafka-1  | [2024-06-09 07:41:17,435] INFO [LogLoader partition=__cluster_metadata-0, dir=/bitnami/kafka/data] Producer state recovery took 1ms for snapshot load and 0ms for segment recovery from offset 28 (kafka.log.UnifiedLog$)
kafka-1  | [2024-06-09 07:41:17,452] INFO Initialized snapshots with IDs Set() from /bitnami/kafka/data/__cluster_metadata-0 (kafka.raft.KafkaMetadataLog$)
kafka-1  | [2024-06-09 07:41:17,460] INFO [raft-expiration-reaper]: Starting (kafka.raft.TimingWheelExpirationService$ExpiredOperationReaper)
kafka-1  | [2024-06-09 07:41:17,551] INFO [RaftManager id=0] Completed transition to ResignedState(localId=0, epoch=1, voters=[0], electionTimeoutMs=1905, unackedVoters=[], preferredSuccessors=[]) from null (org.apache.kafka.raft.QuorumState)
kafka-1  | [2024-06-09 07:41:17,557] INFO [RaftManager id=0] Completed transition to CandidateState(localId=0, epoch=2, retries=1, voteStates={0=GRANTED}, highWatermark=Optional.empty, electionTimeoutMs=1492) from ResignedState(localId=0, epoch=1, voters=[0], electionTimeoutMs=1905, unackedVoters=[], preferredSuccessors=[]) (org.apache.kafka.raft.QuorumState)
kafka-1  | [2024-06-09 07:41:17,565] INFO [RaftManager id=0] Completed transition to Leader(localId=0, epoch=2, epochStartOffset=28, highWatermark=Optional.empty, voterStates={0=ReplicaState(nodeId=0, endOffset=Optional.empty, lastFetchTimestamp=-1, lastCaughtUpTimestamp=-1, hasAcknowledgedLeader=true)}) from CandidateState(localId=0, epoch=2, retries=1, voteStates={0=GRANTED}, highWatermark=Optional.empty, electionTimeoutMs=1492) (org.apache.kafka.raft.QuorumState)
kafka-1  | [2024-06-09 07:41:17,577] INFO [kafka-0-raft-outbound-request-thread]: Starting (org.apache.kafka.raft.KafkaNetworkChannel$SendThread)
kafka-1  | [2024-06-09 07:41:17,577] INFO [kafka-0-raft-io-thread]: Starting (kafka.raft.KafkaRaftManager$RaftIoThread)
kafka-1  | [2024-06-09 07:41:17,586] INFO [MetadataLoader id=0] initializeNewPublishers: the loader is still catching up because we still don't know the high water mark yet. (org.apache.kafka.image.loader.MetadataLoader)
kafka-1  | [2024-06-09 07:41:17,586] INFO [RaftManager id=0] High watermark set to LogOffsetMetadata(offset=29, metadata=Optional[(segmentBaseOffset=0,relativePositionInSegment=2299)]) for the first time for epoch 2 based on indexOfHw 0 and voters [ReplicaState(nodeId=0, endOffset=Optional[LogOffsetMetadata(offset=29, metadata=Optional[(segmentBaseOffset=0,relativePositionInSegment=2299)])], lastFetchTimestamp=-1, lastCaughtUpTimestamp=-1, hasAcknowledgedLeader=true)] (org.apache.kafka.raft.LeaderState)
kafka-1  | [2024-06-09 07:41:17,587] INFO [ControllerServer id=0] Waiting for controller quorum voters future (kafka.server.ControllerServer)
kafka-1  | [2024-06-09 07:41:17,587] INFO [ControllerServer id=0] Finished waiting for controller quorum voters future (kafka.server.ControllerServer)
kafka-1  | [2024-06-09 07:41:17,592] INFO [RaftManager id=0] Registered the listener org.apache.kafka.image.loader.MetadataLoader@1173206478 (org.apache.kafka.raft.KafkaRaftClient)
kafka-1  | [2024-06-09 07:41:17,599] INFO [MetadataLoader id=0] maybePublishMetadata(LOG_DELTA): The loader is still catching up because we have loaded up to offset 0, but the high water mark is 29 (org.apache.kafka.image.loader.MetadataLoader)
kafka-1  | [2024-06-09 07:41:17,605] INFO [QuorumController id=0] Creating new QuorumController with clusterId Pc0lj7PNSkiH_QU6w44YYQ. (org.apache.kafka.controller.QuorumController)
kafka-1  | [2024-06-09 07:41:17,605] INFO [RaftManager id=0] Registered the listener org.apache.kafka.controller.QuorumController$QuorumMetaLogListener@1258775547 (org.apache.kafka.raft.KafkaRaftClient)
kafka-1  | [2024-06-09 07:41:17,607] INFO [QuorumController id=0] Replayed BeginTransactionRecord(name='Bootstrap records') at offset 1. (org.apache.kafka.controller.OffsetControlManager)
kafka-1  | [2024-06-09 07:41:17,607] INFO [QuorumController id=0] Replayed a FeatureLevelRecord setting metadata version to 3.7-IV4 (org.apache.kafka.controller.FeatureControlManager)
kafka-1  | [2024-06-09 07:41:17,607] INFO [QuorumController id=0] Replayed EndTransactionRecord() at offset 4. (org.apache.kafka.controller.OffsetControlManager)
kafka-1  | [2024-06-09 07:41:17,607] INFO [MetadataLoader id=0] maybePublishMetadata(LOG_DELTA): The loader finished catching up to the current high water mark of 29 (org.apache.kafka.image.loader.MetadataLoader)
kafka-1  | [2024-06-09 07:41:17,608] INFO [QuorumController id=0] Replayed RegisterControllerRecord contaning ControllerRegistration(id=0, incarnationId=8kgFNIdzRWiiQzb6qpaBiw, zkMigrationReady=false, listeners=[Endpoint(listenerName='CONTROLLER', securityProtocol=PLAINTEXT, host='0868aaa976bd', port=9093)], supportedFeatures={metadata.version: 1-19}). (org.apache.kafka.controller.ClusterControlManager)
kafka-1  | [2024-06-09 07:41:17,608] INFO [QuorumController id=0] Replayed initial RegisterBrokerRecord for broker 0: RegisterBrokerRecord(brokerId=0, isMigratingZkBroker=false, incarnationId=Yon7a8obTw-BsxtRnhFnFQ, brokerEpoch=6, endPoints=[BrokerEndpoint(name='PLAINTEXT', host='0868aaa976bd', port=9092, securityProtocol=0)], features=[BrokerFeature(name='metadata.version', minSupportedVersion=1, maxSupportedVersion=19)], rack=null, fenced=true, inControlledShutdown=false, logDirs=[HyCjphIex5ZBIzvhgimqaw]) (org.apache.kafka.controller.ClusterControlManager)
kafka-1  | [2024-06-09 07:41:17,609] INFO [QuorumController id=0] Replayed RegisterBrokerRecord modifying the registration for broker 0: RegisterBrokerRecord(brokerId=0, isMigratingZkBroker=false, incarnationId=Yon7a8obTw-BsxtRnhFnFQ, brokerEpoch=7, endPoints=[BrokerEndpoint(name='PLAINTEXT', host='0868aaa976bd', port=9092, securityProtocol=0)], features=[BrokerFeature(name='metadata.version', minSupportedVersion=1, maxSupportedVersion=19)], rack=null, fenced=true, inControlledShutdown=false, logDirs=[HyCjphIex5ZBIzvhgimqaw]) (org.apache.kafka.controller.ClusterControlManager)
kafka-1  | [2024-06-09 07:41:17,609] INFO [QuorumController id=0] Replayed BrokerRegistrationChangeRecord modifying the registration for broker 0: BrokerRegistrationChangeRecord(brokerId=0, brokerEpoch=7, fenced=-1, inControlledShutdown=0, logDirs=[]) (org.apache.kafka.controller.ClusterControlManager)
kafka-1  | [2024-06-09 07:41:17,609] INFO [MetadataLoader id=0] InitializeNewPublishers: initializing SnapshotGenerator with a snapshot at offset 28 (org.apache.kafka.image.loader.MetadataLoader)
kafka-1  | [2024-06-09 07:41:17,610] INFO [controller-0-ThrottledChannelReaper-Fetch]: Starting (kafka.server.ClientQuotaManager$ThrottledChannelReaper)
kafka-1  | [2024-06-09 07:41:17,611] INFO [QuorumController id=0] Replayed BrokerRegistrationChangeRecord modifying the registration for broker 0: BrokerRegistrationChangeRecord(brokerId=0, brokerEpoch=7, fenced=1, inControlledShutdown=0, logDirs=[]) (org.apache.kafka.controller.ClusterControlManager)
kafka-1  | [2024-06-09 07:41:17,611] INFO [controller-0-ThrottledChannelReaper-Produce]: Starting (kafka.server.ClientQuotaManager$ThrottledChannelReaper)
kafka-1  | [2024-06-09 07:41:17,611] INFO [controller-0-ThrottledChannelReaper-Request]: Starting (kafka.server.ClientQuotaManager$ThrottledChannelReaper)
kafka-1  | [2024-06-09 07:41:17,612] INFO [QuorumController id=0] Becoming the active controller at epoch 2, next write offset 29. (org.apache.kafka.controller.QuorumController)
kafka-1  | [2024-06-09 07:41:17,613] INFO [controller-0-ThrottledChannelReaper-ControllerMutation]: Starting (kafka.server.ClientQuotaManager$ThrottledChannelReaper)
kafka-1  | [2024-06-09 07:41:17,615] WARN [QuorumController id=0] Performing controller activation. Loaded ZK migration state of NONE. (org.apache.kafka.controller.QuorumController)
kafka-1  | [2024-06-09 07:41:17,624] INFO [ExpirationReaper-0-AlterAcls]: Starting (kafka.server.DelayedOperationPurgatory$ExpiredOperationReaper)
kafka-1  | [2024-06-09 07:41:17,632] INFO [ControllerServer id=0] Waiting for the controller metadata publishers to be installed (kafka.server.ControllerServer)
kafka-1  | [2024-06-09 07:41:17,632] INFO [ControllerServer id=0] Finished waiting for the controller metadata publishers to be installed (kafka.server.ControllerServer)
kafka-1  | [2024-06-09 07:41:17,632] INFO [MetadataLoader id=0] InitializeNewPublishers: initializing KRaftMetadataCachePublisher with a snapshot at offset 28 (org.apache.kafka.image.loader.MetadataLoader)
kafka-1  | [2024-06-09 07:41:17,632] INFO [MetadataLoader id=0] InitializeNewPublishers: initializing FeaturesPublisher with a snapshot at offset 28 (org.apache.kafka.image.loader.MetadataLoader)
kafka-1  | [2024-06-09 07:41:17,632] INFO [ControllerServer id=0] Loaded new metadata Features(version=3.7-IV4, finalizedFeatures={metadata.version=19}, finalizedFeaturesEpoch=28). (org.apache.kafka.metadata.publisher.FeaturesPublisher)
kafka-1  | [2024-06-09 07:41:17,632] INFO [SocketServer listenerType=CONTROLLER, nodeId=0] Enabling request processing. (kafka.network.SocketServer)
kafka-1  | [2024-06-09 07:41:17,632] INFO [MetadataLoader id=0] InitializeNewPublishers: initializing ControllerRegistrationsPublisher with a snapshot at offset 28 (org.apache.kafka.image.loader.MetadataLoader)
kafka-1  | [2024-06-09 07:41:17,632] INFO [MetadataLoader id=0] InitializeNewPublishers: initializing ControllerRegistrationManager with a snapshot at offset 28 (org.apache.kafka.image.loader.MetadataLoader)
kafka-1  | [2024-06-09 07:41:17,633] INFO [MetadataLoader id=0] InitializeNewPublishers: initializing DynamicConfigPublisher controller id=0 with a snapshot at offset 28 (org.apache.kafka.image.loader.MetadataLoader)
kafka-1  | [2024-06-09 07:41:17,633] INFO [ControllerRegistrationManager id=0 incarnation=Ew6cfEBJRGaCvVQCEtrj7g] Found registration for 8kgFNIdzRWiiQzb6qpaBiw instead of our incarnation. (kafka.server.ControllerRegistrationManager)
kafka-1  | [2024-06-09 07:41:17,633] INFO [MetadataLoader id=0] InitializeNewPublishers: initializing DynamicClientQuotaPublisher controller id=0 with a snapshot at offset 28 (org.apache.kafka.image.loader.MetadataLoader)
kafka-1  | [2024-06-09 07:41:17,634] INFO [MetadataLoader id=0] InitializeNewPublishers: initializing ScramPublisher controller id=0 with a snapshot at offset 28 (org.apache.kafka.image.loader.MetadataLoader)
kafka-1  | [2024-06-09 07:41:17,634] INFO [MetadataLoader id=0] InitializeNewPublishers: initializing DelegationTokenPublisher controller id=0 with a snapshot at offset 28 (org.apache.kafka.image.loader.MetadataLoader)
kafka-1  | [2024-06-09 07:41:17,634] INFO Awaiting socket connections on 0.0.0.0:9093. (kafka.network.DataPlaneAcceptor)
kafka-1  | [2024-06-09 07:41:17,635] INFO [MetadataLoader id=0] InitializeNewPublishers: initializing ControllerMetadataMetricsPublisher with a snapshot at offset 28 (org.apache.kafka.image.loader.MetadataLoader)
kafka-1  | [2024-06-09 07:41:17,635] INFO [MetadataLoader id=0] InitializeNewPublishers: initializing AclPublisher controller id=0 with a snapshot at offset 28 (org.apache.kafka.image.loader.MetadataLoader)
kafka-1  | [2024-06-09 07:41:17,646] INFO [controller-0-to-controller-registration-channel-manager]: Starting (kafka.server.NodeToControllerRequestThread)
kafka-1  | [2024-06-09 07:41:17,646] INFO [ControllerServer id=0] Waiting for all of the authorizer futures to be completed (kafka.server.ControllerServer)
kafka-1  | [2024-06-09 07:41:17,646] INFO [ControllerRegistrationManager id=0 incarnation=Ew6cfEBJRGaCvVQCEtrj7g] initialized channel manager. (kafka.server.ControllerRegistrationManager)
kafka-1  | [2024-06-09 07:41:17,646] INFO [ControllerServer id=0] Finished waiting for all of the authorizer futures to be completed (kafka.server.ControllerServer)
kafka-1  | [2024-06-09 07:41:17,646] INFO [ControllerServer id=0] Waiting for all of the SocketServer Acceptors to be started (kafka.server.ControllerServer)
kafka-1  | [2024-06-09 07:41:17,646] INFO [ControllerServer id=0] Finished waiting for all of the SocketServer Acceptors to be started (kafka.server.ControllerServer)
kafka-1  | [2024-06-09 07:41:17,646] INFO [controller-0-to-controller-registration-channel-manager]: Recorded new controller, from now on will use node kafka:9093 (id: 0 rack: null) (kafka.server.NodeToControllerRequestThread)
kafka-1  | [2024-06-09 07:41:17,647] INFO [BrokerServer id=0] Transition from SHUTDOWN to STARTING (kafka.server.BrokerServer)
kafka-1  | [2024-06-09 07:41:17,647] INFO [BrokerServer id=0] Starting broker (kafka.server.BrokerServer)
kafka-1  | [2024-06-09 07:41:17,647] INFO [ControllerRegistrationManager id=0 incarnation=Ew6cfEBJRGaCvVQCEtrj7g] sendControllerRegistration: attempting to send ControllerRegistrationRequestData(controllerId=0, incarnationId=Ew6cfEBJRGaCvVQCEtrj7g, zkMigrationReady=false, listeners=[Listener(name='CONTROLLER', host='0868aaa976bd', port=9093, securityProtocol=0)], features=[Feature(name='metadata.version', minSupportedVersion=1, maxSupportedVersion=19)]) (kafka.server.ControllerRegistrationManager)
kafka-1  | [2024-06-09 07:41:17,653] INFO [broker-0-ThrottledChannelReaper-Fetch]: Starting (kafka.server.ClientQuotaManager$ThrottledChannelReaper)
kafka-1  | [2024-06-09 07:41:17,653] INFO [broker-0-ThrottledChannelReaper-Produce]: Starting (kafka.server.ClientQuotaManager$ThrottledChannelReaper)
kafka-1  | [2024-06-09 07:41:17,653] INFO [broker-0-ThrottledChannelReaper-Request]: Starting (kafka.server.ClientQuotaManager$ThrottledChannelReaper)
kafka-1  | [2024-06-09 07:41:17,654] INFO [broker-0-ThrottledChannelReaper-ControllerMutation]: Starting (kafka.server.ClientQuotaManager$ThrottledChannelReaper)
kafka-1  | [2024-06-09 07:41:17,669] INFO [BrokerServer id=0] Waiting for controller quorum voters future (kafka.server.BrokerServer)
kafka-1  | [2024-06-09 07:41:17,669] INFO [BrokerServer id=0] Finished waiting for controller quorum voters future (kafka.server.BrokerServer)
kafka-1  | [2024-06-09 07:41:17,670] INFO [broker-0-to-controller-forwarding-channel-manager]: Starting (kafka.server.NodeToControllerRequestThread)
kafka-1  | [2024-06-09 07:41:17,670] INFO [broker-0-to-controller-forwarding-channel-manager]: Recorded new controller, from now on will use node kafka:9093 (id: 0 rack: null) (kafka.server.NodeToControllerRequestThread)
kafka-1  | [2024-06-09 07:41:17,698] INFO [QuorumController id=0] Replayed RegisterControllerRecord contaning ControllerRegistration(id=0, incarnationId=Ew6cfEBJRGaCvVQCEtrj7g, zkMigrationReady=false, listeners=[Endpoint(listenerName='CONTROLLER', securityProtocol=PLAINTEXT, host='0868aaa976bd', port=9093)], supportedFeatures={metadata.version: 1-19}). Previous incarnation was 8kgFNIdzRWiiQzb6qpaBiw (org.apache.kafka.controller.ClusterControlManager)
kafka-1  | [2024-06-09 07:41:17,713] INFO Updated connection-accept-rate max connection creation rate to 2147483647 (kafka.network.ConnectionQuotas)
kafka-1  | [2024-06-09 07:41:17,717] INFO [SocketServer listenerType=BROKER, nodeId=0] Created data-plane acceptor and processors for endpoint : ListenerName(PLAINTEXT) (kafka.network.SocketServer)
kafka-1  | [2024-06-09 07:41:17,718] INFO PLAINTEXT: resolved wildcard host to 0868aaa976bd (org.apache.kafka.metadata.ListenerInfo)
kafka-1  | [2024-06-09 07:41:17,721] INFO [broker-0-to-controller-alter-partition-channel-manager]: Starting (kafka.server.NodeToControllerRequestThread)
kafka-1  | [2024-06-09 07:41:17,722] INFO [broker-0-to-controller-alter-partition-channel-manager]: Recorded new controller, from now on will use node kafka:9093 (id: 0 rack: null) (kafka.server.NodeToControllerRequestThread)
kafka-1  | [2024-06-09 07:41:17,729] INFO [broker-0-to-controller-directory-assignments-channel-manager]: Starting (kafka.server.NodeToControllerRequestThread)
kafka-1  | [2024-06-09 07:41:17,729] INFO [broker-0-to-controller-directory-assignments-channel-manager]: Recorded new controller, from now on will use node kafka:9093 (id: 0 rack: null) (kafka.server.NodeToControllerRequestThread)
kafka-1  | [2024-06-09 07:41:17,732] INFO [ControllerRegistrationManager id=0 incarnation=Ew6cfEBJRGaCvVQCEtrj7g] Our registration has been persisted to the metadata log. (kafka.server.ControllerRegistrationManager)
kafka-1  | [2024-06-09 07:41:17,737] INFO [ControllerRegistrationManager id=0 incarnation=Ew6cfEBJRGaCvVQCEtrj7g] RegistrationResponseHandler: controller acknowledged ControllerRegistrationRequest. (kafka.server.ControllerRegistrationManager)
kafka-1  | [2024-06-09 07:41:17,746] INFO [ExpirationReaper-0-Produce]: Starting (kafka.server.DelayedOperationPurgatory$ExpiredOperationReaper)
kafka-1  | [2024-06-09 07:41:17,746] INFO [ExpirationReaper-0-Fetch]: Starting (kafka.server.DelayedOperationPurgatory$ExpiredOperationReaper)
kafka-1  | [2024-06-09 07:41:17,747] INFO [ExpirationReaper-0-DeleteRecords]: Starting (kafka.server.DelayedOperationPurgatory$ExpiredOperationReaper)
kafka-1  | [2024-06-09 07:41:17,747] INFO [ExpirationReaper-0-ElectLeader]: Starting (kafka.server.DelayedOperationPurgatory$ExpiredOperationReaper)
kafka-1  | [2024-06-09 07:41:17,748] INFO [ExpirationReaper-0-RemoteFetch]: Starting (kafka.server.DelayedOperationPurgatory$ExpiredOperationReaper)
kafka-1  | [2024-06-09 07:41:17,758] INFO [ExpirationReaper-0-Heartbeat]: Starting (kafka.server.DelayedOperationPurgatory$ExpiredOperationReaper)
kafka-1  | [2024-06-09 07:41:17,758] INFO [ExpirationReaper-0-Rebalance]: Starting (kafka.server.DelayedOperationPurgatory$ExpiredOperationReaper)
kafka-1  | [2024-06-09 07:41:17,810] INFO [broker-0-to-controller-heartbeat-channel-manager]: Starting (kafka.server.NodeToControllerRequestThread)
kafka-1  | [2024-06-09 07:41:17,810] INFO [broker-0-to-controller-heartbeat-channel-manager]: Recorded new controller, from now on will use node kafka:9093 (id: 0 rack: null) (kafka.server.NodeToControllerRequestThread)
kafka-1  | [2024-06-09 07:41:17,814] INFO [BrokerLifecycleManager id=0] Incarnation KEy_3lnCREO8_HvGOHb9jA of broker 0 in cluster Pc0lj7PNSkiH_QU6w44YYQ is now STARTING. (kafka.server.BrokerLifecycleManager)
kafka-1  | [2024-06-09 07:41:17,834] INFO [ExpirationReaper-0-AlterAcls]: Starting (kafka.server.DelayedOperationPurgatory$ExpiredOperationReaper)
kafka-1  | [2024-06-09 07:41:17,839] INFO [QuorumController id=0] Replayed RegisterBrokerRecord establishing a new incarnation of broker 0: RegisterBrokerRecord(brokerId=0, isMigratingZkBroker=false, incarnationId=KEy_3lnCREO8_HvGOHb9jA, brokerEpoch=30, endPoints=[BrokerEndpoint(name='PLAINTEXT', host='0868aaa976bd', port=9092, securityProtocol=0)], features=[BrokerFeature(name='metadata.version', minSupportedVersion=1, maxSupportedVersion=19)], rack=null, fenced=true, inControlledShutdown=false, logDirs=[HyCjphIex5ZBIzvhgimqaw]) (org.apache.kafka.controller.ClusterControlManager)
kafka-1  | [2024-06-09 07:41:17,847] INFO [BrokerServer id=0] Waiting for the broker metadata publishers to be installed (kafka.server.BrokerServer)
kafka-1  | [2024-06-09 07:41:17,847] INFO [BrokerServer id=0] Finished waiting for the broker metadata publishers to be installed (kafka.server.BrokerServer)
kafka-1  | [2024-06-09 07:41:17,847] INFO [BrokerServer id=0] Waiting for the controller to acknowledge that we are caught up (kafka.server.BrokerServer)
kafka-1  | [2024-06-09 07:41:17,848] INFO [MetadataLoader id=0] InitializeNewPublishers: initializing BrokerMetadataPublisher with a snapshot at offset 29 (org.apache.kafka.image.loader.MetadataLoader)
kafka-1  | [2024-06-09 07:41:17,848] INFO [BrokerMetadataPublisher id=0] Publishing initial metadata at offset OffsetAndEpoch(offset=29, epoch=2) with metadata.version 3.7-IV4. (kafka.server.metadata.BrokerMetadataPublisher)
kafka-1  | [2024-06-09 07:41:17,849] INFO Loading logs from log dirs ArrayBuffer(/bitnami/kafka/data) (kafka.log.LogManager)
kafka-1  | [2024-06-09 07:41:17,851] INFO No logs found to be loaded in /bitnami/kafka/data (kafka.log.LogManager)
kafka-1  | [2024-06-09 07:41:17,857] INFO Loaded 0 logs in 9ms (kafka.log.LogManager)
kafka-1  | [2024-06-09 07:41:17,858] INFO Starting log cleanup with a period of 300000 ms. (kafka.log.LogManager)
kafka-1  | [2024-06-09 07:41:17,858] INFO Starting log flusher with a default period of 9223372036854775807 ms. (kafka.log.LogManager)
kafka-1  | [2024-06-09 07:41:17,866] INFO Starting the log cleaner (kafka.log.LogCleaner)
kafka-1  | [2024-06-09 07:41:17,867] INFO [BrokerLifecycleManager id=0] Successfully registered broker 0 with broker epoch 30 (kafka.server.BrokerLifecycleManager)
kafka-1  | [2024-06-09 07:41:17,886] INFO [kafka-log-cleaner-thread-0]: Starting (kafka.log.LogCleaner$CleanerThread)
kafka-1  | [2024-06-09 07:41:17,888] INFO [LogDirFailureHandler]: Starting (kafka.server.ReplicaManager$LogDirFailureHandler)
kafka-1  | [2024-06-09 07:41:17,888] INFO [AddPartitionsToTxnSenderThread-0]: Starting (kafka.server.AddPartitionsToTxnManager)
kafka-1  | [2024-06-09 07:41:17,889] INFO [GroupCoordinator 0]: Starting up. (kafka.coordinator.group.GroupCoordinator)
kafka-1  | [2024-06-09 07:41:17,890] INFO [GroupCoordinator 0]: Startup complete. (kafka.coordinator.group.GroupCoordinator)
kafka-1  | [2024-06-09 07:41:17,891] INFO [TransactionCoordinator id=0] Starting up. (kafka.coordinator.transaction.TransactionCoordinator)
kafka-1  | [2024-06-09 07:41:17,891] INFO [TxnMarkerSenderThread-0]: Starting (kafka.coordinator.transaction.TransactionMarkerChannelManager)
kafka-1  | [2024-06-09 07:41:17,891] INFO [TransactionCoordinator id=0] Startup complete. (kafka.coordinator.transaction.TransactionCoordinator)
kafka-1  | [2024-06-09 07:41:17,892] INFO [BrokerMetadataPublisher id=0] Updating metadata.version to 19 at offset OffsetAndEpoch(offset=29, epoch=2). (kafka.server.metadata.BrokerMetadataPublisher)
kafka-1  | [2024-06-09 07:41:17,896] INFO [BrokerMetadataPublisher id=0] Resending BrokerRegistration with existing incarnation-id to inform the controller about log directories in the broker following metadata update: previousMetadataVersion: 3.0-IV1 newMetadataVersion: 3.7-IV4 (kafka.server.metadata.BrokerMetadataPublisher)
kafka-1  | [2024-06-09 07:41:17,900] INFO [QuorumController id=0] Replayed RegisterBrokerRecord modifying the registration for broker 0: RegisterBrokerRecord(brokerId=0, isMigratingZkBroker=false, incarnationId=KEy_3lnCREO8_HvGOHb9jA, brokerEpoch=31, endPoints=[BrokerEndpoint(name='PLAINTEXT', host='0868aaa976bd', port=9092, securityProtocol=0)], features=[BrokerFeature(name='metadata.version', minSupportedVersion=1, maxSupportedVersion=19)], rack=null, fenced=true, inControlledShutdown=false, logDirs=[HyCjphIex5ZBIzvhgimqaw]) (org.apache.kafka.controller.ClusterControlManager)
kafka-1  | [2024-06-09 07:41:17,927] INFO [BrokerLifecycleManager id=0] Successfully registered broker 0 with broker epoch 31 (kafka.server.BrokerLifecycleManager)
kafka-1  | [2024-06-09 07:41:17,927] INFO [QuorumController id=0] Replayed RegisterBrokerRecord modifying the registration for broker 0: RegisterBrokerRecord(brokerId=0, isMigratingZkBroker=false, incarnationId=KEy_3lnCREO8_HvGOHb9jA, brokerEpoch=32, endPoints=[BrokerEndpoint(name='PLAINTEXT', host='0868aaa976bd', port=9092, securityProtocol=0)], features=[BrokerFeature(name='metadata.version', minSupportedVersion=1, maxSupportedVersion=19)], rack=null, fenced=true, inControlledShutdown=false, logDirs=[HyCjphIex5ZBIzvhgimqaw]) (org.apache.kafka.controller.ClusterControlManager)
kafka-1  | [2024-06-09 07:41:17,953] INFO [BrokerLifecycleManager id=0] Successfully registered broker 0 with broker epoch 32 (kafka.server.BrokerLifecycleManager)
kafka-1  | [2024-06-09 07:41:17,955] INFO [QuorumController id=0] processBrokerHeartbeat: event failed with StaleBrokerEpochException in 79 microseconds. (org.apache.kafka.controller.QuorumController)
kafka-1  | [2024-06-09 07:41:17,956] WARN [BrokerLifecycleManager id=0] Broker 0 sent a heartbeat request but received error STALE_BROKER_EPOCH. (kafka.server.BrokerLifecycleManager)
kafka-1  | [2024-06-09 07:41:17,957] INFO [BrokerLifecycleManager id=0] The broker has caught up. Transitioning from STARTING to RECOVERY. (kafka.server.BrokerLifecycleManager)
kafka-1  | [2024-06-09 07:41:17,957] INFO [BrokerServer id=0] Finished waiting for the controller to acknowledge that we are caught up (kafka.server.BrokerServer)
kafka-1  | [2024-06-09 07:41:17,957] INFO [BrokerServer id=0] Waiting for the initial broker metadata update to be published (kafka.server.BrokerServer)
kafka-1  | [2024-06-09 07:41:17,957] INFO [BrokerServer id=0] Finished waiting for the initial broker metadata update to be published (kafka.server.BrokerServer)
kafka-1  | [2024-06-09 07:41:17,958] INFO KafkaConfig values: 
kafka-1  | 	advertised.listeners = PLAINTEXT://:9092
kafka-1  | 	alter.config.policy.class.name = null
kafka-1  | 	alter.log.dirs.replication.quota.window.num = 11
kafka-1  | 	alter.log.dirs.replication.quota.window.size.seconds = 1
kafka-1  | 	authorizer.class.name = 
kafka-1  | 	auto.create.topics.enable = true
kafka-1  | 	auto.include.jmx.reporter = true
kafka-1  | 	auto.leader.rebalance.enable = true
kafka-1  | 	background.threads = 10
kafka-1  | 	broker.heartbeat.interval.ms = 2000
kafka-1  | 	broker.id = 0
kafka-1  | 	broker.id.generation.enable = true
kafka-1  | 	broker.rack = null
kafka-1  | 	broker.session.timeout.ms = 9000
kafka-1  | 	client.quota.callback.class = null
kafka-1  | 	compression.type = producer
kafka-1  | 	connection.failed.authentication.delay.ms = 100
kafka-1  | 	connections.max.idle.ms = 600000
kafka-1  | 	connections.max.reauth.ms = 0
kafka-1  | 	control.plane.listener.name = null
kafka-1  | 	controlled.shutdown.enable = true
kafka-1  | 	controlled.shutdown.max.retries = 3
kafka-1  | 	controlled.shutdown.retry.backoff.ms = 5000
kafka-1  | 	controller.listener.names = CONTROLLER
kafka-1  | 	controller.quorum.append.linger.ms = 25
kafka-1  | 	controller.quorum.election.backoff.max.ms = 1000
kafka-1  | 	controller.quorum.election.timeout.ms = 1000
kafka-1  | 	controller.quorum.fetch.timeout.ms = 2000
kafka-1  | 	controller.quorum.request.timeout.ms = 2000
kafka-1  | 	controller.quorum.retry.backoff.ms = 20
kafka-1  | 	controller.quorum.voters = [0@kafka:9093]
kafka-1  | 	controller.quota.window.num = 11
kafka-1  | 	controller.quota.window.size.seconds = 1
kafka-1  | 	controller.socket.timeout.ms = 30000
kafka-1  | 	create.topic.policy.class.name = null
kafka-1  | 	default.replication.factor = 1
kafka-1  | 	delegation.token.expiry.check.interval.ms = 3600000
kafka-1  | 	delegation.token.expiry.time.ms = 86400000
kafka-1  | 	delegation.token.master.key = null
kafka-1  | 	delegation.token.max.lifetime.ms = 604800000
kafka-1  | 	delegation.token.secret.key = null
kafka-1  | 	delete.records.purgatory.purge.interval.requests = 1
kafka-1  | 	delete.topic.enable = true
kafka-1  | 	early.start.listeners = null
kafka-1  | 	eligible.leader.replicas.enable = false
kafka-1  | 	fetch.max.bytes = 57671680
kafka-1  | 	fetch.purgatory.purge.interval.requests = 1000
kafka-1  | 	group.consumer.assignors = [org.apache.kafka.coordinator.group.assignor.UniformAssignor, org.apache.kafka.coordinator.group.assignor.RangeAssignor]
kafka-1  | 	group.consumer.heartbeat.interval.ms = 5000
kafka-1  | 	group.consumer.max.heartbeat.interval.ms = 15000
kafka-1  | 	group.consumer.max.session.timeout.ms = 60000
kafka-1  | 	group.consumer.max.size = 2147483647
kafka-1  | 	group.consumer.min.heartbeat.interval.ms = 5000
kafka-1  | 	group.consumer.min.session.timeout.ms = 45000
kafka-1  | 	group.consumer.session.timeout.ms = 45000
kafka-1  | 	group.coordinator.new.enable = false
kafka-1  | 	group.coordinator.rebalance.protocols = [classic]
kafka-1  | 	group.coordinator.threads = 1
kafka-1  | 	group.initial.rebalance.delay.ms = 3000
kafka-1  | 	group.max.session.timeout.ms = 1800000
kafka-1  | 	group.max.size = 2147483647
kafka-1  | 	group.min.session.timeout.ms = 6000
kafka-1  | 	initial.broker.registration.timeout.ms = 60000
kafka-1  | 	inter.broker.listener.name = PLAINTEXT
kafka-1  | 	inter.broker.protocol.version = 3.7-IV4
kafka-1  | 	kafka.metrics.polling.interval.secs = 10
kafka-1  | 	kafka.metrics.reporters = []
kafka-1  | 	leader.imbalance.check.interval.seconds = 300
kafka-1  | 	leader.imbalance.per.broker.percentage = 10
kafka-1  | 	listener.security.protocol.map = CONTROLLER:PLAINTEXT,PLAINTEXT:PLAINTEXT
kafka-1  | 	listeners = PLAINTEXT://:9092,CONTROLLER://:9093
kafka-1  | 	log.cleaner.backoff.ms = 15000
kafka-1  | 	log.cleaner.dedupe.buffer.size = 134217728
kafka-1  | 	log.cleaner.delete.retention.ms = 86400000
kafka-1  | 	log.cleaner.enable = true
kafka-1  | 	log.cleaner.io.buffer.load.factor = 0.9
kafka-1  | 	log.cleaner.io.buffer.size = 524288
kafka-1  | 	log.cleaner.io.max.bytes.per.second = 1.7976931348623157E308
kafka-1  | 	log.cleaner.max.compaction.lag.ms = 9223372036854775807
kafka-1  | 	log.cleaner.min.cleanable.ratio = 0.5
kafka-1  | 	log.cleaner.min.compaction.lag.ms = 0
kafka-1  | 	log.cleaner.threads = 1
kafka-1  | 	log.cleanup.policy = [delete]
kafka-1  | 	log.dir = /tmp/kafka-logs
kafka-1  | 	log.dirs = /bitnami/kafka/data
kafka-1  | 	log.flush.interval.messages = 9223372036854775807
kafka-1  | 	log.flush.interval.ms = null
kafka-1  | 	log.flush.offset.checkpoint.interval.ms = 60000
kafka-1  | 	log.flush.scheduler.interval.ms = 9223372036854775807
kafka-1  | 	log.flush.start.offset.checkpoint.interval.ms = 60000
kafka-1  | 	log.index.interval.bytes = 4096
kafka-1  | 	log.index.size.max.bytes = 10485760
kafka-1  | 	log.local.retention.bytes = -2
kafka-1  | 	log.local.retention.ms = -2
kafka-1  | 	log.message.downconversion.enable = true
kafka-1  | 	log.message.format.version = 3.0-IV1
kafka-1  | 	log.message.timestamp.after.max.ms = 9223372036854775807
kafka-1  | 	log.message.timestamp.before.max.ms = 9223372036854775807
kafka-1  | 	log.message.timestamp.difference.max.ms = 9223372036854775807
kafka-1  | 	log.message.timestamp.type = CreateTime
kafka-1  | 	log.preallocate = false
kafka-1  | 	log.retention.bytes = -1
kafka-1  | 	log.retention.check.interval.ms = 300000
kafka-1  | 	log.retention.hours = 168
kafka-1  | 	log.retention.minutes = null
kafka-1  | 	log.retention.ms = null
kafka-1  | 	log.roll.hours = 168
kafka-1  | 	log.roll.jitter.hours = 0
kafka-1  | 	log.roll.jitter.ms = null
kafka-1  | 	log.roll.ms = null
kafka-1  | 	log.segment.bytes = 1073741824
kafka-1  | 	log.segment.delete.delay.ms = 60000
kafka-1  | 	max.connection.creation.rate = 2147483647
kafka-1  | 	max.connections = 2147483647
kafka-1  | 	max.connections.per.ip = 2147483647
kafka-1  | 	max.connections.per.ip.overrides = 
kafka-1  | 	max.incremental.fetch.session.cache.slots = 1000
kafka-1  | 	message.max.bytes = 1048588
kafka-1  | 	metadata.log.dir = null
kafka-1  | 	metadata.log.max.record.bytes.between.snapshots = 20971520
kafka-1  | 	metadata.log.max.snapshot.interval.ms = 3600000
kafka-1  | 	metadata.log.segment.bytes = 1073741824
kafka-1  | 	metadata.log.segment.min.bytes = 8388608
kafka-1  | 	metadata.log.segment.ms = 604800000
kafka-1  | 	metadata.max.idle.interval.ms = 500
kafka-1  | 	metadata.max.retention.bytes = 104857600
kafka-1  | 	metadata.max.retention.ms = 604800000
kafka-1  | 	metric.reporters = []
kafka-1  | 	metrics.num.samples = 2
kafka-1  | 	metrics.recording.level = INFO
kafka-1  | 	metrics.sample.window.ms = 30000
kafka-1  | 	min.insync.replicas = 1
kafka-1  | 	node.id = 0
kafka-1  | 	num.io.threads = 8
kafka-1  | 	num.network.threads = 3
kafka-1  | 	num.partitions = 1
kafka-1  | 	num.recovery.threads.per.data.dir = 1
kafka-1  | 	num.replica.alter.log.dirs.threads = null
kafka-1  | 	num.replica.fetchers = 1
kafka-1  | 	offset.metadata.max.bytes = 4096
kafka-1  | 	offsets.commit.required.acks = -1
kafka-1  | 	offsets.commit.timeout.ms = 5000
kafka-1  | 	offsets.load.buffer.size = 5242880
kafka-1  | 	offsets.retention.check.interval.ms = 600000
kafka-1  | 	offsets.retention.minutes = 10080
kafka-1  | 	offsets.topic.compression.codec = 0
kafka-1  | 	offsets.topic.num.partitions = 50
kafka-1  | 	offsets.topic.replication.factor = 1
kafka-1  | 	offsets.topic.segment.bytes = 104857600
kafka-1  | 	password.encoder.cipher.algorithm = AES/CBC/PKCS5Padding
kafka-1  | 	password.encoder.iterations = 4096
kafka-1  | 	password.encoder.key.length = 128
kafka-1  | 	password.encoder.keyfactory.algorithm = null
kafka-1  | 	password.encoder.old.secret = null
kafka-1  | 	password.encoder.secret = null
kafka-1  | 	principal.builder.class = class org.apache.kafka.common.security.authenticator.DefaultKafkaPrincipalBuilder
kafka-1  | 	process.roles = [controller, broker]
kafka-1  | 	producer.id.expiration.check.interval.ms = 600000
kafka-1  | 	producer.id.expiration.ms = 86400000
kafka-1  | 	producer.purgatory.purge.interval.requests = 1000
kafka-1  | 	queued.max.request.bytes = -1
kafka-1  | 	queued.max.requests = 500
kafka-1  | 	quota.window.num = 11
kafka-1  | 	quota.window.size.seconds = 1
kafka-1  | 	remote.log.index.file.cache.total.size.bytes = 1073741824
kafka-1  | 	remote.log.manager.task.interval.ms = 30000
kafka-1  | 	remote.log.manager.task.retry.backoff.max.ms = 30000
kafka-1  | 	remote.log.manager.task.retry.backoff.ms = 500
kafka-1  | 	remote.log.manager.task.retry.jitter = 0.2
kafka-1  | 	remote.log.manager.thread.pool.size = 10
kafka-1  | 	remote.log.metadata.custom.metadata.max.bytes = 128
kafka-1  | 	remote.log.metadata.manager.class.name = org.apache.kafka.server.log.remote.metadata.storage.TopicBasedRemoteLogMetadataManager
kafka-1  | 	remote.log.metadata.manager.class.path = null
kafka-1  | 	remote.log.metadata.manager.impl.prefix = rlmm.config.
kafka-1  | 	remote.log.metadata.manager.listener.name = null
kafka-1  | 	remote.log.reader.max.pending.tasks = 100
kafka-1  | 	remote.log.reader.threads = 10
kafka-1  | 	remote.log.storage.manager.class.name = null
kafka-1  | 	remote.log.storage.manager.class.path = null
kafka-1  | 	remote.log.storage.manager.impl.prefix = rsm.config.
kafka-1  | 	remote.log.storage.system.enable = false
kafka-1  | 	replica.fetch.backoff.ms = 1000
kafka-1  | 	replica.fetch.max.bytes = 1048576
kafka-1  | 	replica.fetch.min.bytes = 1
kafka-1  | 	replica.fetch.response.max.bytes = 10485760
kafka-1  | 	replica.fetch.wait.max.ms = 500
kafka-1  | 	replica.high.watermark.checkpoint.interval.ms = 5000
kafka-1  | 	replica.lag.time.max.ms = 30000
kafka-1  | 	replica.selector.class = null
kafka-1  | 	replica.socket.receive.buffer.bytes = 65536
kafka-1  | 	replica.socket.timeout.ms = 30000
kafka-1  | 	replication.quota.window.num = 11
kafka-1  | 	replication.quota.window.size.seconds = 1
kafka-1  | 	request.timeout.ms = 30000
kafka-1  | 	reserved.broker.max.id = 1000
kafka-1  | 	sasl.client.callback.handler.class = null
kafka-1  | 	sasl.enabled.mechanisms = [PLAIN, SCRAM-SHA-256, SCRAM-SHA-512]
kafka-1  | 	sasl.jaas.config = null
kafka-1  | 	sasl.kerberos.kinit.cmd = /usr/bin/kinit
kafka-1  | 	sasl.kerberos.min.time.before.relogin = 60000
kafka-1  | 	sasl.kerberos.principal.to.local.rules = [DEFAULT]
kafka-1  | 	sasl.kerberos.service.name = null
kafka-1  | 	sasl.kerberos.ticket.renew.jitter = 0.05
kafka-1  | 	sasl.kerberos.ticket.renew.window.factor = 0.8
kafka-1  | 	sasl.login.callback.handler.class = null
kafka-1  | 	sasl.login.class = null
kafka-1  | 	sasl.login.connect.timeout.ms = null
kafka-1  | 	sasl.login.read.timeout.ms = null
kafka-1  | 	sasl.login.refresh.buffer.seconds = 300
kafka-1  | 	sasl.login.refresh.min.period.seconds = 60
kafka-1  | 	sasl.login.refresh.window.factor = 0.8
kafka-1  | 	sasl.login.refresh.window.jitter = 0.05
kafka-1  | 	sasl.login.retry.backoff.max.ms = 10000
kafka-1  | 	sasl.login.retry.backoff.ms = 100
kafka-1  | 	sasl.mechanism.controller.protocol = GSSAPI
kafka-1  | 	sasl.mechanism.inter.broker.protocol = GSSAPI
kafka-1  | 	sasl.oauthbearer.clock.skew.seconds = 30
kafka-1  | 	sasl.oauthbearer.expected.audience = null
kafka-1  | 	sasl.oauthbearer.expected.issuer = null
kafka-1  | 	sasl.oauthbearer.jwks.endpoint.refresh.ms = 3600000
kafka-1  | 	sasl.oauthbearer.jwks.endpoint.retry.backoff.max.ms = 10000
kafka-1  | 	sasl.oauthbearer.jwks.endpoint.retry.backoff.ms = 100
kafka-1  | 	sasl.oauthbearer.jwks.endpoint.url = null
kafka-1  | 	sasl.oauthbearer.scope.claim.name = scope
kafka-1  | 	sasl.oauthbearer.sub.claim.name = sub
kafka-1  | 	sasl.oauthbearer.token.endpoint.url = null
kafka-1  | 	sasl.server.callback.handler.class = null
kafka-1  | 	sasl.server.max.receive.size = 524288
kafka-1  | 	security.inter.broker.protocol = PLAINTEXT
kafka-1  | 	security.providers = null
kafka-1  | 	server.max.startup.time.ms = 9223372036854775807
kafka-1  | 	socket.connection.setup.timeout.max.ms = 30000
kafka-1  | 	socket.connection.setup.timeout.ms = 10000
kafka-1  | 	socket.listen.backlog.size = 50
kafka-1  | 	socket.receive.buffer.bytes = 102400
kafka-1  | 	socket.request.max.bytes = 104857600
kafka-1  | 	socket.send.buffer.bytes = 102400
kafka-1  | 	ssl.allow.dn.changes = false
kafka-1  | 	ssl.allow.san.changes = false
kafka-1  | 	ssl.cipher.suites = []
kafka-1  | 	ssl.client.auth = none
kafka-1  | 	ssl.enabled.protocols = [TLSv1.2, TLSv1.3]
kafka-1  | 	ssl.endpoint.identification.algorithm = https
kafka-1  | 	ssl.engine.factory.class = null
kafka-1  | 	ssl.key.password = null
kafka-1  | 	ssl.keymanager.algorithm = SunX509
kafka-1  | 	ssl.keystore.certificate.chain = null
kafka-1  | 	ssl.keystore.key = null
kafka-1  | 	ssl.keystore.location = null
kafka-1  | 	ssl.keystore.password = null
kafka-1  | 	ssl.keystore.type = JKS
kafka-1  | 	ssl.principal.mapping.rules = DEFAULT
kafka-1  | 	ssl.protocol = TLSv1.3
kafka-1  | 	ssl.provider = null
kafka-1  | 	ssl.secure.random.implementation = null
kafka-1  | 	ssl.trustmanager.algorithm = PKIX
kafka-1  | 	ssl.truststore.certificates = null
kafka-1  | 	ssl.truststore.location = null
kafka-1  | 	ssl.truststore.password = null
kafka-1  | 	ssl.truststore.type = JKS
kafka-1  | 	telemetry.max.bytes = 1048576
kafka-1  | 	transaction.abort.timed.out.transaction.cleanup.interval.ms = 10000
kafka-1  | 	transaction.max.timeout.ms = 900000
kafka-1  | 	transaction.partition.verification.enable = true
kafka-1  | 	transaction.remove.expired.transaction.cleanup.interval.ms = 3600000
kafka-1  | 	transaction.state.log.load.buffer.size = 5242880
kafka-1  | 	transaction.state.log.min.isr = 1
kafka-1  | 	transaction.state.log.num.partitions = 50
kafka-1  | 	transaction.state.log.replication.factor = 1
kafka-1  | 	transaction.state.log.segment.bytes = 104857600
kafka-1  | 	transactional.id.expiration.ms = 604800000
kafka-1  | 	unclean.leader.election.enable = false
kafka-1  | 	unstable.api.versions.enable = false
kafka-1  | 	unstable.metadata.versions.enable = false
kafka-1  | 	zookeeper.clientCnxnSocket = null
kafka-1  | 	zookeeper.connect = null
kafka-1  | 	zookeeper.connection.timeout.ms = null
kafka-1  | 	zookeeper.max.in.flight.requests = 10
kafka-1  | 	zookeeper.metadata.migration.enable = false
kafka-1  | 	zookeeper.metadata.migration.min.batch.size = 200
kafka-1  | 	zookeeper.session.timeout.ms = 18000
kafka-1  | 	zookeeper.set.acl = false
kafka-1  | 	zookeeper.ssl.cipher.suites = null
kafka-1  | 	zookeeper.ssl.client.enable = false
kafka-1  | 	zookeeper.ssl.crl.enable = false
kafka-1  | 	zookeeper.ssl.enabled.protocols = null
kafka-1  | 	zookeeper.ssl.endpoint.identification.algorithm = HTTPS
kafka-1  | 	zookeeper.ssl.keystore.location = null
kafka-1  | 	zookeeper.ssl.keystore.password = null
kafka-1  | 	zookeeper.ssl.keystore.type = null
kafka-1  | 	zookeeper.ssl.ocsp.enable = false
kafka-1  | 	zookeeper.ssl.protocol = TLSv1.2
kafka-1  | 	zookeeper.ssl.truststore.location = null
kafka-1  | 	zookeeper.ssl.truststore.password = null
kafka-1  | 	zookeeper.ssl.truststore.type = null
kafka-1  |  (kafka.server.KafkaConfig)
kafka-1  | [2024-06-09 07:41:17,962] INFO [BrokerServer id=0] Waiting for the broker to be unfenced (kafka.server.BrokerServer)
kafka-1  | [2024-06-09 07:41:17,963] INFO [QuorumController id=0] The request from broker 0 to unfence has been granted because it has caught up with the offset of its register broker record 32. (org.apache.kafka.controller.BrokerHeartbeatManager)
kafka-1  | [2024-06-09 07:41:17,965] INFO [QuorumController id=0] Replayed BrokerRegistrationChangeRecord modifying the registration for broker 0: BrokerRegistrationChangeRecord(brokerId=0, brokerEpoch=32, fenced=-1, inControlledShutdown=0, logDirs=[]) (org.apache.kafka.controller.ClusterControlManager)
kafka-1  | [2024-06-09 07:41:17,992] INFO [BrokerLifecycleManager id=0] The broker has been unfenced. Transitioning from RECOVERY to RUNNING. (kafka.server.BrokerLifecycleManager)
kafka-1  | [2024-06-09 07:41:17,992] INFO [BrokerServer id=0] Finished waiting for the broker to be unfenced (kafka.server.BrokerServer)
kafka-1  | [2024-06-09 07:41:17,993] INFO authorizerStart completed for endpoint PLAINTEXT. Endpoint is now READY. (org.apache.kafka.server.network.EndpointReadyFutures)
kafka-1  | [2024-06-09 07:41:17,993] INFO [SocketServer listenerType=BROKER, nodeId=0] Enabling request processing. (kafka.network.SocketServer)
kafka-1  | [2024-06-09 07:41:17,993] INFO Awaiting socket connections on 0.0.0.0:9092. (kafka.network.DataPlaneAcceptor)
kafka-1  | [2024-06-09 07:41:17,993] INFO [BrokerServer id=0] Waiting for all of the authorizer futures to be completed (kafka.server.BrokerServer)
kafka-1  | [2024-06-09 07:41:17,993] INFO [BrokerServer id=0] Finished waiting for all of the authorizer futures to be completed (kafka.server.BrokerServer)
kafka-1  | [2024-06-09 07:41:17,993] INFO [BrokerServer id=0] Waiting for all of the SocketServer Acceptors to be started (kafka.server.BrokerServer)
kafka-1  | [2024-06-09 07:41:17,993] INFO [BrokerServer id=0] Finished waiting for all of the SocketServer Acceptors to be started (kafka.server.BrokerServer)
kafka-1  | [2024-06-09 07:41:17,993] INFO [BrokerServer id=0] Transition from STARTING to STARTED (kafka.server.BrokerServer)
kafka-1  | [2024-06-09 07:41:17,994] INFO Kafka version: 3.7.0 (org.apache.kafka.common.utils.AppInfoParser)
kafka-1  | [2024-06-09 07:41:17,994] INFO Kafka commitId: 2ae524ed625438c5 (org.apache.kafka.common.utils.AppInfoParser)
kafka-1  | [2024-06-09 07:41:17,994] INFO Kafka startTimeMs: 1717918877993 (org.apache.kafka.common.utils.AppInfoParser)
kafka-1  | [2024-06-09 07:41:17,995] INFO [KafkaRaftServer nodeId=0] Kafka Server started (kafka.server.KafkaRaftServer)
```

# 테스트

매우 긴 로그들이 생성되었는데, 아무튼 실행은 된 것 같다. 다른 쉘에서 상태를 체크해봤다.

```sh
 sudo docker container ls
CONTAINER ID   IMAGE           COMMAND                  CREATED         STATUS         PORTS                                       NAMES
0868aaa976bd   bitnami/kafka   "/opt/bitnami/script…"   4 minutes ago   Up 3 minutes   0.0.0.0:9092->9092/tcp, :::9092->9092/tcp   docker-kafka-1
```

9092 포트로 맵핑되어 있다.

컨테이너 안에선 `/opt/bitnami/kafka/bin` 내부에 api 들이 쉘 스크립트로 들어있다.
```sh
 sudo docker compose exec kafka bash   

I have no name!@0868aaa976bd:/$ ls opt/bitnami/kafka/bin
connect-distributed.sh	      kafka-dump-log.sh		     kafka-server-stop.sh
connect-mirror-maker.sh       kafka-e2e-latency.sh	     kafka-storage.sh
connect-plugin-path.sh	      kafka-features.sh		     kafka-streams-application-reset.sh
connect-standalone.sh	      kafka-get-offsets.sh	     kafka-topics.sh
kafka-acls.sh		      kafka-jmx.sh		     kafka-transactions.sh
kafka-broker-api-versions.sh  kafka-leader-election.sh	     kafka-verifiable-consumer.sh
kafka-client-metrics.sh       kafka-log-dirs.sh		     kafka-verifiable-producer.sh
kafka-cluster.sh	      kafka-metadata-quorum.sh	     trogdor.sh
kafka-configs.sh	      kafka-metadata-shell.sh	     windows
kafka-console-consumer.sh     kafka-mirror-maker.sh	     zookeeper-security-migration.sh
kafka-console-producer.sh     kafka-producer-perf-test.sh    zookeeper-server-start.sh
kafka-consumer-groups.sh      kafka-reassign-partitions.sh   zookeeper-server-stop.sh
kafka-consumer-perf-test.sh   kafka-replica-verification.sh  zookeeper-shell.sh
kafka-delegation-tokens.sh    kafka-run-class.sh
kafka-delete-records.sh       kafka-server-start.sh
```

컨테이너 밖에서 토픽 생성
```sh
 sudo docker compose exec kafka kafka-topics.sh --create --topic my-topic --bootstrap-server kafka:9092 --replication-factor 1 --partitions 1
Created topic my-topic.
```

마찬가지로 토픽 확인.
```sh
 sudo docker compose exec kafka kafka-topics.sh --list --bootstrap-server kafka:9092
my-topic
```

프로듀서 콘솔로 메세지를 보내보자...
```sh
 sudo docker compose exec kafka kafka-console-producer.sh --topic my-topic --bootstrap-server kafka:9092
>hello world!
>
```

오프셋을 직접 확인해 볼 수도 있다.
```sh
 sudo docker compose exec kafka kafka-get-offsets.sh --bootstrap-server kafka:9092
my-topic:0:1
```

아직 아무도 읽지 않았으니 오프셋은 0이다.

컨슘을 해봅시다.
```sh
 sudo docker compose exec kafka kafka-console-producer.sh --topic my-topic --bootstrap-server kafka:9092
>hello world!
>are you listening?
>hello world is not consumed...!

 sudo docker compose exec kafka kafka-console-consumer.sh --topic my-topic --bootstrap-server kafka:9092
are you listening?
hello world is not consumed...!
```

컨슈머가 없었을 때 메세지가 오지 않았는데...


어... 오프셋을 확인해보는데 뭔지 모르겠다.
```sh
 sudo docker compose exec kafka kafka-get-offsets.sh --bootstrap-server kafka:9092                      
__consumer_offsets:0:0
__consumer_offsets:1:0
__consumer_offsets:10:0
__consumer_offsets:11:0
__consumer_offsets:12:0
__consumer_offsets:13:0
__consumer_offsets:14:0
__consumer_offsets:15:0
__consumer_offsets:16:0
__consumer_offsets:17:0
__consumer_offsets:18:0
__consumer_offsets:19:0
__consumer_offsets:2:0
__consumer_offsets:20:0
__consumer_offsets:21:0
__consumer_offsets:22:0
__consumer_offsets:23:0
__consumer_offsets:24:0
__consumer_offsets:25:0
__consumer_offsets:26:0
__consumer_offsets:27:0
__consumer_offsets:28:0
__consumer_offsets:29:0
__consumer_offsets:3:0
__consumer_offsets:30:0
__consumer_offsets:31:0
__consumer_offsets:32:0
__consumer_offsets:33:0
__consumer_offsets:34:0
__consumer_offsets:35:0
__consumer_offsets:36:0
__consumer_offsets:37:0
__consumer_offsets:38:0
__consumer_offsets:39:0
__consumer_offsets:4:0
__consumer_offsets:40:0
__consumer_offsets:41:0
__consumer_offsets:42:0
__consumer_offsets:43:0
__consumer_offsets:44:0
__consumer_offsets:45:0
__consumer_offsets:46:0
__consumer_offsets:47:0
__consumer_offsets:48:0
__consumer_offsets:49:0
__consumer_offsets:5:0
__consumer_offsets:6:2
__consumer_offsets:7:0
__consumer_offsets:8:0
__consumer_offsets:9:0
my-topic:0:3
```


