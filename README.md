# tcpip-lab

TCP/IPと関連ネットワーク技術を、Cによる実装と実験を通して低レイヤから理解するためのリポジトリです。
対象OSはLinuxです。自作TCP/IPスタックの完成を当面の目標とはせず、プロトコルごとに小さな技術検証を積み重ねます。

## 方針

- Ethernet・ARPなど、学習対象のパケットは自分で組み立て、解析する。
- 3rd partyライブラリは原則使わない。OS・NICとの境界にはLinux APIを利用する。
- 共通化や抽象化より、処理をコードから読み取れることを優先する。
- 実装だけでなく、予想・観測結果・制約・気付きを残す。

## 最初のテーマ：ARP

初回の到達点は、同一リンク上の相手にARP Requestを送信し、ARP ReplyからIPv4アドレスとMACアドレスの対応を読み取ることです。
LinuxのNetwork Namespaceとvethで接続した2台相当の環境を使い、相手側のLinuxカーネルが返すReplyを解析します。

- [ARPの検証計画・実験手順](experiments/arp/README.md)
- [ARPの仕様・実装境界](experiments/arp/spec.md)
- [作業ルール](AGENTS.md)
- [元の引き継ぎ資料](tcpip-lab_handoff.md)

現在は準備段階です。送受信プログラム・Makefile・環境構築スクリプトはまだありません。
macOSでは編集と一部のオフライン検証を行い、Linux固有の送受信・ネットワーク実験はLinux環境で行います。

## 今後の候補

ARP → ICMP → IPv4 / ルーティング → UDP → TCP → DNS → HTTPを候補とし、必要に応じて順序を調整します。
HTTP/2・HTTP/3・QUIC、NAT・Firewall・Reverse Proxy・Load Balancer、パケット解析も後続テーマです。
