title: GPG 签名方针
date: 2021/07/03
layout: post
---

此方针适用于以下密钥做出的 GPG 签名：

```
pub   rsa4096/0xA725CB57CA65CAFE 2020-05-07 [SCEA]
      Key fingerprint = 7A95 4382 9E47 5D7D 3826  B08D A725 CB57 CA65 CAFE
uid                   [ultimate] Outvi V (outloudvi) <i@outv.im>
```

您可以在以下位置获取此公钥的最新版本（通常不含其它用户的签名）：
* https://keys.openpgp.org/vks/v1/by-fingerprint/7A9543829E475D7D3826B08DA725CB57CA65CAFE
* https://outv.im/askme/pubkey.gpg
* https://outv.im/askme/pubkey.asc
* https://github.com/outloudvi/askme/blob/master/pubkey.gpg
* https://github.com/outloudvi/askme/blob/master/pubkey.asc

本方针参考了以下内容：
* Olaf Gellert 的 [GnuPG Key Signing Policy](http://www.arasca.com/olaf/pgp/policy.html)
* Aaron Toponce 的 [PGP Keysigning Policy](https://pthree.org/my-pgp-key-signing-policy/)
* Allen Zhong 的 [PGP 密钥签名策略](https://atr.me/~pgp/policy.html)

更新：
* Jul 2, 2021 - 基于 SKS keyserver 关闭和对 Keybase 的可信度调整而更新。
* Jul 2, 2021 - 调整对 SigLevel2 签名的要求。我们在过往未有进行 SigLevel2 签名，因此对过往的签名并无影响。

## 签名操作

### SigLevel0 签名

您可以发送签名请求到我的任意联系方式[1]中。签名请求中应该包含以下内容：

* 您期望让我签名的 GPG 公钥（或不短于 64 bit 的 fingerprint，如果公钥可以在公共 keyserver 上获取）
* 您期望让我签名的具体 uid（如果不是所有 uid）
* 您能够证明是待签名 uid 所述身份的信息
* 关于期望获得签名的一些说明 *（可选）*

此请求应该以此公钥签名。

此请求可以以我的公钥加密，也可以不加密。

在收到您的请求之后，我会根据您提供的信息确定是否需要进一步验证我需要确认签名的所有 uid。在信息确认完成后，我会根据您的请求进行签名，并将包含此签名的您的公钥发回给您。

### SigLevel1 签名

您可以发送签名请求到我的任意联系方式[1]中。签名请求中应该包含以下内容：

* SigLevel0 签名所包含的所有内容
* 关于期望获得 SigLevel1 签名的一些说明 *（可选）*

在收到您的请求之后，我会对每个待签署 uid 所指代的邮件地址进行验证。一个典型的验证例子：

> 我会向您的每个待签署 uid 所指代的邮件地址各回复一段验证字符串（此回复应以我的 GPG 密钥签名）。您需要从所有期望让我签名的 uid 所指代的邮件地址，相应地各发送一封标题或正文中包含我所发送的验证字符串的消息。根据实际情况，我可能会要求您使用 GPG 密钥对包含验证字符串的回复消息签名。

在信息确认完成后，我会根据您的请求进行签名，并将包含此签名的您的公钥发回给您。

### SigLevel2 签名

此签名基于以下前提发生：

* 您的 User ID 有一定的独特性。这通常代表着完全使用文学作品中虚构人物姓名的用户不符合此条件。

您可以发送签名请求到我的任意联系方式[1]中。签名请求中应该包含以下内容：

* SigLevel0 签名所包含的所有内容
* 关于期望获得 SigLevel2 签名的一些说明 *（可选）*

并且约定一次线下会面。签名请求与线下会面的发起顺序不限。

在线下会面中，您需要向我展示以下内容：

* 签名请求中 GPG 密钥的标识，例如不短于 64 bit 的 fingerprint 或 OpenKeyChain 的二维码/NFC 密钥分享内容

在信息确认完成后，我会根据您的请求进行签名，并将包含此签名的您的公钥发回给您。

## SigLevel 解释

请注意，这里对 SigLevel 的解释可能不同于 GnuPG 文档。

Level 0: 我大致确定此 uid 属于其所指代的网络身份所有。并且，虽然未进行邮件层面上的验证，我大致确定此 uid 所述的邮箱地址在我进行签名时属于此 GPG pubkey 的私钥控制者所有。

Level 1: 在 Level 0 的基础上，我通过邮件层面上的验证（或其它可信度不低于邮件验证的手段），确定此 uid 所述的邮箱地址在我进行签名时属于此 GPG pubkey 的私钥控制者所有。

Level 2: 在 Level 1 的基础上，我已经通过会面的方式（或其它可信度不低于会面的手段），验证此 GPG pubkey 的私钥控制者的身份。

Level 3: 在 Level 2 的基础上，我相信此 GPG pubkey 的私钥控制者是可信的，对 GPG 有一定理解，并能够合理地对其它人进行签名。

## 签名方针

* 我期望相互的签名（SigLevel 不一定要一致）。因此，如果您不希望进行互相签名，请不要发送签名请求。
* 在确认签名的过程中，您可以随时取消我尚未签名的密钥的签名请求。

## 脚注

[1]. 这里的「联系方式」，包括并不限于 E-mail（如果您的邮件通过 DMARC 方针校验）、Telegram、Twitter 私信等。特别地，WeChat 和 QQ 不包含在内。
