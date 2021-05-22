# Amazon Interactive Video Service (IVS) と AWS Amplify を使って自分だけのオリジナル配信サイトを作る！
こんにちは！ 株式会社スタートアップテクノロジー所属、 **JAWS-UG** 浜松支部の松井です！  
オンライン配信しようとした場合、 **YouTube Live** などを活用する方法が考えられますね。  
しかし、既存サービスを活用する場合カスタマイズが難しく、何かと不自由もあるかと思います。  
そこで今回は、 **AWS** で提供されている **Amazon Interactive Video Service (IVS)** と **AWS Amplify** 、  
また **StreamYard** と言うライブストリームサービスを活用して、自分だけのオリジナル配信サイトを構築する方法をご紹介します！

## 目次

1. **IVS** の設定
2. **StreamYard** の登録・設定
3. **Nuxt.js** プロジェクトのセットアップ
4. **Amplify Console** でデプロイ

## 1. **IVS** の設定

### **AWS マネジメントコンソール** にログイン
- [**AWS マネジメントコンソール**](https://console.aws.amazon.com/)にアクセスします。

***

<img width="1198" alt="スクリーンショット 2021-05-22 21 55 41" src="https://user-images.githubusercontent.com/38583473/119227442-db868e00-bb48-11eb-9d74-a43195f3dcf0.png">

- メールアドレスを入力して、**次へ**をクリックします。

***

<img width="1198" alt="スクリーンショット 2021-05-22 22 03 06" src="https://user-images.githubusercontent.com/38583473/119227950-6ff1f000-bb4b-11eb-9163-0534c30c4fc0.png">

- セキュリティチェックを入力して、**送信**をクリックします。

***

<img width="1198" alt="スクリーンショット 2021-05-22 22 18 01" src="https://user-images.githubusercontent.com/38583473/119228043-032b2580-bb4c-11eb-8de0-ff720c362ef1.png">

- パスワードを入力して、**サインイン**をクリックします。

***

### IVS チャネルを作成

<img width="887" alt="スクリーンショット 2021-05-22 22 30 10" src="https://user-images.githubusercontent.com/38583473/119228605-b137cf00-bb4e-11eb-879c-e062fac00f6c.png">

- **ivs** と入力して、 **Amazon Interactive Video Service** をクリックします。

***

<img width="887" alt="スクリーンショット 2021-05-22 22 44 26" src="https://user-images.githubusercontent.com/38583473/119228776-88640980-bb4f-11eb-8624-219168e7a167.png">

- **リージョンを 米国西部（オレゴン）に変更** をクリックします。

***

<img width="1125" alt="スクリーンショット 2021-05-22 22 51 13" src="https://user-images.githubusercontent.com/38583473/119228927-58693600-bb50-11eb-9cf3-3658f473391a.png">

- **チャネルの作成**をクリックします。

***

<img width="491" alt="スクリーンショット 2021-05-22 23 00 16" src="https://user-images.githubusercontent.com/38583473/119229203-c6fac380-bb51-11eb-9814-492a884a0f63.png">

- **チャネル名**に**ivs-nuxt-1**と入力し、**チャネルの作成**をクリックします。

***

<img width="1198" alt="スクリーンショット 2021-05-22 23 07 58" src="https://user-images.githubusercontent.com/38583473/119229520-62d8ff00-bb53-11eb-8146-ceae55c2d511.png">

- 作成した **ivs-nuxt-1** 詳細ページの、**ストリーム設定**の3点をコピーして控えます。
  - **取り込みサーバー**
  - **ストリームキー**
  - **再生設定**

***

## 2. **StreamYard** の登録・設定

### **StreamYard** に登録
- [**StreamYard のトップページ**](https://streamyard.com/) へアクセスします。

***

<img width="1438" alt="streamyard_email" src="https://user-images.githubusercontent.com/38583473/119226345-8b58fd00-bb43-11eb-96a4-7f14efd390cc.png">

- 上記にメールアドレスを入力して、 **Get started** をクリックします。

***

<img width="866" alt="streamyard_confirmation" src="https://user-images.githubusercontent.com/38583473/119226490-631dce00-bb44-11eb-8169-06a62f75555f.png">

- メールが送信されてくるので、6桁の確認コードをコピーします。

***

<img width="1198" alt="スクリーンショット 2021-05-22 21 30 25" src="https://user-images.githubusercontent.com/38583473/119227518-36b88080-bb49-11eb-971d-e3840e4ff8a4.png">

- 確認コードを入力して、 **Log in** をクリックします。

***

<img width="1198" alt="スクリーンショット 2021-05-22 21 33 12" src="https://user-images.githubusercontent.com/38583473/119226708-79785980-bb45-11eb-913c-577782ca94dc.png">

- **Onward!** をクリックします。

***

<img width="1198" alt="スクリーンショット 2021-05-22 23 25 33" src="https://user-images.githubusercontent.com/38583473/119229947-21495380-bb55-11eb-8aca-48bf162d1263.png">

- **Upgrade** をクリックします。

***

<img width="1198" alt="スクリーンショット 2021-05-22 23 28 08" src="https://user-images.githubusercontent.com/38583473/119230032-79805580-bb55-11eb-8589-24543bfa9b3b.png">

- **Basic** の **Upgrade now** をクリックします。

***

<img width="575" alt="スクリーンショット 2021-05-22 23 30 15" src="https://user-images.githubusercontent.com/38583473/119230154-00353280-bb56-11eb-879d-3a091bf4ec88.png">

- カード情報を入力し、 **monthly** / **annually** を任意で選択し、 **Purchase plan** をクリックします **（注意: 料金が発生します）**。

***

<img width="575" alt="スクリーンショット 2021-05-22 23 36 16" src="https://user-images.githubusercontent.com/38583473/119230353-c31d7000-bb56-11eb-9929-f7183d4b27a8.png">

- **Return to dashboard** をクリックします。

***

<img width="1198" alt="スクリーンショット 2021-05-22 23 19 08" src="https://user-images.githubusercontent.com/38583473/119229743-4e493680-bb54-11eb-9aa2-442eb08d7cc2.png">

- **Destinations** をクリックしてから、 **Add a destination** をクリックします。

***

<img width="1198" alt="スクリーンショット 2021-05-22 23 23 02" src="https://user-images.githubusercontent.com/38583473/119229876-d29bb980-bb54-11eb-896b-7cea9e84fa4d.png">

- **Custom RTMP** をクリック

***



## Build Setup

```bash
# install dependencies
$ yarn install

# serve with hot reload at localhost:3000
$ yarn dev

# build for production and launch server
$ yarn build
$ yarn start

# generate static project
$ yarn generate
```

## Installed packages(Requied if you want to build a project from scratch)

```bash
$ yarn add copy-webpack-plugin@6 amazon-ivs-player video.js
```

For detailed explanation on how things work, check out [Nuxt.js docs](https://nuxtjs.org).
