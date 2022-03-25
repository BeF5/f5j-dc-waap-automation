HTTP Load Balancer + API Definitionを用いた通信制御
----

Swagger FileのImport及び、API DefinitionはコンソールよりGUIで設定する必要があります。
`こちら <https://f5j-dc-waap.readthedocs.io/ja/latest/class1/module10/module10.html#swagger-file-api-group>`__ の手順に従って操作をしてください。

.. NOTE::
  Terraform のサンプルファイルは、API Definition の名称が ``demo-app-api-definition`` という想定となっております。
  API Definition の名称が異なる場合、生成されるChild Objectの名称も異なるため、 ``all-operations`` 、 ``base-urls`` 等に関連する名称を適切に変更してください。

パラメータの指定
~~~~

実行に必要なファイル、また実行環境に合わせたパラメータを指定してください

.. code-block:: bash
  :linenos:
  :caption: terraform 実行前作業

  $ git clone https://github.com/BeF5/f5j-dc-waap-automation
  $ cd f5j-dc-waap-automation/terraform/api-control

  $ vi terraform.tfvars
  # ** 環境に合わせて適切な内容に変更してください **
  api_p12_file     = "**/path/to/p12file**"        // Path for p12 file downloaded from VoltConsole
  api_url          = "https://**api url**"     // API URL for your tenant

  # 本手順のサンプルで表示したパラメータの場合、以下のようになります 
  myns             = "**your namespace**"      // Name of your namespace
  op_name          = "demo-origin-pool"        // Name of Origin Pool
  pool_port        = "80"                      // Port Number
  server_name1     = "**your target fqdn1**"   // Target Server FQDN1
  server_name2     = "**your target fqdn1**"   // Target Server FQDN2
  httplb_name      = "demo-echo-lb"            // Name of HTTP LoadBalancer
  mydomain         = ["echoapp.f5demo.net"]    // Domain name to be exposed
  
  cert             = "string///**base 64 encode SSL Certificate**"  // SSL Certificate for HTTPS access
  private_key      = "string///**base 64 encode SSL Private Key**"  // SSL Private Key for HTTPS access

  // Service Policy Parameter
  sp_name          = "demo-app-service-policy"

Terraform の利用
~~~~

以下コマンドを参考に実行および削除をしてください。

.. code-block:: bash
  :linenos:
  :caption: terraform の実行・削除

  # 実行前事前作業
  $ terraform init
  $ terraform plan

  # 設定のデプロイ
  $ terraform apply

  # 設定の削除
  $ terraform destroy