### 暗号の世界の言葉

- 暗号化 (encrypt) / 復号化 (decrypt)
  - 暗号化と符号化 (encoding) を間違えないこと. 符号化は, m -> 01101101, というようなビット列への対応付にすぎない.
- 平文 (plaintext) / 暗号文 (ciphertext)
- 送信者 (sender) / 受信者 (receiver) / 盗聴者 (eavesdropper)
- 対称暗号 (symmetric cryptography) / 公開鍵暗号 (public-key cryptography)
  - 対称暗号 (共通鍵暗号): 1 つの鍵で暗号化, 同じ鍵で復号化
- 一方向ハッシュ関数 (one-way hash function)
  - 正真性 (integrity) を提供する. ハッシュ関数をかけることで機密性 (confidentiality) が守られるわけではない.
  - たとえばデータが改ざんされていないことを調べるために利用する.
- メッセージ認証コード (message authentication code)
  - そのメッセージが改ざんされていないこと, および期待する通信相手からのものであることを確かめる.
  - 正真性 (integrity) と認証を提供する.
- デジタル署名 (digital signature)
  - 正真性 (integrity) を確かめ, 認証と否認 (repudiation) 防止を行う. なりすまし (spoofing) を防ぐ.
    - 否認 (repudiation) ... 自分の主張をあとで翻すこと. 「そんなこと言ってません」的すっとぼけ, など.
- 擬似乱数生成器 (pseudo random number generator)
  - 乱数は暗号技術において, 鍵の生成という重要な役割を担う
- 暗号 (cryptography) / ステガノグラフィ (steganography)
  - 暗号は内容を隠す技法, ステガノグラフィはメッセージの存在そのものを隠す技法. 単純なステガノグラフィの例はタテ読み.
- どんな暗号もいつかは解読される. 弱い暗号化は暗号化しないよりも危険. 暗号はセキュリティのほんの一部.

### 脅威と特性と道具箱

セキュリティに対する脅威 | 脅かされる特性 | 防衛のための暗号技術
--|---|--
盗聴 (秘密が漏れる) | 機密性 (confidentiality) | 対称暗号 (symmetric cryptography), 公開鍵暗号 (public-key cryptography)
改竄 (情報が書き換えられる) | 正真性 (integrity) | 一方向ハッシュ関数, メッセージ認証コード, デジタル署名
なりすまし (正しい送信者のふりをする) | 認証 (authentication) | メッセージ認証コード, デジタル署名
否認 (後から私じゃないと言う) | 否認不可能性 | デジタル署名

### 問題

- Q: 平文を暗号文に変換することを暗号化と呼ぶ ○/×
- Q: 平文は人間が読むデータで, 暗号文はコンピュータが読むデータ ○/×
- Q: 対称暗号では, 暗号化の鍵と復号化の鍵は等しい ○/×

### 暗号アルゴリズムと鍵

暗号 | 暗号アルゴリズム | 鍵
--|---|--
シーザー暗号 | 平文の各文字を「指定した文字数」ずらすこと | ずらす文字数
単一換字暗号 | 「換字表」に従ってアルファベットを変換する | 換字表
エニグマ | エニグマ機械によるアルファベット変換 | 日替わりの鍵 (各種パーツ)

暗号アルゴリズムと鍵を分ける意味. 鍵は毎回交換するけど, 暗号アルゴリズムは繰り返し使用する.


### XOR

XOR (排他的論理和) は, 二回かけるともとに戻る.

- 0 XOR 0 = 0
- 1 XOR 0 = 1
- 0 XOR 1 = 1
- 1 XOR 1 = 0

あるふたつのビット列の XOR は, それぞれの桁数の bit ごとに XOR 演算してその結果.


### 使い捨てパッド (one-time pad)

無条件に安全 (unconditionally secure) であり理論的に解読不可能 (theoretically unbreakable) な暗号. 絶対に解読できない. バーナムによって考案され特許が取られている (失効済). なぜ解読できないかというと, たとえ Brute-force の途中で使い捨て鍵にたどり着いて正解の平文をゲットできたとしても, それが正しいことを判定することが出来ないから.

それでも実用的ではない. ∵ 以下のような問題がある:

- 鍵を安全に配送する事ができない. もし鍵を安全に配送できるなら, 別に暗号を使わず平文そのものを安全に送れるはずである
- 鍵自体は鍵として平文なので, これをどこかに安全に保管しておく必要がある. もし鍵を安全に保管できるなら, 別に暗号化したかったデータも安全に保管できるはずである
- 鍵の再利用が出来ない. "過去の通信記録の秘密を守る" ため, いつでもいつまでも使った鍵は秘密でなければならない
- 平文の長さに応じて鍵も長くなる
- 鍵の生成には擬似乱数ではなく, 再現性のない真の乱数を使う必要がある

=> 使い捨てパッド自体は使われていないが, アイディアはストリーム暗号 (Stream Chiper) に活かされている. ストリーム暗号では真のランダムなビット列の代わりに擬似乱数生成器によるビット列を使う


### DES & AES

DES: Data Encryption Standard. 1977 アメリカで連邦情報処理標準規格に採用された対称暗号 (FIPS 46-3). 現在は Brute-force によって現実的な時間で解読できるため, 過去の暗号を復号化する目的以外で DES を使うべきではない.

- DES は 64 bit の平文を 64 bit の暗号文に暗号化する.
- DES の基本構造はファイステルネットワーク. この構造は便利で, 他のいろいろな暗号アルゴリズムで採用されている
 - DES はファイステルネットワークを 16 ラウンド繰り返す.

AES: Advanced Encryption Standard. DES に代わる新しい暗号アルゴリズムで, 提出された複数の候補の中から Rijndeal (らいんだーる) が選ばれた

Rijndeal はファイステルネットワークの代わりに SPN 構造というものを使う

ブロック暗号アルゴリズムであり, ブロック長 128bit (= 16 bytes) で, 1 byte ごとに subbytes 処理を行う. 次に出力を混ぜてくっつける. これで 1 ラウンド, 実際は 10-14 ラウンド実行する. 鍵の長さは 128,192,256 bit から選択可能.

ref: 暗号アルゴリズムには「ブロック暗号」と「ストリーム暗号」のパターンがある. ブロック暗号は状態を持たないけど, ストリーム暗号はどこまで処理したか, という状態を持つ必要がある

対象暗号を使うためには「通信相手に安全に鍵を送らないといけない」という課題が残る (鍵配送問題). これを解決するのが後で見る公開鍵暗号.
