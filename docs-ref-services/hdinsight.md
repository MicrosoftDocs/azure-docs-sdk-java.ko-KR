---
title: Azure HDInsight Java SDK
description: Azure HDInsight Java SDK 참조 HDInsight Java SDK는 HDInsight 클러스터 관리를 위한 클래스 및 메서드를 제공합니다.
author: tylerfox
ms.author: tyfox
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: reference
ms.devlang: java
ms.date: 9/20/2018
ms.openlocfilehash: 9fd35d12e0aa864b5d23cf03547f7b76dc74c677
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799899"
---
# <a name="hdinsight-java-management-sdk-preview"></a>HDInsight Java 관리 SDK 미리 보기

## <a name="overview"></a>개요

HDInsight Java SDK는 HDInsight 클러스터 관리를 위한 클래스 및 메서드를 제공합니다. 여기에는 HDInsight 클러스터의 속성 만들기, 삭제, 업데이트, 나열, 크기 조정, 스크립트 작업 실행, 모니터링, 가져오기 작업을 포함합니다.

## <a name="prerequisites"></a>필수 조건

* Azure 계정. 계정이 없으면 [체험 계정을 얻습니다](https://azure.microsoft.com/free/).
* [Java JDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html)
* [Maven](https://maven.apache.org/install.html)

## <a name="sdk-installation"></a>SDK 설치

HDInsight Java SDK는 Maven [여기](https://mvnrepository.com/artifact/com.microsoft.azure.hdinsight.v2018_06_01_preview/azure-mgmt-hdinsight)을 통해 사용할 수 있습니다. pom.xml에 다음 종속성을 추가합니다.

```
<dependency>
    <groupId>com.microsoft.azure.hdinsight.v2018_06_01_preview</groupId>
    <artifactId>azure-mgmt-hdinsight</artifactId>
    <version>1.0.0-beta-1</version>
</dependency>
```

또한 pom.xml 파일에 다음 종속성을 추가합니다.

* [Azure 클라이언트 인증 라이브러리:](https://mvnrepository.com/artifact/com.microsoft.azure/azure-client-authentication/1.6.2)
  ```
  <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-client-authentication</artifactId>
    <version>1.6.2</version>
    <scope>test</scope>
  </dependency>
  ```

* [ARM용 Azure Java 클라이언트 런타임:](https://mvnrepository.com/artifact/com.microsoft.azure/azure-arm-client-runtime/1.6.2)
  ```
  <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-arm-client-runtime</artifactId>
    <version>1.6.2</version>
  </dependency>
  ```

## <a name="authentication"></a>인증

Azure 구독을 사용해서 SDK를 먼저 인증해야 합니다.  아래 예제에 따라 서비스 주체를 만들고 이를 인증에 사용합니다. 완료되었으면 관리 작업 수행을 위해 사용할 수 있는 여러 메서드(아래 섹션 참조)가 포함된 `HDInsightManagementClientImpl` 인스턴스가 준비됩니다.

> [!NOTE]
> 아래 설명된 예제 외에도 사용자 요구에 더 적합할 수 있는 다른 인증 방법이 있습니다. 모든 메서드는 여기에 설명되어 있습니다: [Java용 Azure 관리 라이브러리로 인증](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-authenticate?view=azure-java-stable)

### <a name="authentication-example-using-a-service-principal"></a>서비스 주체를 사용한 인증 예제

먼저, [Azure Cloud Shell](https://shell.azure.com/bash)에 로그인합니다. 서비스 주체를 만들려는 구독을 현재 사용하고 있는지 확인합니다. 

```azurecli-interactive
az account show
```

구독 정보는 JSON으로 표시됩니다.

```json
{
  "environmentName": "AzureCloud",
  "id": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "isDefault": true,
  "name": "XXXXXXX",
  "state": "Enabled",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "user": {
    "cloudShellID": true,
    "name": "XXX@XXX.XXX",
    "type": "user"
  }
}
```

올바른 구독으로 로그인되지 않은 경우 다음을 실행하여 올바른 구독을 선택합니다. 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> Azure Portal을 통해 HDInsight Cluster를 만드는 등 다른 방법을 사용해서 HDInsight Resource Provider를 등록하지 않은 경우, 이를 먼저 수행해야 인증할 수 있습니다. 이 작업은 [Azure Cloud Shell](https://shell.azure.com/bash)에서 다음 명령을 실행하여 수행할 수 있습니다.
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

그런 다음 서비스 주체 이름을 선택하고 다음 명령을 사용해서 만듭니다.

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

서비스 주체 정보는 JSON으로 표시됩니다.

```json
{
  "clientId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "clientSecret": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "subscriptionId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```
아래 코드 조각을 복사하고 서비스 주체를 만들기 위해 명령을 실행한 후 반환된 JSON 문자열을 `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` 및 `SUBSCRIPTION_ID`에 채웁니다.

```java
import com.microsoft.azure.management.hdinsight.v2018_06_01_preview.*;
import com.microsoft.azure.management.hdinsight.v2018_06_01_preview.implementation.HDInsightManagementClientImpl;

public class Main {
    public static void main (String[] args) {

        // Tenant ID for your Azure Subscription
        String TENANT_ID = "";
        // Your Service Principal App Client ID
        String CLIENT_ID = "";
        // Your Service Principal Client Secret
        String CLIENT_SECRET = "";
        // Azure Subscription ID
        String SUBSCRIPTION_ID = "";

        ApplicationTokenCredentials credentials = new ApplicationTokenCredentials(
                CLIENT_ID,
                TENANT_ID,
                CLIENT_SECRET,
                AzureEnvironment.AZURE);

        HDInsightManagementClientImpl client = new HDInsightManagementClientImpl(credentials);
```


## <a name="cluster-management"></a>클러스터 관리

> [!NOTE]
> 이 섹션에서는 이미 인증이 수행되었고 `HDInsightManagementClientImpl` 인스턴스가 생성되었으며, `client`라는 변수로 저장되었다고 가정합니다. `HDInsightManagementClientImpl` 인증 및 가져오기 지침은 위에 표시된 인증 섹션에서 찾을 수 있습니다.

### <a name="create-a-cluster"></a>클러스터 만들기

`client.clusters().create()`을(를) 호출하여 새 클러스터를 만들 수 있습니다.

#### <a name="example"></a>예

이 예제에서는 2개의 헤드 노드 및 1개의 작업자 노드를 사용하여 Spark 클러스터를 만드는 방법을 보여줍니다.

> [!NOTE]
> 먼저 아래 설명된 대로 리소스 그룹 및 저장소 계정을 만들어야 합니다. 이미 만든 경우에는 이 단계를 건너뛸 수 있습니다.

##### <a name="creating-a-resource-group"></a>리소스 그룹 만들기

다음을 실행하여 [Azure Cloud Shell](https://shell.azure.com/bash)을 사용해서 리소스 그룹을 만들 수 있습니다.
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a>저장소 계정 만들기

다음을 실행하여 [Azure Cloud Shell](https://shell.azure.com/bash)을 사용해서 저장소 계정을 만들 수 있습니다.
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
이제 다음 명령을 사용해서 저장소 계정에 대한 키를 가져옵니다(클러스터를 만들기 위해 필요).
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
아래의 Java 코드 조각은 2개의 헤드 노드 및 1개의 작업자 노드를 사용해서 Spark 클러스터를 만듭니다. 주석 설명에 따라 빈 변수를 채우고 특정 요구에 따라 다른 매개변수를 변경합니다.

```java
// The name for the cluster you are creating
String clusterName = "";
// The name of your existing Resource Group
String resourceGroupName = "";
// Choose a username
String username = "";
// Choose a password
String password = "";
// Replace <> with the name of your storage account
String storageAccount = "<>.blob.core.windows.net";
// Storage account key you obtained above
String storageAccountKey = "";
// Choose a region
String location = "";
String container = "default";

HashMap<String, HashMap<String, String>> configurations = new HashMap<String, HashMap<String, String>>();
        HashMap<String, String> gateway = new HashMap<String, String>();
        gateway.put("restAuthCredential.enabled_credential", "True");
        gateway.put("restAuthCredential.username", username);
        gateway.put("restAuthCredential.password", password);
        configurations.put("gateway", gateway);

        ClusterCreateParametersExtended parameters = new ClusterCreateParametersExtended()
            .withLocation(location)
            .withTags(Collections.EMPTY_MAP)
            .withProperties(
                new ClusterCreateProperties()
                    .withClusterVersion("3.6")
                    .withOsType(OSType.LINUX)
                    .withClusterDefinition(new ClusterDefinition()
                            .withKind("spark")
                            .withConfigurations(configurations)
                    )
                    .withTier(Tier.STANDARD)
                    .withComputeProfile(new ComputeProfile()
                        .withRoles(List.of(
                            new Role()
                                .withName("headnode")
                                .withTargetInstanceCount(2)
                                .withHardwareProfile(new HardwareProfile()
                                    .withVmSize("Large")
                                )
                                .withOsProfile(new OsProfile()
                                    .withLinuxOperatingSystemProfile(new LinuxOperatingSystemProfile()
                                            .withUsername(username)
                                            .withPassword(password)
                                    )
                                ),
                            new Role()
                                    .withName("workernode")
                                    .withTargetInstanceCount(1)
                                    .withHardwareProfile(new HardwareProfile()
                                        .withVmSize("Large")
                                    )
                                    .withOsProfile(new OsProfile()
                                        .withLinuxOperatingSystemProfile(new LinuxOperatingSystemProfile()
                                            .withUsername(username)
                                            .withPassword(password)
                                        )
                                    )
                        ))
                    )
                    .withStorageProfile(new StorageProfile()
                        .withStorageaccounts(List.of(
                                new StorageAccount()
                                    .withName(storageAccount)
                                    .withKey(storageAccountKey)
                                    .withContainer(container)
                                    .withIsDefault(true)
                        ))
                    )
            );
        client.clusters().create(resourceGroupName, clusterName, parameters);
```

### <a name="get-cluster-details"></a>클러스터 세부 정보 가져오기

지정된 클러스터에 대한 속성을 가져오려면:

```java
client.clusters.getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>예

`get`을(를) 사용하여 클러스터 만들기가 성공했는지 확인할 수 있습니다.

```java
ClusterInner cluster = client.clusters().getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
System.out.println(cluster.name()); //Prints the name of the cluster
System.out.println(cluster.id()); //Prints the resource Id of the cluster
```

출력은 다음과 같습니다.

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```

### <a name="list-clusters"></a>클러스터 나열

#### <a name="list-clusters-under-the-subscription"></a>구독 아래에 클러스터 나열

```java
client.clusters.list();
```
#### <a name="list-clusters-by-resource-group"></a>리소스 그룹별로 클러스터 나열

```java
client.clusters.listByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> `List()` 및 `ListByResourceGroup()` 모두 `PagedList<ClusterInner>` 개체를 반환합니다. `loadNext()`를 호출하면 해당 페이지의 클러스터 목록이 반환되고 `ClusterPaged` 개체가 다음 페이지로 이동합니다. `hasNextPage()`가 `false`를 반환할 때까지 반복할 수 있으며, 더 이상 페이지가 없음을 나타냅니다.

#### <a name="example"></a>예

다음 예제는 현재 구독에 대해 모든 클러스터 속성을 출력합니다.

```java
PagedList<ClusterInner> clusterPages = client.clusters().list();
while (true) {
    for (ClusterInner cluster : clusterPages.currentPage().items()) {
        System.out.println(cluster.name());
    }
    if (clusterPages.hasNextPage()) {
        clusterPages.loadNextPage();
    } else {
        break;
    }
}
```

### <a name="delete-a-cluster"></a>클러스터 삭제

클러스터를 삭제하려면:

```java
client.clusters.delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a>클러스터 태그 업데이트

지정된 클러스터의 태그를 다음과 같이 업데이트할 수 있습니다.

```java
client.clusters.update("<Resource Group Name>", "<Cluster Name>", <Map<String,String> of Tags>);
```

### <a name="resize-cluster"></a>클러스터 크기 조정

새 크기를 지정하여 작업자 노드의 지정된 클러스터 번호를 크기 조정할 수 있습니다.

```java
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a>클러스터 모니터링

또한 HDInsight 관리 SDK를 사용하여 OMS(Operations Management Suite)를 통해 클러스터에서 모니터링을 관리할 수 있습니다.

### <a name="enable-oms-monitoring"></a>OMS 모니터링 사용

> [!NOTE]
> OMS 모니터링을 사용하려면 기존 Log Analytics 작업 영역이 있어야 합니다. 아직 만들지 않았으면 [Azure Portal에서 Log Analytics 작업 영역 만들기](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace)에서 이를 수행하는 방법을 확인할 수 있습니다.

클러스터에서 OMS 모니터링을 사용하려면:

```java
client.extensions().enableMonitoring("<Resource Group Name", "<Cluster Name>", new ClusterMonitoringRequest().withWorkspaceId("<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a>OMS 모니터링의 상태 보기

클러스터에서 OMS 상태를 가져오려면:

```java
client.extensions().getMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a>OMS 모니터링 사용 안 함

클러스터에서 OMS를 사용하지 않으려면:

```java
client.extensions().disableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a>스크립트 동작

HDInsight는 클러스터 사용자 지정을 위해 사용자 지정 스크립트를 호출하는 스크립트 작업이라고 부르는 구성 메서드를 제공합니다.
> [!NOTE]
> 스크립트 작업 사용 방법에 대한 자세한 내용은 [스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)에서 확인할 수 있습니다.

### <a name="execute-script-actions"></a>스크립트 작업 실행

지정된 클러스터에서 다음과 같이 스크립트 작업을 실행할 수 있습니다.

```java
RuntimeScriptAction scriptAction1 = new RuntimeScriptAction()
    .withName("<Script Name>")
    .withUri("<URL To Script>")
    .withRoles(<List<String> of roles>);
client.clusters().executeScriptActions(
    resourceGroupName, 
    clusterName, 
    new ExecuteScriptActionParameters().withPersistOnSuccess(false).withScriptActions(new LinkedList<>(Arrays.asList(scriptAction1)))); //add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a>스크립트 작업 삭제

지정된 클러스터에서 지정된 지속형 스크립트 작업을 삭제하려면:

```java
client.scriptActions().delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a>지속형 스크립트 작업 나열

> [!NOTE]
> `listByCluster()` 둘 다 `PagedList<RuntimeScriptActionDetailInner>` 개체를 반환합니다. `currentPage().items()`를 호출하면 `RuntimeScriptActionDetailInner`의 목록이 반환되고 `loadNextPage()`은 다음 페이지로 넘어갑니다. `hasNextPage()`가 `false`를 반환할 때까지 반복할 수 있으며, 더 이상 페이지가 없음을 나타냅니다.

지정된 클러스터에 대해 모든 지속형 스크립트 작업을 나열하려면:
```java
client.scriptActions().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>예

```java
PagedList<RuntimeScriptActionDetailInner> scriptsPaged = client.scriptActions().listByCluster(resourceGroupName, clusterName);
while (true) {
    for (RuntimeScriptActionDetailInner script : scriptsPaged.currentPage().items()) {
        System.out.println(script.name()); //There are methods to get other properties of RuntimeScriptActionDetail besides name(), such as status(), operation(), startTime(), endTime(), etc. See reference documentation.
    }
    if (scriptsPaged.hasNextPage()) {
        scriptsPaged.loadNextPage();
    } else {
        break;
    }
}
```

### <a name="list-all-scripts-execution-history"></a>모든 스크립트 실행 기록 나열

지정된 클러스터에 대해 모든 스크립트 실행 기록을 나열하려면:

```java
client.scriptExecutionHistorys().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>예

이 예제는 모든 과거 스크립트 실행에 대한 모든 세부 정보를 출력합니다.

```java
PagedList<RuntimeScriptActionDetailInner> scriptExecutionsPaged = client.scriptExecutionHistorys().listByCluster(resourceGroupName, clusterName);
while (true) {
    for (RuntimeScriptActionDetailInner script : scriptExecutionsPaged.currentPage().items()) {
        System.out.println(script.name()); //There are methods to get other properties of RuntimeScriptActionDetail besides name(), such as status(), operation(), startTime(), endTime(), etc. See reference documentation.
    }
    if (scriptExecutionsPaged.hasNextPage()) {
        scriptExecutionsPaged.loadNextPage();
    } else {
        break;
    }
}
```
