# Data mesh



## Architectural failure modes

1. **The first generation**: *proprietary [enterprise data warehouse](https://www.thoughtworks.com/radar/platforms/enterprise-data-warehouse) and business intelligence* platforms  企业数据仓库和商业智能平台
2. **The second generation**: *big data ecosystem with a [data lake](https://martinfowler.com/bliki/DataLake.html) as a silver bullet*  以data lake为基础的大数据生态系统
3. **The third and current generation data platforms**:  a) streaming for real-time data availability 流处理以实现实时数据可用; b) batch and stream processing for data transformation 批处理和流处理以进行数据转换; c) fully embracing [cloud based managed services](https://cloud.google.com/solutions/big-data/#products-and-solutions) for storage, data pipeline execution engines and machine learning platforms  基于云存储托管

### Centralized and monolithic(集中化和单一化)

- ingest
- cleanse, enrich and transform
- serve

![img](https://martinfowler.com/articles/data-monolith-to-mesh/big-data-platform.png)

*Centralized data platform with no clear data domain boundaries and ownership of domain oriented data:* 

![img](https://martinfowler.com/articles/data-monolith-to-mesh/no-domain-data-platform.png)

There are 2 pressure points:

- **Ubiquitous data and source proliferation**(数据分散和数据源扩散)
- **Organizations' innovation agenda and consumer proliferation**



### Coupled pipeline decomposition

![img](https://martinfowler.com/articles/data-monolith-to-mesh/functional-decomposition.png)

 It has high coupling between the stages of the pipeline to deliver an independent feature or value. It's decomposed *orthogonally to the axis of change*.

![img](https://martinfowler.com/articles/data-monolith-to-mesh/axis-of-change.png)

Architecture decomposition is **orthogonal to the axis of change** when introducing or enhancing features, leading to coupling and slower delivery

### Siloed and hyper-specialized ownership

![img](https://martinfowler.com/articles/data-monolith-to-mesh/siloed-teams.png)

does not scale and does not deliver the promised value of creating a data-driven organization



## Date Mesh

