# 第 1 章 简介

## 1.1 权力范围

美国国家标准技术研究所（NIST）开发此文档以履行其在 2002 年美国联邦信息安全管理法案，公法 107-347 下的法定责任。

NIST 负有开发标准和指导意见，包括最低要求的责任，以便为所有政府机构的运作和财产提供足够的信息安全；但是，这些标准和指导意见不会适用于国家安全系统。此指导意见与美国行政管理和预算局（OMB）的公告 A-130 第 8b\(3\) 节“防护政府机构信息系统”相一致，如同在 A-130 的附录 IV“关键章节分析”中所分析的那样。补充信息在 A-130 附录 III 中提供。

此指导意见为联邦政府机构而准备。它可以在自愿基础上被非政府组织使用，并且不受限于版权，尽管我们要求署名权。

此文档中的任何部分都不应该被带到由美国商务部秘书在法定权力之下规定为对于联邦政府机构具有强制性和法定约束力的与之相矛盾的标准中来，这些指导意见也不应该被解读为更改或是取代商务部秘书、OMB 主任或是任何联邦官员的现有职权。

## 1.2 目的和范围

此文档为防止 PC 客户端系统上的针对基本输入/输出系统（_BIOS_）的非授权修改提供了指导意见。由恶意软件进行的非授权 BIOS 修改构成了显著的威胁，由于 BIOS 在 PC 架构中的独特和特权的地位。对 BIOS 的恶意修改可能是针对某个组织的高级攻击的一部分——可以是永久的拒绝服务（如果 BIOS 损坏），也可以是持久的恶意软件存在（如果 BIOS 被植入恶意软件）。

如同在本出版物中所使用的那样，BIOS 这一词语可以指代传统 BIOS、可扩展固件接口（_EFI_）BIOS 以及统一可扩展固件接口（_UEFI_）BIOS。此文档适用于存储于计算机系统中的系统闪存中的系统 BIOS 固件（例如，传统 BIOS 或者 UEFI BIOS），包括可能被格式化为 Option ROM 的部分。然而，它并不适用于存储于计算机系统中的其他位置的 Option ROM、UEFI 驱动程序和固件。

此指南的 3.1 节为平台厂商提供了用于安全 BIOS 更新过程的建议和指导意见。此外，3.2 节提供了针对操作环境中的 BIOS 管理的建议。此出版物的未来修订版本还将应对与 BIOS 进行交互的关键系统固件的安全性。

尽管此文档的关注焦点是当前和未来的 x86 和 x64 客户端平台，其控制和过程独立于任何特别的系统设计。类似地，尽管此指南面向企业级平台，其必要的技术可以期望随着时间迁移到消费者级别的系统上。未来的努力可能会着眼于企业服务器平台的启动固件安全性。

## 1.3 受众

此文档本意中的受众包括 BIOS 和平台厂商，以及负责管理终端平台的安全性、安全启动过程和硬件安全性模块的信息系统安全专业人士。这些素材在开发企业范围的采购策略并且部署的时候可能也会有用。

此文档中的素材是面向技术的，并且它假设读者至少拥有对于系统和网络安全的基本理解。此文档提供了背景信息，以帮助这些读者理解所讨论的话题。我们鼓励读者利用其他资源（包括列出于此文档中的）以获取更多细节信息。

## 1.4 文档结构

此文档的剩余部分被组织为以下章节：

* 第 2 章呈现了对于 BIOS 及其在启动中的作用的总览，并且指认了在操作环境中针对 BIOS 的潜在攻击
* 第 3 章检验了针对 BIOS 的选定威胁可以如何被化解。3.1 节描述了为了化解这些威胁所要求或者推荐的用于 BIOS 实现的安全控制。3.2 节定义了在企业内部作为平台管理生命周期的一部分撬动这些控制以实施一种安全 BIOS 更新过程的过程

此文档还包含带有支持材料的附录：

* 附录 A 包含了关于系统 BIOS 实现的安全指导意见的总结
* 附录 B 定义了此文档中所使用的词语
* 附录 C 包含了此文档中使用的首字母缩略词和缩略语列表
* 附录 D 包含了开发此文档过程中所使用的参考文献列表

