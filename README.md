# azure-streaminganalytics-SQLdb-PowerBi-Grafana-tutorial

This tutorial is a simple step by step instruction to reach the following goals:

*   Configure Microsoft Azure Streaming Analytics with Azure SQL
*   Get the data into Microsoft Power BI and Grafana

## Step 1

**Prerequisite:**

*   Successful completion of the following tutorial: [kafka-mirrormaker-azure-tutorial](https://github.com/Darwin1972/kafka-mirrormaker-azure-tutorial)

## Step 2

**Create and configure Azure SQL:**

Go to your Microsoft Azure subscription.

Create a resource

![](https://user-images.githubusercontent.com/51634515/109393880-78f46c00-7924-11eb-81bd-7cc997f3ed1c.png)

![](https://user-images.githubusercontent.com/51634515/109393912-988b9480-7924-11eb-8f28-19e436e78a04.png)

![](https://user-images.githubusercontent.com/51634515/109393922-a5a88380-7924-11eb-8b85-0ae5bc8f5729.png)

Create

![](https://user-images.githubusercontent.com/51634515/109393945-bf49cb00-7924-11eb-9d24-4c34a3155a69.png)

Select SQL databases / Resource type: Single database.

Create

![](https://user-images.githubusercontent.com/51634515/109394004-02a43980-7925-11eb-8714-7fa8f28ff6ca.png)

Server\*: Create new

Enter server name (mysqlsever1968), server admin login and password:

![](https://user-images.githubusercontent.com/51634515/109394029-2a939d00-7925-11eb-82b8-02e3fc27a2da.png)

OK

![](https://user-images.githubusercontent.com/51634515/109394093-79413700-7925-11eb-9b68-a74aecef3c9d.png)

Configure database

Chose serverless and data max size 1GB:

![](https://user-images.githubusercontent.com/51634515/109394130-ad1c5c80-7925-11eb-8497-d760e7de5e07.png)

![](https://user-images.githubusercontent.com/51634515/109394151-cae9c180-7925-11eb-9830-d542057fbcc3.png)

Apply

![](https://user-images.githubusercontent.com/51634515/109394170-e2c14580-7925-11eb-89bd-b3bac2a569c9.png)

Next: Networking >

Choose:

*   Connectivity method: Public endpoint
*   Allow Azure services and resources to access this server = yes
*   Add current client IP address = yes

![](https://user-images.githubusercontent.com/51634515/109394185-f9679c80-7925-11eb-8242-326afe4f3f08.png)

Next : Additional settings > 

Chose:

*   Use existing data: Sample
*   Enable Azure Defender for SQL: Not now

![](https://user-images.githubusercontent.com/51634515/109394261-654a0500-7926-11eb-885a-eff1b4b6f646.png)

Review + create, Create

![](https://user-images.githubusercontent.com/51634515/109394361-e4d7d400-7926-11eb-94d8-2a0ebad9a212.png)

Go to resource

## Step 3

**Create and configure Azure Streaming Analytics.**

![](https://user-images.githubusercontent.com/51634515/109394381-02a53900-7927-11eb-9385-66c9a996d604.png)

![](https://user-images.githubusercontent.com/51634515/109394393-1a7cbd00-7927-11eb-8915-8671bf88e799.png)

Create

Enter job name: mysqlstreaming123

![](https://user-images.githubusercontent.com/51634515/109394426-3da76c80-7927-11eb-9df2-f6e6e54d9ee7.png)

Next: Input >

Please make sure you have  tutorial completed the following tutoral: [kafka-mirrormaker-azure-tutorial](https://github.com/Darwin1972/kafka-mirrormaker-azure-tutorial)

Configure:

*   Input type: Event Hub
*   Event Hub namespace: kafkaazure
*   Event Hub name: mymachine
*   Event Hub policy name: Create new
*   Event Hub consumer group: Use existing

![](https://user-images.githubusercontent.com/51634515/109394470-734c5580-7927-11eb-9858-b1a8ef448786.png)

Next: Output

Enter username and password from Step 2.

Validate:

![](https://user-images.githubusercontent.com/51634515/109394701-9c211a80-7928-11eb-8834-00a1db39a8c8.png)

Table: Create new

mymachine

![](https://user-images.githubusercontent.com/51634515/109394747-d8ed1180-7928-11eb-8b54-b235828b3f96.png)

Create

Enter the following value into the **Kafka producer on Ubuntu 20.04:**

{"sensor\_id": 1,"ltime": 1613204245,"temp": 5.5,"status": 1}

{"sensor\_id": 1,"ltime": 1613204245,"temp": 6.5,"status": 1}

{"sensor\_id": 1,"ltime": 1613204245,"temp": 7.5,"status": 1}

![](https://user-images.githubusercontent.com/51634515/109394896-a5f74d80-7929-11eb-8cc3-be479cc8444d.png)

![](https://user-images.githubusercontent.com/51634515/109394961-2322c280-792a-11eb-8c53-462ecda32821.png)

Start streaming analytics job:

![](https://user-images.githubusercontent.com/51634515/109394843-6c264700-7929-11eb-9038-b1781b00e9df.png)

![](https://user-images.githubusercontent.com/51634515/109394975-36ce2900-792a-11eb-82af-9c2ba629030b.png)

Start

![](https://user-images.githubusercontent.com/51634515/109395062-a8a67280-792a-11eb-9efa-309bd857f749.png)

## Step 4

**Validate streaming analytics job with SQL database query editor.**

![](https://user-images.githubusercontent.com/51634515/109395070-b825bb80-792a-11eb-833b-9f72bca02530.png)

Query editor

![](https://user-images.githubusercontent.com/51634515/109395095-d4c1f380-792a-11eb-9151-bef20b680684.png)

Enter SQL server authentication login and password from Step 2.

OK

Enter the following value into the **Kafka producer on Ubuntu 20.04:**

{"sensor\_id": 1,"ltime": 1613204245,"temp": 5.5,"status": 1}

{"sensor\_id": 1,"ltime": 1614448017,"temp": 6.5,"status": 1}

{"sensor\_id": 1,"ltime": 1614448093,"temp": 7.5,"status": 1}

![](https://user-images.githubusercontent.com/51634515/109395423-90375780-792c-11eb-8d73-39a18d4ab445.png)

Then run the following SQL statement: SELECT \* FROM \[dbo\].\[mymachine\];

You should see the following results:

![](https://user-images.githubusercontent.com/51634515/109395437-a2b19100-792c-11eb-9de7-084eea07af00.png)

## Step 5
