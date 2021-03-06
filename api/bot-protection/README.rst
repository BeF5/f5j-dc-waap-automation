パラメータの指定
----

``bot-protection-httplb.json`` をAPIの値として指定します。
``**<変数名>**`` が環境に合わせて変更するパラメータとなります。適切な内容に変更してください。

``Originl Pool Object`` は HTTP Load Balancer の Originl Pool 作成手順に従って作成ください

APIの利用
----

以下のサンプルを参考にAPIを実行してください。
証明書のファイル名、パスワード情報は適切な内容を指定してください。

- ファイル取得

.. code-block:: bash
  :linenos:
  :caption: APIによるオブジェクトの作成

  $ git clone https://github.com/BeF5/f5j-dc-waap-automation
  $ cd f5j-dc-waap-automation/api/bot-protection

- オブジェクトの作成

.. code-block:: bash
  :linenos:
  :caption: APIによるオブジェクトの作成 (HTTP Load Balancer の Origin Pool 設定ファイルを指定)

  # Originl Pool の作成 (HTTP LoadBalancer のパラメータを指定)
  $ curl -k https://**tenant_name**.console.ves.volterra.io/api/config/namespaces/**namespace**/origin_pools \
       --cert **/path/to/api_credential.p12-file**:**password** \
       --cert-type P12 \
       -X POST \
       -d @../http-load-balancer/base-origin-pool.json

  # HTTP LB の作成
  $ curl -k https://**tenant_name**.console.ves.volterra.io/api/config/namespaces/**namespace**/http_loadbalancers \
       --cert **/path/to/api_credential.p12-file**:**password** \
       --cert-type P12 \
       -X POST \
       -d @bot-protection-httplb.json


- オブジェクトの削除

.. code-block:: bash
  :linenos:
  :caption: APIによるオブジェクトの削除

  # HTTP LB の削除
  $ curl -k https://**tenant_name**.console.ves.volterra.io/api/config/namespaces/**namespace**/http_loadbalancers/**httplb_name** \
       --cert **/path/to/api_credential.p12-file**:**password** \
       --cert-type P12 \
       -X DELETE

  # Origin Pool の削除
  $ curl -k https://**tenant_name**.console.ves.volterra.io/api/config/namespaces/**namespace**/origin_pools/**op_name** \
       --cert **/path/to/api_credential.p12-file**:**password** \
       --cert-type P12 \
       -X DELETE

