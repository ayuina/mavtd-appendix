
# FAQ - Migrating Server Infrastructure

セミナー中にお問い合わせいただいたご質問を紹介しています。

## Windows Server 2019 への移行

### IIS アプリケーションの移行方法を教えてください

まず 3rd Party 製品であれば開発元にお問い合わせいただくのが確実です。移行手順やインストーラなどが用意されている可能性があります。

独自で保守されているアプリケーションの場合、Windows のバージョンアップであれば、
[Web Deploy](https://docs.microsoft.com/ja-jp/archive/blogs/jpiis/webdeploytool_migration)
を用いた移行が可能です。
あるいは構築手順書があると思いますので、そちらを使って新規に構築してしまうことも可能です。
なお Azure 仮想マシンへの移行であっても上記の Web Deploy や 新規構築アプローチは有効です。

また Azure の PaaS である App Service に移行を検討される場合には、
[App Service Migration Assistant](https://azure.microsoft.com/ja-jp/blog/introducing-the-app-service-migration-assistant-for-asp-net-applications/)
のご利用をご検討ください。
こちらは主に ASP.NET Web アプリケーションを対象としたアセスメント等を行う移行ツールになりますが、
PaaS への移行は IaaS に比べると各種制約が多く、そのままスムーズに移行できることは稀です。
上記の紹介記事にも非サポートの構成の記載がありますのでご確認ください。

### Windows Server 2019 ではどのエディションを利用すればよいですか

[Windows Server 2019 の Standard エディションと Datacenter エディションの比較](https://docs.microsoft.com/ja-jp/windows-server/get-started-19/editions-comparison-19)
をご参照ください。
アプリケーションのコンテナ化を検討されている場合は
[Windows 上のコンテナーに関するドキュメント](https://docs.microsoft.com/ja-jp/virtualization/windowscontainers/)
をご参照ください。

## クラウドテクノロジの統合

### 現在 Windows Server 上で動作しているアプリケーションであれば Azure 仮想マシン上での動作がサポートされますか

Microsoft 社のサーバー製品であれば
[こちら](https://support.microsoft.com/ja-jp/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)
に記載されているものがサポートされています。

オンプレミス環境の Windows サーバーで動作しているアプリケーションであれば、原理的には Azure 仮想マシンで動作させることは可能です。
しかしそのアプリケーションおよび開発元が、動作環境としての Azure をサポートしているかは別問題ですし、現在保有されているライセンスが Azure への持ち込みを許可されているか否かもご確認いただくべきです。
これらの情報に関しては各アプリケーションの開発元へお問い合わせいただくことをお勧めします。

また Azure では用意されていない、なんらかの特殊なハードウェアを必要とするアプリケーションの場合は移行は極めて難しくなります。

### Storage Migration Service で移行されるのはファイルだけですか？アクセス権も移行されますか

[移行されるフラグの一覧](https://docs.microsoft.com/ja-jp/windows-server/storage/storage-migration-service/faq#what-attributes-are-migrated-by-the-storage-migration-service)
はこちらをご参照ください。

## IaaS ワークロードのAzure への移行

### Azure Site Recovery による移行では Express Route による Private ネットワーク接続によるデータ転送が行われますか

オンプレミス環境から Site Recoveryのパブリックエンドポイントに対してのレプリケーションが必要ですので、Microsoft ピアリング（あるいは以前のパブリックピアリング）が構成されていれば可能です。詳細は
[こちら](https://docs.microsoft.com/ja-jp/azure/site-recovery/concepts-expressroute-with-site-recovery)
をご参照ください。

### Azure File Sync で更新が競合した場合はどうなりますか

Azure File Syncが変更の競合を検知した場合は両方が保持されます。
詳細は
[こちら](https://docs.microsoft.com/ja-jp/azure/storage/files/storage-files-faq)
をご参照ください。

### Azure Files のバックアップを Azure Backup で管理する場合の料金体系を教えてください

Azure Backup自体の料金に加えて、Azure Files 共有スナップショットのストレージ料金が必要になります。
詳細は
[料金表](https://azure.microsoft.com/ja-jp/pricing/details/backup/) をご参照ください。

### AzureMigrateをvSphere環境の仮想マシン移行に使用する場合、vCenter上に仮想アプライアンスなどの登録が必須になるのでしょうか

VMを物理サーバーとして扱ってネットワーク経由で情報を収集/移行する場合はvCenter上にアプライアンスを構築する必要はありませんが、
物理仮想問わず何らかのマシンで移行サーバーを構築します。
