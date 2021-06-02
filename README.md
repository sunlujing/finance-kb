# finance-kb 金融知识图谱
## 目标
以上市公司年报为基础信息，构建上市公司的金融知识图谱，强调投资逻辑的构建
## 主要实体
1. [Company](#company)

目前市场上的公司股权类图谱已经很多，我们这里存储简单的信息。

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
| name  | string | 公司全名 | 
|ticker	| string	| 上市公司代码 |
|short_name |	string	|上市公司简称 |
| cn_spell	| string	| 拼音简写 |
| list_date |	string	|上市时间,yyyy-mm-dd |
| delist_date	| string | 退市时间,yyyy-mm-dd	 |

2. [Industry](#industry)

行业实体，行业分类有很多种，目前市面上的行业分类都比较粗粒度；对于行业的分类越细越有区分度。在量化研究领域，有通过自己实现行业分类来获取超额收益的。
比如，利用同行业公司的补涨，跟涨等逻辑来构建投资策略等。
我们希望行业的信息来自公司的 年报或者招股书，相比市场上的分类更加有参考价值。


|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
| name  | string | 行业名称 | 
|source | string | 分类源:比如申万,自定义 |
|key_words | string	|行业相关的关键词 |

3. [MainBusiness](#mainBusiness)

对应年报中的主营拆分项

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
| name  | string | 主营名称 | 
|classification | string | 拆分标准，比如行业，产品|
|period_date | string	|报告期 |
|revenue | double	|营收，单位：亿 |
|gross_profit | double	|毛利，单位：亿 |

4. [Product](#product)

主营拆分相对来说还是比较粗粒度，对主营项目拆分到具体的产品，并结合产业链上下游的信息，能够更加准确的做出投资判断

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
| name  | string | 产品名称 | 
|source | string | 产品来源:比如年报，研报，专业机构 |
|key_words | string	|行业相关的关键词，同义词等 |
|scope | string	|应用领域 |

5. [EmployeeStats](#employeeStats)

员工统计信息，可以帮助分析公司的人均人效，员工扩展情况。

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
| period_date  | string | 报告期 | 
|total | long | 总人数|
|research | string	|研发人员 |
|sales | string	|销售人员 |
|admin | string	|支持类人员 |
|bachelor_degree | string	| 本科学历人员 |
|master_degree | string	|硕士学历及以上 |


6. [CapacityLogic](#capacityLogic) 产能逻辑

我们认为业绩是驱动公司股价上涨的最核心因素，而 业绩的增长，可以是 卖得多，卖得贵，成本低
我们从这个模型出发构建相应的逻辑实体。

产能扩张，对于一个公司是重要的信息，以为这未来可卖的产品讲大幅提升，营收讲大幅增长。

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
| project_name  | string | 项目名称 | 
|expected_capacity | string | 目标产能|
|expected_revenue | string	|目标营收 |
|investment | double |投资额：亿 |
|related_product | string	|相关产品 |
|brief | string	| 简介 |
|refer | text	|产能扩张的信息来源，比如连接，截图等等 |
|start_date | string	|开始时间 |
|end_date | string	|结束时间 |

7. [PriceLogic](#priceLogic) 涨价逻辑

主营产品涨价，将会带来业绩大幅增长，是投资分析中需要重点捕捉的信息。

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
| upstream  | string | 上游 | 
|downstream | string | 下游|
|reason | string	|原因 |
|price_circle | string | 价格周期 |
|capacity_circle | string | 产能周期 |
|price_trend_now | string	|当前价格趋势 |
|price_trend_history | string	| 历史趋势 |
|refer | text	|价格上涨的信息来源，比如连接，截图等等|
|start_date | string	|开始时间 |
|end_date | string	|结束时间 |

8. [CostLogic](#costLogic) 成本控制逻辑

降本增效，可以有效的提高净利润水平

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
| total  | long | 总的成本：亿 | 
|supplier_cost | long | 供应商成本|
|sales_cost | long	|销售成本 |
|mgr_cost | long	|管理成本 |
|fin_cost | long	|财务成本 |
|rd_cost | long	|研发成本 |

9. [RiskLogic](#riskLogic) 风险逻辑

识别风险，可以有效的规避损失

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
| title  | string | 风险简介  | 
|scope	|string |	财务，供应链，客户，行业等|
| abstract  | string | 摘要  | 
| refer| string | 信息来源，比如连接，截图等等  | 


10. [RDLogic](#rdLogic) 研发逻辑

对于高新技术企业而言，需要时刻把握主要的研发方向

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
| project_name  | string | 研发项目  | 
|content	|string |	主要内容能够|
|related_product  | string | 涉及的产品  | 
|start_date | string	|开始时间 |
|end_date | string	|结束时间 |
|impact_est| string	|预估的影响 |

11. [IndustryLogic](#industrLogic) 行业逻辑

对公司涉及行业的一个把握，可以从研报和公司经营评述中获得相关信息

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
| total_scale  | long | 行业整体规模  | 
|competition_struct	|string |	竞争格局|
|maturity  | string | 行业成熟度  | 
|key_driver | string	|行业发展主要驱动因素 |
|CAGR_5 | string	|未来五年复合增长率估计 |
|demand| string	|需求情况 |
|supply| string	|供给情况 |
| refer| string | 信息来源，比如连接，截图等等  | 

12. [InvestLogic](#investLogic)

相对宏观的投资逻辑，比较主观化，依赖个人经验。

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|logic_tag  | string | 逻辑风格，枚举值，价值投资，技术面，量化，底部反转,etc.  | 
|detail	|string |	逻辑详情|
|rise_space  | string | 上涨空间  | 
|proposal | string	|long/short |


13. [DataItem](#dataItem)

数据节点，对于任何需要以数据挂载来作为辅助分析的，都可以挂载数据节点。

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|name  | string | 数据项名称  | 
|classification	|string |	分类，比如财务，经营等等|
|value  | double | 值  |
 |unit  | string | 单位，枚举  |
 |yoy  | double | 百分比 |
 |period_date  | string | 时间|


## 主要关系

1. Comp_BelongTo_Ind(公司属于行业)

- source: <a href="#company">Company</a>
- target: <a href="#industry">Industry</a>

2. Ind_ParentOf_Ind(行业父级关系)

行业通分类体系中，多以层级关系组织

- source: <a href="#industry">Industry</a>
- target: <a href="#industry">Industry</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|classification	|string |	分类标准|

3. Comp_Has_Main_Bus(公司主营拆分)

- source: <a href="#company">Company</a>
- target: <a href="#mainBusiness">MainBusiness</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|start_date  | string | 报告期起始日期  | 
|end_date	|string |	报告期结束日期 |

4. MainBus_Include_Prod(主营拆分关联的产品)
- source: <a href="#mainBusiness">MainBusiness</a>
- target: <a href="#product">Product</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|start_date  | string | 报告期起始日期  | 
|end_date	|string |	报告期结束日期 |
|ratio	|double |	产品占营收的比例 |


5. Prod_UpStreamOf_Prod (产品上下游关系)

用于产品的产业链构建，产业链对投资逻辑的传导有重要作用。

- source: <a href="#product">Product</a>
- target: <a href="#product">Product</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|relation  | string | 产业链关系，比如 原材料，组件  | 

6. Comp_Has_EmpStats (公司员工关系)

- source: <a href="#company">Company</a>
- target: <a href="#employeeStats">EmployeeStats</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|start_date  | string | 报告期起始日期  | 
|end_date	|string |	报告期结束日期 |


7. 产能逻辑相关的关系

产能逻辑节点，可以挂载到 行业， 主营拆分， 产品节点上， 用来分析他们的产能情况。

7.1 CapLgc_RelateTo_Ind(行业产能关系)

- source: <a href="#capacityLogic">CapacityLogic</a>
- target: <a href="#industry">Industry</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|start_date  | string | 逻辑起始日期  | 
|end_date	|string |	逻辑期结束日期 |

7.2 CapLgc_RelateTo_MainBus(主营产能关系)

- source: <a href="#capacityLogic">CapacityLogic</a>
- target: <a href="#mainBusiness">MainBusiness</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|start_date  | string | 逻辑起始日期  | 
|end_date	|string |	逻辑期结束日期 |

7.3 CapLgc_RelateTo_Prod(产品产能关系)

- source: <a href="#capacityLogic">CapacityLogic</a>
- target: <a href="#product">Product</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|start_date  | string | 逻辑起始日期  | 
|end_date	|string |	逻辑期结束日期 |


8. 成本逻辑相关关系

成本逻辑节点，可以挂载到 公司，主营拆分， 产品节点上

8.1 CstLgc_RelateTo_Comp(公司成本关系)

- source: <a href="#costLogic">CostLogic</a>
- target: <a href="#company">Company</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|start_date  | string | 逻辑起始日期  | 
|end_date	|string |	逻辑期结束日期 |

8.2 CapLgc_RelateTo_MainBus(主营成本关系)

- source: <a href="#costLogic">CostLogic</a>
- target: <a href="#mainBusiness">MainBusiness</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|start_date  | string | 逻辑起始日期  | 
|end_date	|string |	逻辑期结束日期 |

8.3 CapLgc_RelateTo_Prod(产品成本关系)

- source: <a href="#costLogic">CostLogic</a>
- target: <a href="#product">Product</a>

9. 价格逻辑相关的关系

价格逻辑节点，可以挂载到 行业， 主营拆分， 产品节点上， 用来分析他们的涨价情况。

9.1 PrcLgc_RelateTo_Ind(行业价格关系)

- source: <a href="#priceLogic">PriceLogic</a>
- target: <a href="#industry">Industry</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|start_date  | string | 逻辑起始日期  | 
|end_date	|string |	逻辑期结束日期 |

9.2 PrcLgc_RelateTo_MainBus(主营价格关系)

- source: <a href="#priceLogic">PriceLogic</a>
- target: <a href="#mainBusiness">MainBusiness</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|start_date  | string | 逻辑起始日期  | 
|end_date	|string |	逻辑期结束日期 |

9.3 PrcLgc_RelateTo_Prod(产品价格关系)

- source: <a href="#priceLogic">PriceLogic</a>
- target: <a href="#product">Product</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|start_date  | string | 逻辑起始日期  | 
|end_date	|string |	逻辑期结束日期 |


10. 风险逻辑相关的关系

风险逻辑节点，可以挂载到 公司， 行业， 主营拆分， 产品节点上。

10.1 RskLgc_RelateTo_Ind(行业风险关系)

- source: <a href="#riskLogic">RiskLogic</a>
- target: <a href="#industry">Industry</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|start_date  | string | 逻辑起始日期  | 
|end_date	|string |	逻辑期结束日期 |

10.2 RskLgc_RelateTo_MainBus(主营风险关系)

- source: <a href="#riskLogic">RiskLogic</a>
- target: <a href="#mainBusiness">MainBusiness</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|start_date  | string | 逻辑起始日期  | 
|end_date	|string |	逻辑期结束日期 |

10.3 RskLgc_RelateTo_Prod(产品风险关系)

- source: <a href="#riskLogic">RiskLogic</a>
- target: <a href="#product">Product</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|start_date  | string | 逻辑起始日期  | 
|end_date	|string |	逻辑期结束日期 |

10.4 RskLgc_RelateTo_Company(公司风险关系)

- source: <a href="#riskLogic">RiskLogic</a>
- target: <a href="#company">Company</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|start_date  | string | 逻辑起始日期  | 
|end_date	|string |	逻辑期结束日期 |


11. 研发逻辑相关的关系

研发逻辑节点，可以挂载到 行业， 主营拆分， 产品节点上。

11.1 RDLgc_RelateTo_Ind(行业研发关系)

- source: <a href="#rdLogic">RDLogic</a>
- target: <a href="#industry">Industry</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|start_date  | string | 逻辑起始日期  | 
|end_date	|string |	逻辑期结束日期 |

11.2 RDLgc_RelateTo_MainBus(主营研发关系)

- source: <a href="#rdLogic">RDLogic</a>
- target: <a href="#mainBusiness">MainBusiness</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|start_date  | string | 逻辑起始日期  | 
|end_date	|string |	逻辑期结束日期 |

11.3 RDLgc_RelateTo_Prod(产品研发关系)

- source: <a href="#rdLogic">RDLogic</a>
- target: <a href="#product">Product</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|start_date  | string | 逻辑起始日期  | 
|end_date	|string |	逻辑期结束日期 |


12. 行业逻辑相关的关系

行业逻辑节点，可以挂载到 行业节点上。

12.1 IndLgc_RelateTo_Ind(行业研发关系)

- source: <a href="#indsutryLogic">IndustryLogic</a>
- target: <a href="#industry">Industry</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|start_date  | string | 逻辑起始日期  | 
|end_date	|string |	逻辑期结束日期 |

13. 公司投资逻辑相关的关系

投资逻辑overview，不好标准化的逻辑，依赖人的经验

13.1 InvstLgc_RelateTo_Company(行业研发关系)

- source: <a href="#investLogic">InvestLogic</a>
- target: <a href="#company">Company</a>

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|start_date  | string | 逻辑起始日期  | 
|end_date	|string |	逻辑期结束日期 |

14. 数据节点相关关系

数据节点可以挂载到任何其他节点，作为数据说明
通用属性：

|  属性   | 类型  | 描述 |
|  ----  | ----  | ---- |
|start_date  | string | 逻辑起始日期  | 
|end_date	|string |	逻辑期结束日期 |


14.1 Data_RelateTo_Comp
- source: <a href="#dataItem">DataItem</a>
- target: <a href="#company">Company</a>

14.2 Data_RelateTo_Ind
- source: <a href="#dataItem">DataItem</a>
- target: <a href="#industry">Industry</a>

14.3 Data_RelateTo_MainBus
- source: <a href="#dataItem">DataItem</a>
- target: <a href="#mainBusiness">MainBusiness</a>

14.4 Data_RelateTo_Prod
- source: <a href="#dataItem">DataItem</a>
- target: <a href="#product">Product</a>

14.5 Data_RelateTo_CapLgc
- source: <a href="#dataItem">DataItem</a>
- target: <a href="#capacityLogic">CapacityLogic</a>

14.6 Data_RelateTo_PrcLgc
- source: <a href="#dataItem">DataItem</a>
- target: <a href="#priceLogic">PriceLogic</a>

14.7 Data_RelateTo_CstLgc
- source: <a href="#dataItem">DataItem</a>
- target: <a href="#costLogic">CostLogic</a>

14.8 Data_RelateTo_RskLgc
- source: <a href="#dataItem">DataItem</a>
- target: <a href="#riskLogic">RiskLogic</a>

14.9 Data_RelateTo_RDkLgc
- source: <a href="#dataItem">DataItem</a>
- target: <a href="#rdLogic">RDLogic</a>

14.10 Data_RelateTo_IndLgc
- source: <a href="#dataItem">DataItem</a>
- target: <a href="#industryLogic">IndustryLogic</a>

14.11 Data_RelateTo_InvstLgc
- source: <a href="#dataItem">DataItem</a>
- target: <a href="#investLogic">InvestLogic</a>
