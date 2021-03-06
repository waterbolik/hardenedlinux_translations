# 第 5 章 关于服务处理器的指导意见

服务器和客户端的关键区别之一在于系统中是否包含服务处理器。服务处理器在管理和监视服务器的过程中具有重要作用，并且可能在更新系统 BIOS 过程中也有作用。本章描述服务处理器并且为包含服务处理器的系统提供更加详细的安全性要求。

## 5.1 作为可信根的服务处理器

受管理的服务器和刀片服务器中的服务处理器可能拥有直接更新 BIOS 闪存存储器、BIOS 执行内存或者它们自己的闪存或者其他存储介质的能力。在这些情况下，某些或者全部服务处理器环境可以被用作系统 BIOS 的 RTU。这适用于在那些使用 BIOS 闪存保护机制以防止对 BIOS 代码的非授权修改的系统（例如使用第 4 章所述的更新机制 1 或 2 的系统）上能够更新 BIOS 闪存的服务处理器。这也适用于在那些在执行前验证 BIOS 代码的系统（例如使用更新机制 3 的系统）上能够修改用于验证 BIOS 代码的 RTU 的服务处理器。

在这些情况下，服务处理器（SP）的执行环境必须被保护以防止那些能够更新 BIOS 或者 SP 闪存的恶意代码。为了满足第 3 章所述的 BIOS 安全性原则，用作可信根以保护 BIOS 的服务处理器应该满足以下指导意见：

1. 针对 SP 代码、密码学密钥以及存储于 SP 闪存中的静态数据的更新应该经过认证更新机制
2. SP 环境应该被控制，使得只有合法代码可以在 SP 上执行
3. 用户同服务处理器的交互应该要求授权。

## 5.2 由服务处理器实现的 BIOS 保护的不可绕过性

某些带有服务处理器的服务器可能不将服务处理器用作 BIOS 更新的 RTU。为了保证 SP 环境不能绕过 BIOS 保护，这些系统中的服务处理器不应该拥有对于 BIOS 代码在其中验证或者执行的 BIOS 闪存存储器的直接写入访问权限。更进一步地，服务处理器应该受到限制，使得它不能干涉 BIOS 更新过程，也不能干涉 BIOS 或者 RTU 代码在其中执行的内存。

未被实施这些限制的服务处理器可能能够绕过此文档所概述的 BIOS 保护。因此，它们必须被信任以保护 BIOS，即使它们在其正常操作中并未被用于 BIOS 更新。这样的服务处理器应该被视为可信根，并且满足 5.1 节的要求。

