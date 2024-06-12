---
marp: true
title: DNS as Code — CI/CDを利用したゾーン管理 —
size: 16:9
theme: my-theme
headingDivider: 4
header: "DNS as Code — CI/CDを利用したゾーン管理 —"
footer: "TAKIZAWA, Takashi"
paginate: true
---

# DNS as Code<br>— CI/CDを利用したゾーン管理 —
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

- 氏名：滝澤隆史
- 所属：さくらインターネット株式会社
    - 2月からお世話になっている
- DNSとの関わり
    - 何となくDNSで遊んでいる人

## 概要

- クラウド時代におけるDNSゾーン運用の課題
- “DNS as Code”とは
- “DNS as Code”の実装
    - DNSControl
    - octoDNS


## クラウド時代におけるDNSゾーン運用の課題
<!--
class: heading
-->

### クラウド時代におけるDNSゾーン運用
<!--
class: body
-->

- マネージドDNSサービスを利用することが主流になっている
- DNSゾーンの運用にAPIを利用したい
- APIを利用可能なサービスでは、
    - SDK（ソフトウェア開発キット）やツールが提供されていれば、それを利用してゾーンを運用できる
    - SDKやツールはクラウドサービスを統合管理して利用するには便利だが、DNSゾーンの運用に利用するには煩雑である（後述）
- 結局、WebUI（コントロールパネル）を利用する

### WebUI（コントロールパネル）起因による課題

- 変更管理ができない
    - 変更履歴や変更理由を残せない
        - いつ誰が何をなぜ変更したのか
    - 変更内容（差分）を確認できない
    - 問題発生時に切り戻しができない
    - レビューや承認ができない
- コメントを記述できない

#### WebUI（コントロールパネル）起因による課題の対策1

- WebUI（コントロールパネル）を使わない

#### WebUI（コントロールパネル）起因による課題の対策2

- ゾーンデータを手元でテキストファイルとして運用し、APIを利用して、プロバイダーに反映させる
    - 変更管理に起因する課題
        - GitHubやGitLabのようなバージョン管理システムのプラットフォームを利用することで解決する
    - コメントの課題
        - コメントを記述できるフォーマットを利用すれば解決する
    - DNSに特化したツールを利用する
        - → “DNS as Code”（本資料のテーマ）

### マネージドDNSサービスプロバイダー起因による課題

- 大規模障害が発生したとき
    - 運用しているDNSゾーンに関する名前解決ができなくなる
    - 運営しているサービスに影響がでる
- ゾーンデータの保管
    - プロバイダーであり、手元にはない
        - 運用でカバーするしかない
            - スプレッドシート管理（辛い） 
    - 取り出したいときに取り出せるとは限らない
        - 障害時に取り出せるとは思えない

### 大規模障害発生時の対策

- あらかじめ他のプロバイダーに切り替えられる準備をしておく
- あらかじめ複数のプロバイダーを利用する

#### 他のプロバイダーに切り替えるには

- 障害時にゾーンデータを取り出せるとは限らない
- 一次情報としてゾーンデータを手元に持つ必要がある

#### 複数のプロバイダーを利用するには

- WebUI（コントロールパネル）による運用は無理がある
- 一次情報としてゾーンデータを手元に持つ必要がある
- APIを利用して、手元のゾーンデータを複数のプロバイダーに反映させる

#### 大規模障害発生時の対策のまとめ

- ゾーンデータを手元でテキストファイルとして運用し、APIを利用して、プロバイダーに反映させる
    - DNSに特化したツールを利用する
        - → “DNS as Code”（本資料のテーマ）

## “DNS as Code”とは
<!--
class: heading
-->


### “DNS as Code”とは
<!--
class: body
-->

- “DNS as Code”を明確に定義したものはない
- “DNS as Code”に言及されている情報を見ていく

### DNSControl: A DSL for DNS as Code from StackOverflow.com

- https://www.usenix.org/conference/srecon17americas/program/presentation/peterson
![srecon-dnscontrol](images/srecon-dnscontrol.png)

#### DNSControl: A DSL for DNS as Code from StackOverflow.com

- 2017年3月14日
- SREcon17 AmericasでのDNSControlについての発表
- DNSControlはDNS as Codeの実装の1つ

### octoDNS - README.md(v0.8.0)

- https://github.com/octodns/octodns/blob/7957a4c018f729e47ce976fa89f065284b959a52/README.md
![README.md](images/octodns-readme-v0.8.0.png)

#### octoDNS - README.md(v0.8.0)

- 2017年3月16日
- octoDNSはDNS as Codeの実装の1つ
- 公開当初（v0.8.0）のREADME.mdの見出しに「DNS as code - Tools for managing DNS across multiple providers」という記述がある

### Introducing DnsControl – “DNS as Code” has Arrived

- https://blog.serverfault.com/2017/04/11/introducing-dnscontrol-dns-as-code-has-arrived/
![Introducing DnsControl – “DNS as Code” has Arrived](images/introducing-dnscontrol.png)

#### Introducing DnsControl – “DNS as Code” has Arrived

- 2017年4月11日
- DNSControlはDNS as Codeの実装の1つ
- DNSControlの開発元のStack Exchange社のブログ記事
- 記事のタイトルに“DNS as Code”が含まれている

### DevOps and DNS

- https://www.oreilly.com/library/view/devops-and-dns/9781492049241/
![DevOps and DNS](images/devops-and-dns.png)

#### DevOps and DNS

- 2017年7月
- 著者：Andy Still (Intechnica), Phil Stanhope (Oracle Dyn)
- O'Reilly Mediaのレポート
    - 注意）O’Reilly learning platformのサブスクリプションが必要
- “Chapter 4. Managing DNS in a DevOps Culture”に“DNS as Code”についての言及がある
- 概要箇所を要約すると
    - すべてのDNSの変更を動的APIで管理できるようになれば、すべてのDNSレコードを含めるようにInfrastructure as Codeを拡張し、コードの変更管理をし始めることが次の論理的な段階だ

### DNS as Code

- https://www.akamai.com/blog/security/dns-as-code-
![DNS as Code](images/akamai.png)

#### DNS as Code

- 2020年6月
- Akamai社のブログ
- Edge DNSのDNSゾーンの管理にTerraformを利用する例を紹介している
- 実はぐぐるとトップに出てくる

### “DNS as Code”とは結局は何なの

- 2017年から登場した言葉のようである
- Infrastructure as Code (IaC)をDNSに特化したもの
- DNSゾーンをコードとして管理し、ツールを使ってゾーンデータをDNSサービスに反映する

### なぜ2017年から登場したのか

- 2016年10月のマネージドDNSサービスプロバイダーのDynへの大規模DDoSがきっかけ
![Dyn Statement on 10/21/2016 DDoS Attach](images/dyn-ddos.png)

#### How Stack Overflow plans to survive the next DNS attack

- https://blog.serverfault.com/2017/01/09/surviving-the-next-dns-attack/
![How Stack Overflow plans to survive the next DNS attack](images/stackexchange-blog.png)

#### How Stack Overflow plans to survive the next DNS attack

- 2017年1月に公開されたStack Exchange社のブログ
- 2016年10月のDynへの大規模DDoS攻撃を背景として、次に同様な攻撃が発生したときにどのようなアプローチをとれるかを検討した記事
    - さまざまなDNSプロバイダーとその選択方法をベンチマークする
    - 複数のDNSプロバイダーを導入する
    - DNSを意図的に破壊し、その影響を測定する
    - 我々の仮定を検証し、DNS標準の実装をテストする
- その後、DNSControlを公開することになる

#### “DNS as Code”の実装が公開

- 2017年3月14日：DNSControl v0.1.0公開
- 2017年3月16日：octoDNS v0.8.0公開

### “DNS as Code”の実装の主な特徴

- DNSControlとoctoDNSの主な特徴
    - ゾーンをコードとして記述するテキストファイル
        - DNSControl: JavaScript
        - octoDNS: YAML、マスターファイル
    - 複数のDNSサービスプロバイダーに対応
    - 既存のDNSサービスプロバイダーからのインポートに対応
    - プレビュー/Dry Run機能により実際に登録されているゾーンデータからの更新内容の確認

### コード（テキストファイル）であることの利点

- コメントを記述できる
- Gitのようなバージョン管理システムを利用できる
- GitHubやGitLabのようなバージョン管理システムのプラットフォームを利用できる

#### Gitのようなバージョン管理システムを利用できる

- 変更履歴や変更理由を残せる
- 変更内容（差分）を確認できる
- 問題発生時に切り戻しができる

#### GitHubやGitLabのようなバージョン管理システムのプラットフォームを利用できる

- レビューや承認ができる
    - プルリクエストやマージリクエスト
- CI（継続的インテグレーション）が利用できる
    - 構文チェック
    - 更新内容の確認（プレビュー/Dry Run機能の利用）
- CD（継続的デリバリー）が利用できる
    - DNSサービスプロバイダーへのゾーンの反映

## DNS as Codeの実装
<!--
class: heading
-->

### DNS as Codeの実装
<!--
class: body
-->

- クラウドサービスプロバイダー提供プロビジョニングツール
- [Terraform](https://www.terraform.io/)/[OpenTofu](https://opentofu.org/)
- [DNSControl](https://github.com/StackExchange/dnscontrol)
- [octoDNS](https://github.com/octodns/octodns)

本資料では特定のマネージドDNSサービスプロバイダー依存ではないツールとしてDNSControlとoctoDNSを主に取り上げる。

### リソースレコードの記述例

- リソースレコードの記述しやすさ
    - リソースレコードの数が少なけば、それほど問題にならない
    - リソースレコードの数が多いと、記述しやすさは重要である
- リソースレコードの記述例をそれぞれの公式ドキュメントから見てみる

#### AWS CloudFormation (Amazon Route 53)

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

https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/quickref-route53.html

#### Azure Resource Manager template (Azure DNS)

```json
    {
      "type": "Microsoft.Network/dnsZones/A",
      "apiVersion": "2018-05-01",
      "name": "[format('{0}/{1}', parameters('zoneName'), parameters('recordName'))]",
      "properties": {
        "TTL": 3600,
        "ARecords": [
          {
            "ipv4Address": "1.2.3.4"
          },
          {
            "ipv4Address": "1.2.3.5"
          }
        ]
      },
略
    }
```

https://learn.microsoft.com/en-us/azure/dns/dns-get-started-template

#### Google Cloud Deployment Manager (Google Cloud DNS)

```yaml
- name: {{ properties["rrsetName"] }}
  type: gcp-types/dns-v1:resourceRecordSets
  properties:
    name: {{ properties["rrsetDomain"] }}
    managedZone: $(ref.{{ properties["zoneName"] }}.name)
    records:
    - type: A
      ttl: 50
      rrdatas:
      - 10.40.10.0
```

https://github.com/GoogleCloudPlatform/deploymentmanager-samples/blob/master/google/resource-snippets/dns-v1/one_a_record.jinja

#### Terraform/OpenTofu (Amazon Route 53)

```h
resource "aws_route53_record" "www" {
  zone_id = aws_route53_zone.primary.zone_id
  name    = "www.example.com"
  type    = "A"
  ttl     = 300
  records = [aws_eip.lb.public_ip]
}
```

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route53_record


#### Terraform/OpenTofu (Azure DNS)

```h
resource "azurerm_dns_a_record" "example" {
  name                = "test"
  zone_name           = azurerm_dns_zone.example.name
  resource_group_name = azurerm_resource_group.example.name
  ttl                 = 300
  records             = ["10.0.180.17"]
}
```

https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/dns_a_record

#### Terraform/OpenTofu (Google Cloud DNS)

```h
resource "google_dns_record_set" "a" {
  name         = "backend.${google_dns_managed_zone.prod.dns_name}"
  managed_zone = google_dns_managed_zone.prod.name
  type         = "A"
  ttl          = 300

  rrdatas = ["8.8.8.8"]
}
```

https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/dns_record_set

#### DNSControl

- JavaScriptベースのDSL

```javascript
  A("test", "5.6.7.8")
```

https://github.com/StackExchange/dnscontrol

#### octoDNS

- YAML

```yaml
---
'':
  ttl: 60
  type: A
  values:
    - 1.2.3.4
    - 1.2.3.5
```

https://github.com/octodns/octodns

#### 【参考】マスターファイル（ゾーンファイル）

```
test 300 IN A 192.0.2.1
```

### リソースレコードの設定例のまとめ

- クラウドサービスプロバイダー提供プロビジョニングツールとTerraform/OpenTofu
    - プロバイダーにより記述方法が異なる
    - リソースレコードセットごとにリソースを定義するため、記述が冗長である
        - 数個だけであれば大変ではないが、100個あるときはどうだろうか
- DNSControlとoctoDNSとマスターファイル
    - DNSに特化しているため、記述が簡潔である

## DNSControl
<!--
class: heading
-->

### DNSControlとは
<!--
class: body
-->

- Stack Exchange社が開発しているDNSゾーンの保守ツール
    - Stack Exchange社はStack Overflow（開発者向けのQ&Aサイト）やServer Fault（システム・ネットワーク管理者向けのQ&Aサイト）の運営元
- 公式サイト
    - https://docs.dnscontrol.org/
- 次の2つから構成される
    - DNSゾーンを記述するDSL
        - DSL: ドメイン固有言語、domain specific language
    - DSLを処理し、DNSプロバイダーにゾーン情報を反映するソフトウェア


### 背景・経緯

- 2016年10月：Dynへの大規模DDoS
- 2017年1月9日：ブログ記事『[How Stack Overflow plans to survive the next DNS attack](https://blog.serverfault.com/2017/01/09/surviving-the-next-dns-attack/)』
- 2017年3月14日：SREcon17 Americas『[DNSControl: A DSL for DNS as Code from StackOverflow.com](https://www.usenix.org/conference/srecon17americas/program/presentation/peterson)』
- 2017年3月14日：v0.1.0公開
- 2017年4月11日：ブログ記事『[Introducing DnsControl – “DNS as Code” has Arrived](https://blog.serverfault.com/2017/04/11/introducing-dnscontrol-dns-as-code-has-arrived/)』
- 2023年5月19日：v4.0.1リリース

### DNSControlの概要

- 公式サイト（https://dnscontrol.org/）より
    - DNSデータを高レベルDSとして管理し、マクロや変数を使用して更新を容易にする
    - ベンダーロックインを排除。DNSプロバイダーを、いつでも、簡単に、完全にそのまま切り替えられる
    - BIND、AWS Route 53、Google DNS、name.comなど35以上のDNSプロバイダーをサポート
    - DNSゾーンデータにGit（または任意のVCS）のすべての利点を。履歴を見たり、PRを受け入れたり

### DNSControlの概要

- 公式サイト（https://dnscontrol.org/）より
    - IPアドレスを定数に割り当て、コンフィギュレーション全体でその変数名を使用する
    - 障害ポイントの削減：デュアルDNSプロバイダーを簡単に維持し、ダウンしたDNSプロバイダーを簡単に停止できる
    - CI/CDの原則をDNSに適用する：ユニットテスト、システムテスト、自動デプロイメント
    - SPFオプティマイザでDNSを最適化。多すぎるルックアップを検出。フラット化

### DNSControlの設定ファイル

- creds.json：プロバイダー定義（認証情報含む）
- dnsconfig.js：ゾーン設定

#### プロバイダー定義（認証情報含む）

- creds.json

```json
{
  "sakuracloud": {
    "TYPE": "SAKURACLOUD",
    "access_token": "$SAKURACLOUD_ACCESS_TOKEN",
    "access_token_secret": "$SAKURACLOUD_ACCESS_TOKEN_SECRET"
  }
}
```

- ここでの`sakuracloud`はプロバイダーを指定する任意の名前
- `TYPE`はプロバイダーのタイプ識別子
- 他のパラメーターは認証情報やAPIに関連するもので、プロバイダーにより異なる

#### ゾーンファイル（レジストラー、プロバイダー定義）

- dnsconfig.js

```javascript
var REG_NONE = NewRegistrar("none");
var DSP_SAKURACLOUD = NewDnsProvider("sakuracloud");
```

- ゾーンの定義はJavaScriptの記法で行う。あらかじめ、関数や修飾子が用意されている
- `NewRegistrar`にはレジストラーを指定する。なければ、`none`を指定する
- `NewDnsProvider`にはcreds.jsonに記述したプロバイダーを指定する

#### ゾーンファイル（ゾーン定義）

- dnsconfig.js

```javascript
D("dnsbeer.com", REG_NONE, DnsProvider(DSP_SAKURACLOUD),
  DefaultTTL(3600),
  HTTPS("@", 1, "pale-ale.dnsbeer.com.", ""),
  A("pale-ale", "192.0.2.2"),
END);
```

- ゾーンは関数`D`の引数として記述し、引数は`END`で終わる
- ゾーン名（“.”で終わらない）、レジストラー、プロバイダーを指定する
- リソースタイプごとの修飾子を使ってリソースレコードを記述する
- リソースタイプによってはRDATAをそのまま記述するのではなく、要素ごとに記述する

### DNSControlの実行例

- 実行例からどういうことができるかを確認する

#### プレビュー

```sh
dnscontrol preview
```

![dnscontrol preview](images/dnscontrol-preview.png)

- 作成、更新、削除されるリソースレコードが出力される
- 各種チェックも行う
    - 構文チェック、MX/CNAMEの絶対ドメイン名チェック

#### プロバイダーへの反映

```sh
dnscontrol push
```

![dnscontrol push](images/dnscontrol-push.png)

- 作成、更新、削除されるリソースレコードが表示され、プロバイダーに反映される

#### インポート（マスターファイル形式）

```sh
dnscontrol get-zones --format=zone プロバイダー - ゾーン
```

![dnscontrol get-zones](images/dnscontrol-get-zones-zone.png)

- 既存のプロバイダーからゾーンをインポートしたいときに利用できる

#### インポート（dnscontrolの形式）

```sh
dnscontrol get-zones --format=js プロバイダー - ゾーン
```

![dnscontrol get-zonews](images/dnscontrol-get-zones-js.png)

- 新規に利用開始するときにはこのコマンドを使うとよい

#### リソースタイプについての注意点

- SOA：ほとんどの場合はプロバイダー側で管理しているため、記述不要
- NS：変更できないプロバイダーの場合は記述不要
- ALIAS：疑似リソースタイプはプロバイダーが対応していれば利用できる
- TXT：SPFやDMARCを利用するときには`SPF_BUILDER`や`DMARC_BUILDER`を利用できる
- CAA：`CAA_BUILDER`を利用できる

#### SPF_BUILDER

- 10 DNS lookupsのチェックあり
- https://docs.dnscontrol.org/language-reference/domain-modifiers/spf_builder

```javascript
D("example.com", REG_MY_PROVIDER, DnsProvider(DSP_MY_PROVIDER),
  A("@", "10.2.2.2"),
  MX("@", "example.com."),
  SPF_BUILDER({
    label: "@",
    overflow: "_spf%d",
    raw: "_rawspf",
    ttl: "5m",
    parts: [
      "v=spf1",
      "ip4:198.252.206.0/24", // ny-mail*
      "ip4:192.111.0.0/24", // co-mail*
      "include:_spf.google.com", // GSuite
      略
      "~all"
    ]
  }),
END);
```

### フォーマッターを使っているときの注意点

- PrettierやBiomeなどのフォーマッターを利用していると次のように整形されることがある
- DNSControlにおいては最後に引数の末尾のカンマは許容されないので、`trailingComma`の設定を`es5`にする

```javascript
D(
  "example.com",
  REG_MY_PROVIDER,
  DnsProvider(DSP_MY_PROVIDER),
  A("@", "192.0.2.1"),
  A("foo", "192.0.2.2"),
  END, ←このカンマは許容されない
);
```

## octoDNS
<!--
class: heading
-->

### octoDNSとは
<!--
class: body
-->

- GitHub社が開発・保守しているオープンソースソフトウェア
- DNS as code - Tools for managing DNS across multiple providers
- https://github.com/github/octodns


### 背景・経緯

- 2016年10月：Dynへの大規模DDoS
- 2017年3月16日：v0.8.0公開
- 2017年4月27日：ブログ記事『[Enabling DNS split authority with OctoDNS](https://github.blog/2017-04-27-enabling-split-authority-dns-with-octodns/)』
- 2017年5月31日：ブログ記事『[DNS Infrastructure at GitHub](https://github.blog/2017-05-31-dns-infrastructure-at-github/)』
- 2023年8月1日：v1.0.0リリース

### CLIツール

- octodns-sync
    - ソースプロバイダーのゾーン情報をターゲットプロバイダーにAPIで同期する

```sh
$ octodns-sync --config-file=./config/production.yaml --doit
...
```

### octoDNSの設定ファイル



#### プロバイダー定義（認証情報含む）

```yaml
---
providers:
  config:
    class: octodns.provider.yaml.YamlProvider
    directory: ./config
    default_ttl: 3600
    enforce_order: True
  ns:
    class: octodns_ns1.Ns1Provider
    api_key: env/NS1_API_KEY
  route53:
    class: octodns_route53.Route53Provider
    access_key_id: env/AWS_ACCESS_KEY_ID
    secret_access_key: env/AWS_SECRET_ACCESS_KEY
```

#### ゾーンごとのプロバイダーの指定

```yaml
zones:
  # This is a dynamic zone config. The source(s), here `config`, will be
  # queried for a list of zone names and each will dynamically be set up to
  # match the dynamic entry.
  '*':
    sources:
      - config
    targets:
      - ns1
      - route53
```

#### ゾーンファイル（YamlProvider）

```yaml
---
'':
  ttl: 60
  type: A
  values:
    - 1.2.3.4
    - 1.2.3.5
```

#### ゾーンファイル（ZoneFileProvider）

- マスターファイル形式のゾーンファイルを利用できる

### octoDNSの実行例（DRY RUN）

- デフォルトはDRY RUNとして動作する

```sh
$ octodns-sync --config-file=./config/production.yaml
...
********************************************************************************
* example.com.
********************************************************************************
* route53 (Route53Provider)
*   Create <ARecord A 60, example.com., [u'1.2.3.4', '1.2.3.5']>
*   Summary: Creates=1, Updates=0, Deletes=0, Existing Records=0
* dyn (DynProvider)
*   Create <ARecord A 60, example.com., [u'1.2.3.4', '1.2.3.5']>
*   Summary: Creates=1, Updates=0, Deletes=0, Existing Records=0
********************************************************************************
...
```

### octoDNSの実行例（反映）

- 実際に反映するためには --doitオプションを付ける

```sh
$ octodns-sync --config-file=./config/production.yaml --doit
...
```

### octoDNSが対応しているプロバイダー





## マスターファイル（ゾーンファイル）
<!--
class: heading
-->

### マスターファイル（ゾーンファイル）
<!--
class: body
-->



## 編集環境の注意点
<!--
class: heading
-->

### .editorconfig
<!--
class: body
-->

- 複数人で編集したときに以下のことが生じないように`.editorconfig`を用意する
    - タブとスペースが混在する
    - インデントのスペースの桁数が統一されていない
    - 最終行が改行で終わったり終わらなかったりする

```ini
root = true

[*]
indent_style = space
indent_size = 2
tab_width = 2
end_of_line = lf
charset = UTF-8
trim_trailing_whitespace = true
insert_final_newline = true
```

### .editorconfigをサポートしていないエディター

- プラグインを入れて利用できるようにすることを徹底させる
    - Vim用プラグイン
        - https://github.com/editorconfig/editorconfig-vim
        - Vim 9.0.1799, Neovim 0.9以降ではバンドルされている
    - Emacs用プラグイン
        - https://github.com/editorconfig/editorconfig-emacs


### JavaScriptのフォーマッターの設定

Prettier (.prettier)

```json
{
  "trailingComma": "es5"
}
```

Biome (biome.json)

```json
{
  "javascript": {
    "formatter": { "trailingComma": "es5" }
  }
}
```


## まとめ
<!--
class: heading
-->

### まとめ
<!--
class: body
-->



