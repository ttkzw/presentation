---
marp: true
title: DNS as Code — コードとしてのゾーン管理 —
size: 16:9
theme: my-theme
headingDivider: 3
header: "DNS as Code — コードとしてのゾーン管理 —"
footer: "TAKIZAWA, Takashi"
paginate: true
---

# DNS as Code<br>— コードとしてのゾーン管理 —
<!--
class: title
_header: ""
_footer: ""
_paginate: false
-->

- 所属：さくらインターネット株式会社
- 氏名：滝澤隆史

## 自己紹介
<!--
class: body
-->




## “DNS as Code”とは
<!--
class: heading
-->


### “DNS as Code”とは
<!--
class: body
-->

- “DNS as Code”を明確に定義したものはない
- [OctoDNS](https://github.com/octodns/octodns/)
    - 2017年3月公開
    - 公開当初（v0.8.0）のREADME.mdの見出しに「DNS as code - Tools for managing DNS across multiple providers」という記述がある
- 『[DevOps and DNS](https://www.oreilly.com/library/view/devops-and-dns/9781492049241/)』（O'Reilly Media, Inc.）
    - 2017年7月にリリースされたレポート
    - 著者：Andy Still (Intechnica), Phil Stanhope (Oracle Dyn)）
    - “Chapter 4. Managing DNS in a DevOps Culture”に“DNS as Code”についての言及がある

### “DNS as Code”とは

- 


### CI/CD



## DNS as Codeの実装
<!--
class: heading
-->

### DNS as Codeの実装
<!--
class: body
-->

- マネージドDNSプロバイダー提供プロビジョニングツール
- [Terraform](https://www.terraform.io/)/[OpenTofu](https://opentofu.org/)
- [OctoDNS](https://github.com/octodns/octodns)
- [dnscontrol](https://github.com/StackExchange/dnscontrol)

※本資料では特定のマネージドDNSプロバイダー依存ではないツールとしてOctoDNSとdnscontrolを主に取り上げる。

### 【参考】マネージドDNSプロバイダー提供プロビジョニングツール

Amazon Route 53をAWS CloudFormationでプロビジョニングする例を[公式ドキュメント](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/quickref-route53.html)からその設定例を紹介する。

```json
"myDNSRecord" : {
  "Type" : "AWS::Route53::RecordSet",
  "Properties" : 
  {
    "HostedZoneId" : "Z3DG6IL3SJCGPX",
    "Name" : "mysite.example.com.",
    "Type" : "SPF",
    "TTL" : "900",
    "ResourceRecords" : [ "\"v=spf1 ip4:192.168.0.1/16 -all\"" ]
  }
}
```



### 【参考】Terraform/OpenTofu

[Resource: aws_route53_record](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route53_record)

```hcl
resource "aws_route53_record" "www" {
  zone_id = aws_route53_zone.primary.zone_id
  name    = "www.example.com"
  type    = "A"
  ttl     = 300
  records = [aws_eip.lb.public_ip]
}
```

## OctoDNS
<!--
class: heading
-->

### OctoDNSとは
<!--
class: body
-->


## dnscontrol
<!--
class: heading
-->

### dnscontrolとは
<!--
class: body
-->



## まとめ
<!--
class: heading
-->

### まとめ
<!--
class: body
-->



