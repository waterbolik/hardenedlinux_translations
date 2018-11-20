# 第 1 章 简介

## 1.1 目的

现代计算和信息技术系统构建于一系列提供系统运行所必需的功能能力的硬件组件之上。众多此类硬件组件拥有驱动其行为的固件和配置数据，并且它们必须维持在某种具有完整性的状态，以使得系统正常运作。此类固件的一个范例通常被称为基本输入/输出系统（BIOS），它被用于辅助硬件初始化过程并且将控制权移交给操作系统。取决于系统，可能有数十或者数百个具有其他类型的可编程固件的微控制器，其固件支持了整体系统架构。这些硬件和固件的集合通常称为 _平台_。

构成了平台的设备对于基于此平台构建的系统的完整性和可用性至关重要。没有这些设备，系统可能不能正确地运行，甚至完全不能运行。针对平台中的某些设备的攻击可以对系统的安全状态造成重大影响，有可能允许低级恶意软件的持久存在。定位于损坏或者移除平台固件的攻击具有使得系统永久损坏的潜力，从而对受其影响的相关方受到实质性的损失。

此文档的目的是为在平台层级支持系统弹性提供安全性指导意见。如同系统工程国际委员会（INCOSE）所定义，系统弹性是指“具有某些特定性质的系统在干扰发生之前、之中和之后吸收此干扰、恢复至某种可接受的性能水平，并且维持该水平达到一段可接受的时间的能力” \[10\]。应用于信息系统时，网络弹性是指“预见、抵御、恢复并且适应针对包含网络资源的系统的不利条件、压力、攻击或者破坏的能力”。尽管关于系统层级的网络弹性的指导意见在 NIST 特别出版 800-160 草案第 2 卷中有所描述，此出版物指出这种系统层级的弹性应该由计算机平台中的基础安全性能力所支持。此文档中的指导意见支持网络弹性，通过具体说明保护固件和配置数据不受攻击，以及能够检测并且从成功的攻击中恢复的机制。

## 1.2 受众

此文档本意中的受众包括计算机系统的系统和平台设备厂商，其中包括客户端、服务器和网络设备的制造商。这些技术指导意见假设读者拥有平台架构方面的技能，并且主要面向负责在系统和设备中实现固件级安全技术的开发者和工程师。

这些素材对于开发企业范围内的采购和部署策略可能也会有用。此文档中的素材是面向技术的，并且假设读者对于计算机安全性原理和计算机架构至少拥有基本的理解。此文档提供了背景信息以帮助这些读者理解正在讨论的话题。

## 1.3 适用性和范围

此文档的目的是提供能够支持主要面对远程攻击的平台弹性的原则和指导意见。这些原则和指导意见直接适用于构成了平台的独立设备（参见 2.1 节以获取一系列范例的列表）。具体地，它们描述了定位于保护每个设备使其固件或者关键数据不被非授权修改以及将平台恢复至某种具有完整性的状态的安全机制。

## 1.4 文档结构

此文档的剩余部分被组织进下列主要部分中：

* 第 2 章提供了描述平台组件和架构的信息性素材
* 第 3 章描述了构成此文档中的指导意见的基础的安全性原则，并且描述了将这些原则应用于平台弹性的关键概念
* 第 4 章包含关于保护固件代码和关键数据、检测非授权更改以及恢复至某个具有完整性的状态的安全技术指导意见
* 附录 A 提供了此文档中的首字母缩略词和缩略语
* 附录 B 呈现了此文档中的选定的术语的词汇表
* 附录 C 包含此文档中的参考文献列表
