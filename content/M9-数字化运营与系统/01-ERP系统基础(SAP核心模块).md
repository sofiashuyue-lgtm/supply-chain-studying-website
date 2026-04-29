# 01 ERP 系统基础（SAP 核心模块）

> **📌 知识层级说明**
> 🟢 **基础必掌握** — 入职前、面试前必须理解
> 🟡 **进阶了解** — 有基础后扩展，理解逻辑即可
> 🔴 **暂缓** — 工作后遇到实际场景再深入

---

## 一、什么是 ERP？采购人为什么必须懂？🟢 基础必掌握

**ERP（Enterprise Resource Planning，企业资源规划）**：将企业所有核心业务流程（采购、生产、库存、财务、销售）集成在同一系统中，共享一个数据库，实现信息实时流转。

**采购人的日常工作几乎全在 ERP 系统中完成**：

```
收到 PR（采购申请）→ 在 ERP 中审核 PR
    ↓
在 ERP 中创建 PO（采购订单）
    ↓
跟踪 PO 状态（在途、部分收货、完全收货）
    ↓
确认 GR（收货过账）
    ↓
匹配 Invoice（发票核验）
    ↓
触发付款
```

**面试常问**："你用过哪些 ERP 系统？" — 即使没有实操经验，也要能说出 SAP 的核心模块名称和逻辑。

---

## 二、全球主流 ERP 系统概览 🟢 基础必掌握

| 系统 | 公司 | 市场定位 | 中国应用情况 |
|------|------|---------|------------|
| **SAP S/4HANA** | SAP（德国）| 大型企业首选 | 华为、比亚迪、富士康、中国500强 |
| **Oracle ERP Cloud** | Oracle（美国）| 大中型企业 | 外资企业常用 |
| **用友 U9/U8** | 用友网络 | 中国中大型企业 | 国内制造业广泛使用 |
| **金蝶 EAS/云星空** | 金蝶国际 | 中国中小企业 | 国内制造/贸易企业 |
| **Microsoft Dynamics 365** | 微软 | 中型企业 | 外资中型企业 |

> 💡 **求职重点**：目标企业（华为、大疆、海康、中兴等）基本全部使用 **SAP**。优先熟悉 SAP 的采购相关模块。

---

## 三、SAP 采购相关核心模块 🟢 基础必掌握

### SAP 的模块架构（采购相关）

```
SAP 系统
├── MM（Materials Management，物料管理）← 采购最核心
│   ├── 采购（Purchasing）— PR/PO/GR/IV
│   ├── 库存管理（Inventory Management）
│   └── 发票验证（Invoice Verification）
│
├── SD（Sales & Distribution，销售与分销）
├── PP（Production Planning，生产计划）← MRP/MPS 所在模块
├── FI（Financial Accounting，财务会计）← AP 应付账款
├── CO（Controlling，管理会计）← 成本中心分析
└── QM（Quality Management，质量管理）← IQC/SCAR
```

### MM 模块（物料管理）核心流程 🟢

#### 采购流程（Purchase to Pay）

| 步骤 | SAP 操作 | 事务代码（T-Code）|
|------|---------|----------------|
| 创建采购申请 | 需求部门/MRP 自动生成 | **ME51N** |
| 审核/转化 PO | Buyer 将 PR 转为 PO | **ME21N**（创建）/ **ME22N**（修改）|
| 发送 PO 给供应商 | 打印/邮件/EDI 发送 | — |
| 收货（GR）| 仓库确认入库 | **MIGO** |
| 发票验证（IV）| 财务核对三单 | **MIRO** |
| 付款 | 财务到期付款 | FI 模块处理 |

#### 物料主数据（Material Master）

每个物料在 SAP 中有一个**物料主数据（Material Master）**，包含：

| 字段 | 说明 |
|------|------|
| **物料编号（Material Number）** | 唯一标识，贯穿所有模块 |
| **物料描述** | 中英文描述 |
| **物料类型（Material Type）** | 原料/半成品/产成品/MRO |
| **计量单位（UoM）** | 个/千克/米/套 |
| **采购数据** | Lead Time、安全库存、最小批量 |
| **MRP 数据** | MRP 类型（自动补货/手动/无 MRP）|
| **仓储数据** | 存储条件、货位 |

#### 供应商主数据（Vendor Master）

| 字段 | 说明 |
|------|------|
| **供应商编号** | 唯一标识 |
| **名称/地址/税号** | 基础信息 |
| **付款条件** | Net 60、月结45天等 |
| **银行账户** | 付款用 |
| **采购组织** | 哪个采购组有权向该供应商下单 |

---

## 四、SAP 常用事务代码速查 🟡 进阶了解

| T-Code | 功能 | 使用频率 |
|--------|------|---------|
| **ME21N** | 创建采购订单 PO | ⭐⭐⭐⭐⭐ |
| **ME22N** | 修改采购订单 | ⭐⭐⭐⭐ |
| **ME23N** | 查看采购订单 | ⭐⭐⭐⭐⭐ |
| **ME51N** | 创建采购申请 PR | ⭐⭐⭐ |
| **ME2M** | 按物料查询 PO 列表 | ⭐⭐⭐⭐ |
| **ME2N** | 按 PO 号查询 | ⭐⭐⭐ |
| **MIGO** | 收货/GR 过账 | ⭐⭐⭐⭐ |
| **MIRO** | 发票验证 | ⭐⭐⭐ |
| **MB52** | 查询当前库存 | ⭐⭐⭐⭐ |
| **MB51** | 物料流水账（移动历史）| ⭐⭐⭐ |
| **MD04** | 物料需求情况（含 MRP 结果）| ⭐⭐⭐⭐ |
| **ME5A** | 采购申请清单 | ⭐⭐⭐ |

---

## 五、SAP S/4HANA vs SAP ECC — 了解版本差异 🟡 进阶了解

| 对比 | SAP ECC 6.0（旧版）| SAP S/4HANA（新版）|
|------|------------------|------------------|
| 数据库 | 传统关系型数据库 | HANA 内存数据库（速度极快）|
| 界面 | SAP GUI（桌面客户端）| Fiori（网页端，移动端友好）|
| 实时分析 | 慢，需跑报表 | 实时，边操作边分析 |
| 国内普及率 | 大量老系统仍在用 | 新上线企业主流选择 |

> 💡 **实务建议**：简历上写"熟悉 SAP MM 模块（ECC 6.0/S4HANA）"。即使你只学过 ECC，S/4HANA 的业务逻辑完全相同，只是界面不同。

---

## 六、如何在没有实际 SAP 经验时展示系统能力 🟢 基础必掌握

**方法1：使用 SAP 官方试用环境**
- SAP Learning Hub（学习中心）提供免费的模拟系统
- [SAP Learning Hub](https://learning.sap.com/)

**方法2：参加 SAP 认证课程**
- **SAP Certified Application Associate - SAP MM**（物料管理模块认证）
- 考试费约 USD 500，国内培训机构有模拟题

**方法3：在简历和面试中用正确的术语**
即使无实操，能说出"我理解 PR → PO → GR → IV 的三单匹配流程，在 SAP 中对应 ME51N/ME21N/MIGO/MIRO 的操作"，已经能给面试官留下不错印象。

---

## 七、关键术语速查 🟢

| 术语 | 解释 |
|------|------|
| **ERP** | Enterprise Resource Planning，企业资源规划 |
| **MM** | Materials Management，SAP 物料管理模块 |
| **T-Code** | Transaction Code，SAP 中每个功能的快捷操作代码 |
| **Material Master** | 物料主数据，每个物料在 SAP 的唯一档案 |
| **Vendor Master** | 供应商主数据 |
| **GR/IR** | Goods Receipt / Invoice Receipt，收货/发票应计账 |
| **HANA** | SAP 的内存数据库技术，S/4HANA 的底层 |
| **Fiori** | SAP S/4HANA 的现代化网页界面 |

---

## 📚 参考来源

- [SAP MM 物料管理模块官方文档 - SAP Help Portal](https://help.sap.com/docs/SAP_S4HANA_ON-PREMISE/mm-module)
- [SAP 采购流程（P2P）详解 - SAP Community](https://community.sap.com/topics/mm/procurement)
- [SAP MM 常用事务代码大全 - CSDN](https://blog.csdn.net/sap_mm/t-code-list)
- [SAP S/4HANA vs ECC 对比 - 知乎](https://zhuanlan.zhihu.com/p/298456123)
- [SAP 学习资源与认证路径 - SAP Learning Hub](https://learning.sap.com/)
- [采购人 SAP 快速入门指南 - 博客园](https://www.cnblogs.com/sap-mm/p/buyer-sap-guide.html)
