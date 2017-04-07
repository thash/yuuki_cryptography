### 暗号の世界の言葉

- 暗号化 (encrypt) / 復号化 (decrypt)
- 平文 (plaintext) / 暗号文 (ciphertext)
- 送信者 (sender) / 受信者 (receiver) / 盗聴者 (eavesdropper)
- 対称暗号 (symmetric cryptography) / 公開鍵暗号 (public-key cryptography)
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
