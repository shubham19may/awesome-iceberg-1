# Awesome Iceberg

A curated catalog of the **Apache Iceberg** ecosystem — spec, catalogs, engines, table services, cloud offerings, and learning paths.

Sibling to [Audie-glitch/awesome-lakehouse](https://github.com/Audie-glitch/awesome-lakehouse) (multi-format lakehouse). This list goes **Iceberg-deep**. Broader than [e6data/awesome-optimizing-iceberg-tables](https://github.com/e6data/awesome-optimizing-iceberg-tables) (compaction/tuning focus). Inspired by how [public-apis](https://github.com/public-apis/public-apis) keeps rows short and links honest. Every blurb here is original.

PRs welcome: one link + 1–2 sentences you wrote. No star-farming.

## Index

- [Official](#official)
- [Spec / format docs](#spec--format-docs)
- [Catalogs](#catalogs)
- [Engines & connectors](#engines--connectors)
- [Tools](#tools)
- [Cloud services](#cloud-services)
- [Learning](#learning)
- [Related](#related)
- [Contributing](#contributing)

## Official

Project home, reference implementation, and language clients.

| Link | Notes |
|------|--------|
| [iceberg.apache.org](https://iceberg.apache.org/) | Project site: docs hub, vendor list, community entry points |
| [apache/iceberg](https://github.com/apache/iceberg) | Reference Java implementation, Spark/Flink modules, and ASF release trains |
| [Docs (latest)](https://iceberg.apache.org/docs/latest/) | User-facing concepts: snapshots, manifests, hidden partitioning, time travel |
| [Multi-engine support](https://iceberg.apache.org/multi-engine-support/) | Which engines read/write which Iceberg features |
| [Integrations](https://iceberg.apache.org/integrations/) | Cataloged integrations (engines, catalogs, tools) maintained with the project |
| [Vendors](https://iceberg.apache.org/vendors/) | Commercial products that ship first-class Iceberg support |
| [Releases](https://iceberg.apache.org/releases/) | Version notes and download pointers |
| [Community](https://iceberg.apache.org/community/) | Mailing lists, Slack/Zulip, meeting cadence |
| [Contribute](https://iceberg.apache.org/contribute/) | How to propose changes and land PRs |
| [PyIceberg](https://py.iceberg.apache.org/) | Python client for catalog ops, scan planning, and commits without a JVM job |
| [iceberg-python](https://github.com/apache/iceberg-python) | Upstream source for PyIceberg |
| [iceberg-rust](https://github.com/apache/iceberg-rust) | Rust implementation; powers several lightweight catalogs and engines |
| [iceberg-go](https://github.com/apache/iceberg-go) | Go libraries + CLI for table/catalog work outside the JVM |

## Spec / format docs

The open table format contract — what every engine and catalog must honor.

| Link | Notes |
|------|--------|
| [Iceberg table format spec](https://iceberg.apache.org/spec/) | Canonical format: metadata trees, manifests, snapshots, partition specs, delete files |
| [REST Catalog OpenAPI](https://github.com/apache/iceberg/blob/main/open-api/rest-catalog-open-api.yaml) | Vendor-neutral HTTP API for namespaces, tables, commits, and credential vending |
| [Java API](https://iceberg.apache.org/docs/latest/api/) | Core Table/Catalog/Transaction surfaces used by most JVM engines |
| [Java API quickstart](https://iceberg.apache.org/docs/latest/java-api-quickstart/) | Minimal create → append → scan loop in Java |
| [Configuration](https://iceberg.apache.org/docs/latest/configuration/) | Table and catalog properties (write targets, commit retries, metadata retention) |
| [Partitioning](https://iceberg.apache.org/docs/latest/partitioning/) | Hidden partitioning and partition evolution without rewriting user SQL |
| [Schema evolution](https://iceberg.apache.org/docs/latest/evolution/) | Add/drop/rename/reorder columns with safe field IDs |
| [Branching & tagging](https://iceberg.apache.org/docs/latest/branching/) | Named refs for WAP-style publish and multi-writer isolation |
| [Reliability](https://iceberg.apache.org/docs/latest/reliability/) | Optimistic concurrency, atomic commits, and object-store failure modes |
| [Performance](https://iceberg.apache.org/docs/latest/performance/) | Planning, file pruning, and write/read knobs that actually move latency |
| [Maintenance](https://iceberg.apache.org/docs/latest/maintenance/) | Expire snapshots, remove orphan files, rewrite manifests — the ops baseline |
| [Terms](https://iceberg.apache.org/terms/) | Shared vocabulary (snapshot, manifest list, equality vs position deletes) |

## Catalogs

The catalog is the commit authority: names → metadata pointers, concurrency, RBAC, and (often) credential vending. Prefer **Iceberg REST Catalog** implementations for multi-engine lakes.

| Link | Notes |
|------|--------|
| [Apache Polaris](https://polaris.apache.org/) | ASF Iceberg REST catalog; RBAC + credential vending; common multi-engine default |
| [Polaris (GitHub)](https://github.com/apache/polaris) | Source, Helm charts, and release trains |
| [Snowflake Open Catalog](https://docs.snowflake.com/en/user-guide/opencatalog/overview) | Managed Polaris service — same REST surface without self-hosting |
| [Unity Catalog](https://www.unitycatalog.io/) | Open governance catalog with Iceberg REST + Delta paths |
| [Unity Catalog (GitHub)](https://github.com/unitycatalog/unitycatalog) | OSS server and clients |
| [Unity Catalog (Databricks)](https://docs.databricks.com/aws/en/data-governance/unity-catalog/) | Managed Unity — fine-grained grants, lineage, foreign Iceberg |
| [Project Nessie](https://projectnessie.org/) | Git-style branches/tags/commits across tables; Iceberg REST compatible |
| [Nessie (GitHub)](https://github.com/projectnessie/nessie) | Catalog service + client SDKs |
| [Nessie Iceberg docs](https://iceberg.apache.org/docs/latest/nessie/) | Wiring Iceberg tables through Nessie refs |
| [AWS Glue Data Catalog](https://aws.amazon.com/glue/) | Default metastore gravity on AWS; Hive + Iceberg REST endpoints |
| [Glue developer guide](https://docs.aws.amazon.com/glue/latest/dg/what-is-glue.html) | Catalog, crawlers, and Lake Formation touchpoints |
| [AWS Lake Formation](https://aws.amazon.com/lake-formation/) | Permission layer over Glue/S3 — TBAC and column filters |
| [Apache Gravitino](https://gravitino.apache.org/) | Federated metadata lake: Iceberg/Hive/JDBC under one API |
| [Gravitino (GitHub)](https://github.com/apache/gravitino) | Connectors and REST surfaces |
| [Lakekeeper](https://docs.lakekeeper.io/) | Rust Iceberg REST catalog — single-binary ops, vended credentials, OpenFGA-friendly |
| [Lakekeeper (GitHub)](https://github.com/lakekeeper/lakekeeper) | Source + Helm/K8s notes |
| [Hive catalog](https://iceberg.apache.org/docs/latest/hive/) | Classic HMS-backed Iceberg catalog (still everywhere in Hadoop estates) |
| [JDBC catalog](https://iceberg.apache.org/docs/latest/jdbc/) | Lightweight SQL-backed catalog for labs and single-tenant deployments |
| [AWS catalog helpers](https://iceberg.apache.org/docs/latest/aws/) | Glue, DynamoDB, and S3-specific catalog/storage wiring in the Java client |

## Engines & connectors

Engines that **commit** Iceberg snapshots (not read-only hacks). Favor REST catalog clients where available.

| Link | Notes |
|------|--------|
| [Apache Spark](https://spark.apache.org/) | Workhorse batch + Structured Streaming writer for Iceberg |
| [Spark quickstart](https://iceberg.apache.org/spark-quickstart/) | Minimal SparkSession → Iceberg table loop |
| [Spark getting started](https://iceberg.apache.org/docs/latest/spark-getting-started/) | Dependencies, catalogs, and first DDL/DML |
| [Spark configuration](https://iceberg.apache.org/docs/latest/spark-configuration/) | Catalog types, write distribution, and planning knobs |
| [Spark writes](https://iceberg.apache.org/docs/latest/spark-writes/) | Append, overwrite, MERGE, copy-on-write vs merge-on-read |
| [Spark queries](https://iceberg.apache.org/docs/latest/spark-queries/) | Time travel, metadata tables, and filter pushdown |
| [Spark procedures](https://iceberg.apache.org/docs/latest/spark-procedures/) | `rewrite_data_files`, `expire_snapshots`, `remove_orphan_files`, and friends |
| [Spark Structured Streaming](https://iceberg.apache.org/docs/latest/spark-structured-streaming/) | Streaming writes into Iceberg with checkpointing |
| [Trino](https://trino.io/) | Federated MPP SQL; strong Iceberg connector + REST catalogs |
| [Trino Iceberg connector](https://trino.io/docs/current/connector/iceberg.html) | Partition evolution, hidden partitioning, merge/update |
| [Apache Flink](https://flink.apache.org/) | Streaming upserts into Iceberg tables |
| [Iceberg Flink docs](https://iceberg.apache.org/docs/latest/flink/) | Source/sink and catalog wiring |
| [Flink configuration](https://iceberg.apache.org/docs/latest/flink-configuration/) | Write options, upsert mode, and checkpoint behavior |
| [DuckDB Iceberg extension](https://duckdb.org/docs/stable/extensions/iceberg.html) | Attach REST catalogs and scan Iceberg from an in-process engine |
| [Dremio](https://www.dremio.com/) | Lakehouse query + reflections; deep Iceberg/Nessie history |
| [Dremio Arctic](https://www.dremio.com/platform/arctic/) | Catalog/branching surface around Iceberg (Polaris-lineage story) |
| [Starburst](https://www.starburst.io/) | Trino-based commercial distribution |
| [Starburst Galaxy](https://www.starburst.io/platform/starburst-galaxy/) | Hosted Trino with Iceberg connectors |
| [Apache Impala](https://impala.apache.org/) | Low-latency MPP; Iceberg support in recent releases |
| [ClickHouse Iceberg](https://clickhouse.com/docs/en/engines/table-engines/integrations/iceberg) | ClickHouse table engine / integration path for Iceberg data |
| [StarRocks](https://starrocks.io/) | Real-time MPP with Iceberg external catalogs |
| [Apache Doris](https://doris.apache.org/) | Analytics engine with Iceberg external tables |
| [PrestoDB](https://github.com/prestodb/presto) | Meta lineage of Presto; Iceberg connector still in-tree |
| [RisingWave Iceberg sink](https://docs.risingwave.com/integrations/destinations/apache-iceberg) | Streaming SQL → Iceberg with append/upsert and REST catalogs |
| [Apache Kyuubi](https://kyuubi.apache.org/) | Multi-tenant Spark SQL gateway often pointed at Iceberg catalogs |
| [Confluent Iceberg Sink](https://docs.confluent.io/cloud/current/connectors/cc-iceberg-sink.html) | Kafka Connect path that lands topics as Iceberg tables |
| [dbt + Iceberg](https://docs.getdbt.com/guides/iceberg) | Transform layer patterns when the warehouse is Iceberg-backed |

## Tools

Compaction, migration, interop, branching, and local labs — the ops layer around the format.

| Link | Notes |
|------|--------|
| [Apache XTable](https://xtable.apache.org/) | Metadata-only translation across Iceberg ↔ Delta ↔ Hudi (no data rewrite) |
| [XTable (GitHub)](https://github.com/apache/incubator-xtable) | Incubating sync tooling (ex-OneTable) |
| [Apache Amoro](https://amoro.apache.org/) | Lakehouse management: self-optimizing compaction, expire, and catalog hosting for Iceberg |
| [Amoro (GitHub)](https://github.com/apache/amoro) | AMS + optimizer workers |
| [Amoro self-optimizing](https://amoro.apache.org/docs/latest/self-optimizing/) | Minor/major/full optimizing vs hand-rolled `rewrite_data_files` jobs |
| [Spark maintenance procedures](https://iceberg.apache.org/docs/latest/spark-procedures/) | Built-in rewrite/expire/orphan cleanup callable from SQL |
| [Maintenance guide](https://iceberg.apache.org/docs/latest/maintenance/) | When to expire snapshots vs rewrite manifests vs compact data files |
| [lakeFS](https://lakefs.io/) | Git-like branching for object storage — useful WAP staging before catalog publish |
| [MinIO](https://min.io/) | S3-compatible object store for on-prem / hybrid Iceberg labs |
| [docker-spark-iceberg](https://github.com/databricks/docker-spark-iceberg) | Local Spark + Iceberg + REST catalog demo stack (Tabular/Databricks lineage) |
| [Delta UniForm](https://docs.databricks.com/aws/en/delta/uniform) | Write Delta, expose Iceberg metadata for non-Databricks readers |
| [Databricks Iceberg external access](https://docs.databricks.com/aws/en/external-access/iceberg) | Read Unity-managed Iceberg from external engines via REST |
| [Netflix/iceberg (historical)](https://github.com/Netflix/iceberg) | Pre-ASF origin repo — useful for archaeology, not for new work |

## Cloud services

Managed Iceberg tables, catalogs, and query surfaces from major clouds and warehouses.

| Link | Notes |
|------|--------|
| [Amazon S3 Tables](https://aws.amazon.com/s3/features/tables/) | Managed Iceberg tables in S3 with a built-in REST catalog endpoint |
| [S3 Tables user guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-tables.html) | Bucket types, maintenance, and access patterns |
| [Amazon Athena + Iceberg](https://docs.aws.amazon.com/athena/latest/ug/querying-iceberg.html) | Serverless SQL over Iceberg (Glue catalog gravity) |
| [Amazon EMR + Iceberg](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-iceberg.html) | Spark/Flink/Trino on EMR pointed at Iceberg |
| [Snowflake Iceberg tables](https://docs.snowflake.com/en/user-guide/tables-iceberg) | Snowflake as compute over Iceberg in your object store or Snowflake-managed storage |
| [Snowflake Iceberg storage](https://docs.snowflake.com/en/user-guide/tables-iceberg-storage) | External vs Snowflake-managed Iceberg storage choices |
| [BigQuery Iceberg tables](https://cloud.google.com/bigquery/docs/iceberg-tables) | BigLake/BigQuery paths for Iceberg metadata on GCS |
| [BigQuery open-source metadata](https://cloud.google.com/bigquery/docs/manage-open-source-metadata) | Managing Iceberg (and related) metadata from BigQuery |
| [Databricks Unity Catalog](https://www.databricks.com/product/unity-catalog) | Managed governance with Iceberg REST / UniForm bridges |
| [Microsoft Fabric](https://www.microsoft.com/en-us/microsoft-fabric) | Lakehouse SaaS; Iceberg interop evolving via OneLake / Delta UniForm-style bridges |
| [Bauplan](https://www.bauplanlabs.com/) | Python-first lakehouse compute aimed at Iceberg tables as the storage contract |

## Learning

Start with the spec and docs, then one catalog + one engine — not a vendor tour.

| Link | Notes |
|------|--------|
| [Iceberg docs (latest)](https://iceberg.apache.org/docs/latest/) | Best first read after the homepage |
| [Table format spec](https://iceberg.apache.org/spec/) | Read before designing a custom catalog or writer |
| [Talks](https://iceberg.apache.org/talks/) | Conference talks from committers and practitioners |
| [dev@ mailing list archive](https://lists.apache.org/list.html?dev@iceberg.apache.org) | Design threads and release votes |
| [Lakehouse CIDR paper (PDF)](https://www.cidrdb.org/cidr2021/papers/cidr2021_paper17.pdf) | Systems context for why open table formats exist |
| [Data Engineering Wiki](https://dataengineering.wiki/) | Community encyclopedia spanning lakes, warehouses, and orchestration |
| [e6data optimizing list](https://github.com/e6data/awesome-optimizing-iceberg-tables) | Narrow, practical list focused on Iceberg table optimization |

## Related

| Link | Notes |
|------|--------|
| [Audie-glitch/awesome-lakehouse](https://github.com/Audie-glitch/awesome-lakehouse) | **Sibling** — multi-format lakehouse (Iceberg / Delta / Hudi + catalogs, engines, governance). This repo is the Iceberg-deep cut of that surface |
| [e6data/awesome-optimizing-iceberg-tables](https://github.com/e6data/awesome-optimizing-iceberg-tables) | Compaction, file layout, and cost/latency tuning resources |

## Contributing

1. PR = one live URL + a short blurb **you** wrote.
2. Prefer primary docs/repos over marketing landings.
3. Iceberg-relevant only (spec, catalogs, engines that commit, table tools, cloud Iceberg surfaces, learning).
4. No paid starring, no dumping other awesome lists, no fake badges.

## License

List text: [CC0 1.0](./LICENSE). Linked projects keep their own licenses.
