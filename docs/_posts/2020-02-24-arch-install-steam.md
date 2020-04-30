---
top: 1
category: 解説
tags:
  - ja
  - archlinux
  - steam
  - 解説
date: 2020-04-24
title: ArchLinuxにSteamをインストールする方法
vssue-id: 10
---

<!-- more -->

::: tip
この解説ではGitなどのコマンドがすでに使用できることを前提としています。
:::

<TOC />

## 概要

ArchLinuxを入れてよし、いざゲームするぞー！と意気込んで
sudo pacman -S steam
をやろうとした人は少なからずいるはずです。しかし、ArchLinuxはデフォルトで32bitパッケージが無効化されている為、有効化した後にインストールしてもコアダンプが発生します。今回は32bitの有効化、コアダンプの修正を解説します。

## 32bitパッケージの有効化

さて、こんな辺境の地のblogを見てる時点で大体の方はご存知でしょうが、
一応解説をArchLinuxでは32bitパッケージがデフォルトでは無効になっています。
なので、最初にいきなり

```bash
sudo pacman -S steam
```

とコンソールに打ってもパッケージが見当たらないよ！と言われてしまいます。
ということで本題です。ArchLinuxでは無効になっているだけで、32bitは有効化できます。なので、手動で有効化する方法が以下の手順です。

**/etc/pacman.conf** に以下のような行が存在します。

```
#[multilib]
#Include = /etc/pacman.d/mirrorlist
```

見てわかるとおり、これらの行は#でコメントアウトされています。
そこで、そのコメントアウトを外しましょう

```
[multilib]
Include = /etc/pacman.d/mirrorlist
```

この様に先頭についていた#を外すことによりパッケージの有効化ができます。
しかしながら、このままだとパッケージリストが更新されていないため、以下のコマンドを実行して、パッケージリストを最新の状態にしましょう。

```bash
sudo pacman -Syy
```

## Steamのインストール & パッケージのインストール

さて、ここまで来ればフィニッシュに近いです。
ではいよいよSteamをインストールしましょう。

```bash
sudo pacman -S steam
```

よし、インストールに成功した！ここで喜びに浸るのはまだ早いです。
大きな落とし穴として、ArchLinuxではSteamをインストールするだけだと、コアダンプを起こし、起動することができません。  
**そこで追加するのが32bitのnvidia driverです**

```bash
sudo pacman -S lib32-nvidia-utils
```

さて、これで遂にSteamが起動できると思います。

<div class="auther-grid">
  <article class="auther-side">
    <div class="auther-line">
        <div class="balloon1">
          <p>この記事を書いた人</p>
        </div>
        <br>
        <img
        class="auther-icon"
        src="https://repo.akarinext.org/assets/image/icon/yupix-icon.png"
        width="100"
        height="100"
        />
          <h3>ゆぴ</h3>
    </div>
  </article>
  <section class="auther-main">
    <div class="auther-main">
      本サイトでのテンプレートのデザインに手を加えたり、独自のデザインを追加している人です。主にMinecraftServerを運営しています
    </div>
  </section>
</div>

## 参考
<a class="button yx-background-color-archlinux font1 button-a-tag" style="font-size:1.5em;" href="https://wiki.archlinux.jp/index.php/Multilib"><i class="mdi mdi-arch"></i> ArchWiki</a>

## サポート

<a class="button yx-background-color-discord font1 button-a-tag" style="font-size:1.5em;" href="https://discord.gg/gsjcMQe"><i class="fab fa-discord"></i> Discord</a>