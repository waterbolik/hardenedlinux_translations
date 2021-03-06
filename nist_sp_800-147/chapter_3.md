# 第 3 章 化解威胁

BIOS 是安全系统中的重要组成部分。作为在启动过程中首先被执行的代码，系统 BIOS 被系统中的软硬件组件隐含地信任。上述章节描述了系统 BIOS 在启动过程中的作用、它对攻击者的吸引力，以及可能导致对 BIOS 的未经授权的修改的潜在威胁。本章呈现了 BIOS 实现的安全指导意见以及在企业环境中推荐的 BIOS 管理实践。3.1 节提供了安全 BIOS 更新过程的指导意见，它本意是用于平台厂商设计、实施或者选择一种 BIOS 实现。尽管产品可能不会立即可获得，组织机构可以在它们投入采购过程时采用这些指导意见，并且开始开发计划，以便在产品可获得时利用这些安全特性。组织机构可以在开发这些计划时使用 3.2 节所建议的 BIOS 管理实践。这些建议本意是防止对 BIOS 的未经授权的修改。

## 3.1 对于系统 BIOS 实现的安全指导意见

本节提供的指导意见的本意是在供货之后通过防护用于更新 BIOS 的机制来维持 BIOS 的完整性。特别地，本节定义了用于安全 BIOS 更新机制的系统 BIOS 实现的指导意见。安全的 BIOS 更新机制包括：

1. 一种过程，用于验证 BIOS 更新的合法性和完整性
2. 一种机制，用于确保 BIOS 受到保护，不受安全更新过程以外的修改。

认证过程确认 BIOS 更新镜像是由合法的来源生成的，并且未被替换。所有系统 BIOS 更新应该要么执行 3.1.1 节所描述的认证 BIOS 更新机制，要么使用一种符合 3.1.2 节中的指导意见的最优安全本地更新机制。

这些安全 BIOS 更新机制指导意见并不能化解与系统 BIOS 相关联的全部风险。某些对于系统 BIOS 的未经授权的修改的威胁仍然存在。例如，这些指导意见不能防止对系统拥有物理访问的个人修改系统 BIOS，它们也不能保证系统 BIOS 实现没有漏洞。关于系统 BIOS 的指导意见应当与组织已有的安全策略和过程联用。

### 3.1.1 BIOS 更新认证

认证 BIOS 更新机制使用数字签名以保证 BIOS 更新镜像的合法性。如需使用认证 BIOS 更新机制来更新 BIOS，应该有一个更新可信根（RTU），它包含一种签名验证算法以及一个包含了验证 BIOS 更新镜像的签名所需的公钥的密钥存储器。此密钥存储器和签名验证算法应该以一种受保护的方式存储于计算机系统上，并且应该仅可使用认证更新机制或者 3.1.2 节所列举的一种安全本地更新机制来修改。

存储于 RTU 中的密钥应该包括用于验证 BIOS 更新镜像的签名的公钥，或者在公钥的一份副本由 BIOS 更新镜像提供的情况下包含此公钥的散列值 \[FIPS180-3\]。在后一种情况下，更新机制应该计算由 BIOS 更新镜像所提供的公钥的散列值，以确保它与出现在密钥存储器中的散列值相匹配，然后再用所提供的公钥来验证 BIOS 更新镜像的签名。

BIOS 镜像应该以符合 NIST SP 800-89，_Recommendation for Obtaining Assurances for Digital Signature Applications_（关于获得数字签名应用程序的担保的建议）\[SP800-89\] 的方式签名，使用一种在 NIST FIPS 186-3，_Digital Signature Standard_（数字签名标准）\[FIPS186-3\] 中具体说明的一种许可的数字签名算法，它提供至少 112 位的安全强度，以符合 NIST SP 800-131A，_Transitions: Recommendation for Transitioning the Use of Cryptographic Algorithms and Key Lengths_（过渡：关于密码学算法和密钥长度的使用的过渡的建议）\[SP800-131A\] 的要求。

更新机制应该保证 BIOS 更新镜像经过数字签名，并且在更新 BIOS 之前，该数字签名可以使用 RTU 中的密钥进行验证。恢复机制也应该使用认证更新机制，除非恢复过程符合安全本地更新指导意见的要求。认证更新机制应该能够防止未经授权地将 BIOS 回滚到一个带有已知的安全弱点的早期认证版本。这种回滚限制机制可以通过例如验证 BIOS 镜像的版本号大于当前所安装的 BIOS 镜像的版本号等方式来实现。

某些组织可能想要在高度安全环境下主张对于 BIOS 更新的更大控制权。认证更新机制可以被设计为允许组织对于更新过程的控制，在此，更新 BIOS 或者回滚至早期版本的操作仅当此更新或者回滚过程得到组织授权时才被允许。例如，特定的 BIOS 镜像可以被组织许可，通过使用由组织控制的密钥对其附署签名，这可以在更新过程中被验证。

### 3.1.2 安全本地更新

BIOS 实现可以可选地包括一种安全本地更新机制，以便在不使用认证更新机制的情况下更新系统 BIOS。安全本地更新机制如果被实施，应该仅被用于加载首个 BIOS 镜像，或者从一个不能由 3.1.1 节描述的认证更新机制修复的系统 BIOS 损坏中恢复。安全本地更新机制应该通过要求物理存在来保证 BIOS 更新镜像的合法性和完整性。安全本地更新机制中的未来的保护可以通过在允许更新系统 BIOS 之前要求输入管理员口令或者解锁某个物理锁（例如某个主板跳线）来实现。

### 3.1.3 完整性保护

为了防止认证 BIOS 更新过程以外的针对系统 BIOS 的无意或者恶意的修改，RTU 和系统 BIOS（不包括那些存储于非易失性存储器中的被系统 BIOS 所使用的配置数据）应该通过某种在认证 BIOS 更新以外不能被超越的机制保护起来，使其不会受到无意或者恶意的修改。此保护机制本身也应该被保护起来，使其不会受到非授权的修改。

认证 BIOS 更新机制应该被某种机制保护起来，使其不会受到无意或者恶意的修改。此机制至少和保护 RTU 和系统 BIOS 的机制一样强。

此保护机制应该在执行任何无需使用认证更新机制或者安全本地更新机制就能被修改的固件或者软件前保护包含系统 BIOS 的系统闪存的相关区域。这种保护应该由除了通过认证更新机制以外不可更改的硬件机制来强制执行。

### 3.1.4 不可绕过性

认证 BIOS 更新机制应该是在没有贯穿于安全本地更新机制的物理介入的情况下更新系统 BIOS 的唯一机制。系统及其附带的系统组件和固件的设计应该保证没有任何机制可以允许系统处理器或者任何其他系统组件绕过认证更新机制，除了安全本地更新机制以外。任何诸如此类能够绕过认证更新机制的机制可能会创建一种漏洞以允许恶意软件利用来自非法来源的 BIOS 镜像修改系统 BIOS 或者重写系统闪存。

现代平台拥有这样的设计特性，它赋予系统组件对于系统 BIOS 的直接访问以提升性能，例如将 BIOS 复制到内存或者将其用于系统管理模式操作。系统组件可能拥有对于 BIOS 闪存的读取访问权限，但是它们不应该能够直接修改系统 BIOS，除非是经过认证更新机制，或者通过某种要求物理介入的认证机制。例如，能够绕过主处理器的总线控制（例如，对于系统闪存的直接内存访问）不应该能够直接修改固件。同样，系统中的微控制器不应该能够直接修改固件，除非该微控制器的硬件和固件组件在 RTU 处是以相同的机制保护的。这些不可绕过性的指导意见并不适用于存储于非易失性存储器中的由系统 BIOS 所使用的配置数据。

## 3.2 关于 BIOS 管理的实践建议

本节介绍在企业操作环境中管理系统 BIOS 以撬动现存策略、过程和操作实践的考虑。它专注于围绕作为其整体平台生命周期的一部分的系统 BIOS 的供货、部署、管理和废弃处理等阶段的关键活动。在恢复阶段所执行的活动也被具体说明以处理例外情况。

**供货阶段**：组织机构在企业范围内为不同的计算机系统制定一套用于标识、列入清单和跟踪的机制以贯穿其生命周期是至关重要的。识别并监视 BIOS 镜像的特征，诸如制造商名称、版本号或者时间戳允许该组织进行更新、回滚和恢复。该组织应该在安全的离线存储中为每种许可的系统 BIOS，包括其废弃的版本维护一套“黄金主镜像”。

如果平台拥有可配置的更新可信根（RTU），该组织需要维护一套密钥存储器和签名验证算法。如果 RTU 被集成到系统 BIOS 中，那么只需维护 BIOS 黄金镜像就能满足此指导意见。如果 RTU 并未集成到系统 BIOS 中，为 RTU 提供的安全性应该至少和用于 BIOS 黄金镜像的一样强。

大多数组织机构将会依赖制造商作为经过认证的 BIOS 的来源。在这种情况下，该组织并未维持任何私钥，并且 RTU 仅包含由制造商提供的公钥。如果组织机构想要通过附署签名某些或者全部经过许可的系统 BIOS 更新来积极地参与 BIOS 认证过程，RTU 可能包含一个或者多个与该组织相关联的公钥。在这种情况下，该组织必须安全地维持对应地私钥，以使得下一次 BIOS 更新可以被签名。私钥应该采用多方控制来维护，以防止局中人攻击。对于组织的密钥，对应的公钥也必须安全地维持（以保证来源的合法性）。

此外，对于每种平台的通用配置基线必须被创建以符合组织的策略，该基线应该保证完整性保护和不可绕过性的特性被启用（如果它们可配置），并且组织的口令策略和启动设备顺序策略被强制执行。最后，每种平台的 BIOS 镜像信息和与之相关的设置基线应该被记录在配置管理计划中（脚注 2）。

> 脚注 2：参见 NIST SP 800-128 草案，_Guide for Security Configuration Management of Information Systems_（信息系统的安全配置管理指南）\[SP800-128\] 以获得关于开发配置管理计划的指导意见。

**平台部署阶段**：安全本地更新过程应该被用于从黄金主镜像为该平台提供经过许可的 BIOS。对应的 RTU 应该被安装，并且在计算机系统部署之前，与 BIOS 相关的配置参数应该被建立。这会帮助组织维护一种一致的、已知的初始状态。组织应该周期性地进行评估以确保组织的 BIOS 策略、过程和程序被恰当地遵循。

具体地，程序必须保证恰当的系统 BIOS 被安装，RTU 包含所有必需的密钥并且没有非授权的密钥，以及完整性保护和不可绕过性的特性被启用，如果它们可配置。

**操作维护阶段**：本阶段包含那些对于在操作环境中维持 BIOS 的安全性和可靠性至关重要的操作和维护活动。系统 BIOS 更新应该使用更改管理过程来实施，并且新的经过许可的版本应该被记录在配置计划中，并且注释之前的 BIOS 镜像已被其取代。

BIOS 镜像和配置基线还应该被连续监视。如果一个由此基线衍生的未经许可的版本被检测到，此事件应该被调查、记录并且作为事故响应活动的一部分而被修复。事故响应计划应该记录此过程以及可用于捕获证据以帮助确定其根本原因的经过认证的配套工具（脚注 3）。安全本地更新机制应该被用于从 BIOS 镜像攻击中恢复。

> 脚注 3：关于如何建立事故响应能力以及高效地应对事故的额外信息，参见 NIST SP 800-61 修订版本 1，_Computer Security Incident Handling Guide_（计算机安全事故处理指南）\[SP800-61\]。

如果需要新的 BIOS 镜像以扩展系统能力、改进系统可靠性或是修复软件漏洞，BIOS 更新应该使用认证更新过程来执行。如果组织积极参与更新过程，多方控制过程必须被执行以便从安全存储中获取私钥并且生成数字签名。BIOS 安装包也应该被签名，并且此数字签名应该在执行前被验证。一旦更新成功执行，配置基线应该被验证以确认该计算机系统仍然符合组织的既定策略。

**恢复阶段**：在某些情况下，所需的 BIOS 更新不能使用认证更新过程来完成。例如，损坏的系统 BIOS 或者 RTU 可能无法执行或者调用认证程序。在这种情况下，BIOS 更新可能会有意料之外的结果，迫使组织回滚到某个早期版本。对于认证更新，可能需要额外的步骤以认证回滚（如果在标准认证过程中比较了版本号或者时间戳），或者可能需要安全本地更新过程以重建安全基线。如同在操作维护阶段那样，在 BIOS 回滚或者重新安装之后验证 BIOS 配置是否满足组织的既定策略是至关重要的。

**废弃处理阶段**：在计算机系统被废弃处理并且离开组织之前，组织应该从系统 BIOS 中移除或者销毁任何敏感数据。配置基线应该被重置为制造商的默认设置；特别地，诸如口令等敏感设置应该从系统中删除，密钥也应该从密钥存储器中移除。如果系统 BIOS 包含任何组织特定的自定义，那么由厂商提供的 BIOS 镜像应该被安装。平台生命周期的这一阶段减少了意外数据泄露的机会。

