---
marp: true
title: シェルの歴史
size: 16:9
theme: my-theme
headingDivider: 4
header: "Unixシェルの歴史"
footer: "TAKIZAWA, Takashi"
paginate: true
---

# Unixシェルの歴史
<!--
class: title
_header: ""
_footer: ""
_paginate: false
-->

- 未発表資料
    - 2024-11-10 最終更新
- 所属：さくらインターネット株式会社
- 氏名：滝澤隆史

## 自己紹介
<!--
class: body
-->

- 氏名：滝澤隆史
- 所属：さくらインターネット株式会社
    - 2024年2月から
    - クラウドの中の人をやっている

## 背景
<!--
class: body
-->

- Software Design 2024年12月号に以下の記事を寄稿
    - 第1特集 シェルスクリプトの基本と罠 コンテナ、クラウド、Web開発、なにかと使える基礎技術
        - 第1章：シェルスクリプトの基礎
        - 第2章：シェルスクリプトの基本文法
- テーマのスコープ外であったり、ページ数の都合だったりで記事に書ききれなかったものを含めてまとめてみた

## 概要

- Unixシェルの歴史

## シェルの起源
<!--
class: heading
-->

### RUNCOM
<!--
class: body
-->

- Louis Pouzin（ルイ・プザン）によりCTSS向けに開発されたプログラム
    - CTSS（Compatible Time-Sharing System）はMITで1963年から64年にかけて開発されたタイムシェアリングシステム
- シェルスクリプトの起源
- >a sort of shell driving the execution of command scripts, with argument substitution
- >引数の置換ができる、コマンドスクリプトを実行するシェルのようなも
- 参考文献
    - 『[The Origin of the Shell](https://www.multicians.org/shell.html)』（Louis Pouzin（ルイ・プザン））

### SHELL

- Louis Pouzin（ルイ・プザン）はMulticsのコマンド言語がどのように設計できるかを説明する論文を書いた。その名称として「SHELL」という言葉を作った。
    - [The SHELL: A Global Tool for Calling and Chaining Procedures in the System](https://people.csail.mit.edu/saltzer/Multics/Multics-Documents/MDN/MDN-4.pdf)
    - [RUNCOM: A Macro-Procedure Processor for the 636 System](https://people.csail.mit.edu/saltzer/Multics/Multics-Documents/MDN/MDN-5.pdf)

### SHELL

>We may envision a common procedure called automatically by the supervisor whenever a user types in some message at his console, at a time when he has no other process in active execution under console control (presently called command level). This procedure acts as an interface between console messages and subroutine. The purpose of such a procedure is to create a medium of exchange into which one could activate any procedure, as if it were called from inside of another program. Hereafter, for simplification, w·e shall refer to that procedure as the ''SHELL".

### SHELL

>コンソール制御下（現在コマンドレベルと呼ばれる）で他のプロセスがアクティブに実行されていない時に、ユーザーがコンソールで何らかのメッセージをタイプするたびに、スーパーバイザによって自動的に呼び出される共通のプロシージャを想定することができる。この手続きは、コンソールメッセージとサブルーチン間のインターフェースとして機能する。このようなプロシージャの目的は、あたかも他のプログラムの内部から呼び出されたかのように、任意のプロシージャをアクティブにすることができる交換媒体を作成することである。以後、簡略化のため、このプロシージャーを''SHELL''と呼ぶことにする。（DeepLによる翻訳）

### 
