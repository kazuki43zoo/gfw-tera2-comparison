.. _Rich:

TERASOLUNA Framewrok for Richとの機能比較
********************************************************************************

.. only:: html

 .. contents:: 目次
    :depth: 2
    :local:

.. _RichAboutRich:

TERASOLUNA Framework for Richとは
================================================================================
TERASOLUNA Framework for Richは、
Richクライアント向けのWebアプリケーションを構築するためのWebアプリケーションフレームワークであり、
Spring MVC 3.1.4をベースに構築されている。

 .. warning:: **Richのアーキテクチャについて**

    TERASOLUNA Framework for Richが使用しているSpring Frameworkのバージョンは3系だが、
    3系から導入された新しい仕組みは使用しておらず、
    **実体はSpring Frameworkの2系のアーキテクチャをベースに構築されている。**
    
    **Richが使用している一部のAPIは、3系から非推奨になっており、4系では廃止となっているものもある。**

|

.. _RichComparisonResultOverview:

比較結果の概要
================================================================================

以下に、機能性の違いの有無を一覧で示す。
個々の比較結果の詳細は、「xxxxx」を参照されたい。

.. _RichComparisonResultOverviewCommon:

共通機能
--------------------------------------------------------------------------------
以下に、フレームワークの共通系機能の機能性の違いの有無を一覧で示す。

.. tabularcolumns:: |p{0.05\linewidth}|p{0.25\linewidth}|p{0.05\linewidth}|p{0.55\linewidth}|
.. list-table::
    :header-rows: 1
    :widths: 5 25 5 55

    * - 項番
      - 機能名
      - 違い
      - 概要
    * - 1.
      - :ref:`RichComparisonResultDetailsTransactionManagement`
      - 無
      - 共にSpring Frameworkのトランザクション機能を使用する前提である。
      
        \ **利用方法が若干異なる**\。
    * - 2.
      - :ref:`RichComparisonResultDetailsDataAccess`
      - 無
      - 共にMyBatis2を使用する前提である。

        Global Frameworkは、JPA、MyBatis2、MyBatis3(1.1.0.RELEASEからサポート予定)の3つから選択。
    * - 3.
      - :ref:`RichComparisonResultDetailsJndiAccess`
      - 無
      - Spring Framework標準機能で代替可能。
    * - 4.
      - \ :ref:`RichComparisonResultDetailsUtilities`\
      - **有**
      - **Global Frameworkでは、基本的には3rdパーティーのOSSライブラリから提供されているユーティリティ機能を使用する前提である。
        推奨する依存ライブラリから提供されているユーティリティ機能で代替可能なものもあるが、代替出来ないものもある。**
 
        Global Frameworkを使用する場合は、必要に応じて別のOSSライブラリを導入するかプロジェクト側で自作してもらう事になる。
    * - 5.
      - :ref:`RichComparisonResultDetailsMessageManagement`
      - **有**
      - プロパティファイルから取得する機能は共にSpring Frameworkの標準機能を使用しているが、
        **Richにはデータベースから取得する機能がある。**

        **Global Frameworkでは、データベースから取得する機能は提供していない。**

|

.. _RichComparisonResultOverviewRich:

Rich機能
--------------------------------------------------------------------------------
以下に、Richクライアント向けWebアプリケーションフレームワーク機能の機能性の違いの有無を一覧で示す。

.. tabularcolumns:: |p{0.05\linewidth}|p{0.25\linewidth}|p{0.05\linewidth}|p{0.55\linewidth}|
.. list-table::
    :header-rows: 1
    :widths: 5 25 5 55

    * - 項番
      - 機能名
      - 違い
      - 概要
    * - 6.
      - :ref:`RichComparisonResultDetailsRequestMapping`
      - 無
      - Spring MVC標準機能で代替可能。
    * - 7.
      - :ref:`RichComparisonResultDetailsController`
      - 無
      - Spring MVC標準機能で代替可能。

        **Global Frameworkでは、BLogicControllerのような抽象クラスは提供しないため、
        リクエスト毎にコントローラ(メソッド)を用意するスタイルとなる。**
    * - 8.
      - :ref:`RichComparisonResultDetailsRequestDataParse`
      - **有**
      - リクエストデータの解析(JSON or XML -> JavaBean)自体はSpring MVC標準機能で代替可能。

        **ただし、形式チェック(スキーマチェック)を単項目エラーとして扱う仕組みはない？（TODO）**
        **Global Frameworkでは、DataBinderではなく、HttpMessageConverterの仕組みを利用する。**
    * - 9.
      - :ref:`RichComparisonResultDetailsResponseDataFormat`
      - 無
      - Spring MVC標準機能で代替可能。

        **Global Frameworkでは、Richクライアント向けのアプリケーションの場合は、Viewではなく、HttpMessageConverterの仕組みを利用する。**
    * - 10.
      - :ref:`RichComparisonResultDetailsXmlObjectConvert`
      - 無
      - Java標準機能で代替可能。

        Global Frameworkでは、デフォルトではJava標準のJAXB2が有効になっている。
        Spring-Oxmというライブラリを使うとRichで使用しているCasterを使用する事も可能である。
    * - 11.
      - :ref:`RichComparisonResultDetailsRequestContext`
      - **有**
      - **Global Frameworkには制御情報という概念がない。**
      
        **Global Framewokでは、Spring MVCの標準機能を使用してリクエストデータ解析とコントローラの決定を行うため、
        Richが使用している制御情報を必要としない。そのため、機能自体の提供も行っていない。
        リクエストに紐づく制御情報（コンテキスト情報）を業務アプリ層で必要なのであれば、
        Spring MVC標準のやり方で行うことを推奨している。**
    * - 12.
      - :ref:`RichComparisonResultDetailsFileUpload`
      - 無
      - 共にSpring Framework提供のファイルアップロード機能を使用する前提である。

        **ただし、デフォルトの実装プロバイダが異なる。RichはCommons-FileUpload、
        Global FrameworkはServlet3標準(Commons-FileUploadでも可だが、動作は未検証)。**
    * - 13.
      - :ref:`RichComparisonResultDetailsBusinessLogicExecute`
      - 無
      - Global Frameworkは、ビジネスロジックはServiceクラス(POJO)で実装する事を想定しているが、Richが提供するBLogicのようなインタフェースを実装したクラスでも問題ない。

        **Global Frameworkでは、BLogicControllerのようなクラスは提供しないため、
        ServiceやBLogicをコントローラにDIし、DIされたオブジェクトのメソッドを呼び出すコードを実装するスタイルとなる。**
    * - 14.
      - :ref:`RichComparisonResultDetailsExceptionHandling`
      - 無
      - Spring MVC標準機能で代替可能。

        **Global Frameworkでは、Richクライアント向けアプリケーションの場合は、
        Richが提供しているような定義ベースの例外ハンドリングではなく、
        Javaベースで例外ハンドリングするスタイルを推奨している。**
    * - 15.
      - :ref:`RichComparisonResultDetailsAccessControl`
      - 無
      - Spring Security標準機能で代替可能。
    * - 16.
      - :ref:`RichComparisonResultDetailsSchemaValidate`
      - **有**
      - **Global Frameworkでは、XMLのスキーマをチェックする機能は提供していない。**
    * - 17.
      - :ref:`RichComparisonResultDetailsInputValidate`
      - **有**
      - **Spring MVC標準機能で代替可能だが、実装プロバイダが異なるため、デフォルトで提供しているチェックルールなどに違いがある。**

        RichはCommons-Validator+独自拡張、Global FrameworkはJSR-303 Bean Validation(Hibernate Validator実装)。

\

 .. note:: **制御情報をSpring MVC標準の仕組みを使った連携する方法について**
 
    AP基盤内の部と連携する場合は\ ``HttpServletRequest``\の属性として連携し、
    業務AP(コントローラ)と連携する場合は\ ``HandlerMethodArgumentResolver``\を使用してコントローラの引数として連携する。

 .. note:: **形式チェックについて**
 
    Richの機能説明書には、形式チェックは性能劣化の要因となるため、使用することを推奨していない。
    そのため、Global Frameworkで機能提供がなくても、問題ないのではないか？

 .. todo:: **スキーマチェックと入力チェックの連動性に関する課題**
 
    Global Frameworkにて、XMLのスキーマチェックエラーを入力チェックエラーとして扱えるかは調査が必要・・。

 .. todo:: **スキーマチェックの実現方法について**

    Global Frameworkにて、スキーマチェックはJAXBの機能で実現できると思われるが、
    エラー情報などをSpring MVCと連携できるか？など調査が必要。

 .. todo:: **Global FrameworkにおけるCommons-FileUploadの扱いについて**

    簡単な動作確認が出来ているが、正式な検証は出来ていない。
    

|

.. _RichComparisonResultDetails:

比較結果の詳細
================================================================================

.. _RichComparisonResultDetailsTransactionManagement:

CA-01 トランザクション管理機能
--------------------------------------------------------------------------------
Rich及びGlobal Framework両方とも、Spring Frameworkから提供されているトランザクション管理機能を使用する前提であるため、
実現方式は同じである。

実現方式は同じだが、トランザクション管理対象にするメソッドの指定方法が異なる。


 .. note:: **トランザクション管理対象にするメソッドの指定方法の違いについて**

    RichではBean定義ファイルにAOPの設定を記載するスタイルなのに対して、
    Global Framworkはトランザクション管理が必要な箇所にアノテーション(\ ``@Transactional``\)を指定するスタイルである。

|

.. _RichComparisonResultDetailsTransactionManagementForRich:

TERASOLUNA Framework for Rich
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Richは、

 * トランザクション管理を行うAOPの設定
 * AOPを適用するメソッド

の指定を、Spring FrameworkのBean定義ファイルに定義し、
アプリケーション全体でトランザクション管理方法を指定するスタイルである。

|

- :file:`dataAccessContext-local.xml`

トランザクション制御を行うインタセプタの設定を指定する。
Richではメソッドの命名ルールによって、どのようなトランザクション制御を行うか指定するスタイルとなっている。

.. code-block:: xml

    <tx:advice id="transactionInterceptor" >
        <tx:attributes>
            <tx:method name="execute*" propagation="REQUIRED"
                       rollback-for="java.lang.Exception"/>
        </tx:attributes>
    </tx:advice>

|

- :file:`applicationAOP.xml`

トランザクション制御を行うAOPの設定を指定する。ここではDAOに対してAOPを設定している。
RichではBean名の命名ルールによって、トランザクション制御対象を指定するスタイルとなっている。

.. code-block:: xml

    <aop:config>
        <aop:pointcut id="daoBeans" expression="bean(*DAO)"/>
        <aop:advisor pointcut-ref="daoBeans" advice-ref="transactionInterceptor"/>
    </aop:config>

|

- :file:`commonContext.xml`

トランザクション制御を行うAOPの設定を指定する。ここではServiceとBLogicに対してAOPを設定している。
RichではBean名の命名ルールによって、トランザクション制御対象を指定するスタイルとなっている。

.. code-block:: xml

    <aop:config>
        <aop:pointcut id="serviceBeans" expression="bean(*Service)"/>
        <aop:pointcut id="blogicBeans"  expression="bean(*BLogic)"/>
        <aop:advisor pointcut-ref="serviceBeans" advice-ref="transactionInterceptor"/>
        <aop:advisor pointcut-ref="blogicBeans" advice-ref="transactionInterceptor"/>
    </aop:config>

|

.. _RichComparisonResultDetailsTransactionManagementForGfw:

TERASOLUNA Global Framework
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Global Frameworkは、
\ ``@org.springframework.transaction.annotation.Transactional``\アノテーションを、
AOPを適用する必要があるクラス又はメソッドに個々に指定するスタイルである。

- :file:`xxx-domain.xml`

\ ``<tx:annotation-driven />``\を指定すると、\ ``@Transactional``\アノテーションベースのトランザクション制御を有効になる。

.. code-block:: xml

    <tx:annotation-driven />

|

- Serviceクラス

トランザクション制御が必要な箇所に\ ``@Transactional``\アノテーションを指定する。
クラスに指定すると、クラスに実装されている全てのpublicメソッドに提供されるが、
個別に指定することで設定を上書きすることも可能である。

.. code-block:: java
    :emphasize-lines: 1 

    @Transactional
    @Service
    public class XxxServiceImpl implements XxxService {
        // ...
    }

|

.. _RichComparisonResultDetailsDataAccess:

CB-01 データベースアクセス機能
--------------------------------------------------------------------------------
Rich及びGlobal Framework両方とも、TERASOLUNA DAO + MyBatis2をサポートしており、機能性は完全に同じである。

 .. note:: **Global FrameworkがサポートしているO/R Mapperについて**

    Global Frameworkは、

     * Srping Data JPA + JPA(Hibernate実装)
     * TERASOLUNA DAO + MyBatis2
     * MyBatis3 (1.1.0.RELEASEでサポート予定)

    の3つのO/R Mapperをサポートしている。

    ただし、TERASOLUNA DAO + MyBatis2については、MyBatis3にシフトしていく。

|

.. _RichComparisonResultDetailsJndiAccess:

CC-01 JNDI アクセス機能
--------------------------------------------------------------------------------
Richでは、\ ``jp.terasoluna.fw.web.jndi.DefaultJndiSupport``\というクラスが提供されている。
このクラスはSpring Frameworkから提供されている\ ``org.springframework.jndi.JndiLocatorSuppor``\というクラスを継承しており、
Spring Framework標準クラスに対して使いやすさを加えている。
Global Frameworkでは、Spring Frameworkから提供されている標準機能をそのまま使う想定である。

 .. note:: **Global Frameworkが拡張クラスを提供しない理由について**
 
    機能性的に問題がないという点と、Spring Framework標準機能のままでも十分そのまま使えると判断しているためである。

    Spring Frameworkの標準機能が不便と感じる場合は、プロジェクト側で拡張する事になる。

|

.. _RichComparisonResultDetailsJndiAccessForRich:

TERASOLUNA Framework for Rich
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Richの場合は、以下に示す方法でJNDIアクセスを行う。

- Spring Framework Bean定義ファイル

Richから提供されている\ ``DefaultJndiSupport``\に必要な設定を行いBean登録する。

.. code-block:: xml

    <bean id="jndiSupport" scope="prototype"
        class="jp.terasoluna.fw.web.jndi.DefaultJndiSupport" init-method="initialize">
        <property name="jndiEnvironmentMap">
            <map>
                <entry key="factory" value="weblogic.jndi.WLInitialContextFactory" />
                <entry key="url" value="t3://localhost:7001" />
                <entry key="username" value="weblogic" />
                <entry key="password" value="password" />
            </map>
        </property>
        <property name="jndiPrefix" value="false" />
    </bean>

    <bean id="jndiLogic" scope=”prototype” class="jp.terasoluna.sample.JndiLogic">
        <property name="jndiSupport" ref="jndiSupport" />
    </bean>

|

- Javaクラス

Richから提供されている\ ``JndiSupport``\をDIし、必要なオブジェクトをlookup、rebind、unbindする。

.. code-block:: java

    public class JndiService {
        private JndiSupport jndiSupport = null;
        public void setJndiSupport(jndiSupport) {
            this.jndiSupport = jndiSupport;
        }
        public Object jndiLookup(String name) {
            return jndiSupport.lookup(name);
        }
    }

|

.. _RichComparisonResultDetailsJndiAccessForGfw:

TERASOLUNA Global Framework
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Global Frameworkの場合は、以下に示す方法でJNDIアクセスを行う。

- :file:`xxx-env.xml`

Spring Frameworkから提供されている\ ``JndiTemplate``\に必要な設定を行いBean登録する。

.. code-block:: xml
    :emphasize-lines: 1

    <bean id="jndiTemplate" class="org.springframework.jndi.JndiTemplate">
        <constructor-arg>
            <value>
                java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
                java.naming.provider.url=t3://localhost:7001
                java.naming.security.principal=weblogic
                java.naming.security.credentials=password
            </value>
        </constructor-arg>
    </bean>

|

- Javaクラス

\ ``JndiTemplate``\をDIし、必要なオブジェクトをlookup、bind、rebind、unbindする。

.. code-block:: java
    :emphasize-lines: 3-4,7 

    @Service
    public class JndiServiceImpl implements JndiService {
        @Inject
        JndiTemplate jndiTemplate;
        public <T> T lookup(String name, Class<T> requiredType) {
            try {
                return jndiTemplate.lookup(name, requiredType);
            } catch (NamingException e) {
                throw new SystemException("e.xx.fw.9003", e);
            }
        }
    }

\

 .. note:: **lookupのみ行う場合の標準的な実装方法について**
 
    lookupのみでよい場合は、\ ``<jee:jndi-lookup>``\要素を使用してJNDI経由でオブジェクトをDIコンテナ上に登録し、
    必要なオブジェクトにDIする方法が標準的な実装方法である。

    .. code-block:: xml
        :emphasize-lines: 1

        <jee:jndi-lookup id="dataSource" jndi-name="DataSource/xxxx">
            <jee:environment>
                java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
                java.naming.provider.url=t3://localhost:7001
                java.naming.security.principal=weblogic
                java.naming.security.credentials=password
            </jee:environment>
        </jee:jndi-lookup>

    .. code-block:: java
        :emphasize-lines: 3-4,6
    
        @Service
        public class XxxServiceImpl implements XxxService {
            @Inject
            DataSource dataSource;
            public Xxx getXxx(String id) {
                Connection con = dataSource.getConnection();
                // ...
                return xxx;
            }
        }
 
    
|

.. _RichComparisonResultDetailsUtilities:

CD-01 ユーティリティ機能
--------------------------------------------------------------------------------

ClassUtil
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Global Frameworkが推奨しているOSSライブラリから提供されているクラスで代替可能である。

.. tabularcolumns:: |p{0.05\linewidth}|p{0.25\linewidth}|p{0.30\linewidth}|p{0.05\linewidth}|p{0.25\linewidth}|
.. list-table::
    :header-rows: 1
    :widths: 5 20 30 5 30

    * - 項番
      - メソッド
      - 概要
      - 代替
        手段
      - 説明
    * - 1.
      - create(String)
      - 指定されたクラス名を元にインスタンスを生成する。
      - 有
      - Spring FrameworkやCommons-langのユーティリティメソッドで代替可能。
    * - 2.
      - create(String, Object[])
      - 指定されたクラス名を元にコンストラクタ引数を指定してインスタンスを生成する。
      - 有
      - 同上。

|

DateUtil
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Java標準のクラス、又はGlobal Frameworkが推奨しているOSSライブラリから提供されているクラスで代替可能である。

.. tabularcolumns:: |p{0.05\linewidth}|p{0.25\linewidth}|p{0.30\linewidth}|p{0.05\linewidth}|p{0.25\linewidth}|
.. list-table::
    :header-rows: 1
    :widths: 5 20 30 5 30

    * - 項番
      - メソッド
      - 概要
      - 代替
        手段
      - 説明
    * - 3.
      - getSystemTime()
      - システム時刻を取得する。
      - 有
      - 共通ライブラリから提供している\ ``DateFactory``\で代替可能。
    * - 4.
      - dateToWarekiString(String,Date)
      - \ ``Date``\インスタンスを和暦として、指定したフォーマットに変換する。
      - 有
      - Java標準の\ ``SimpleDateFormat``\の第2引数に\ ``new Locale("ja","JP","JP")``\を指定することで、和暦に変換可能。
    * - 5.
      - getWarekiGengoName(Date)
      - 指定された日付の和暦元号を取得する。
      - 有
      - 同上。
    * - 6.
      - getWarekiGengoRoman(Date)
      - 指定された日付の和暦元号のローマ字表記(短縮 形)を取得する。
      - 有
      - 同上。
    * - 7.
      - getWarekiYear(Date)
      - 指定された日付の和暦年を取得する。
      - 有
      - 同上。

|

FileUtil
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

ディレクトリの強制削除については、Global Frameworkが推奨しているOSSライブラリから提供されているクラスで代替可能である。
セッションディレクトリの管理については、Global Frameworkではサポートしていない。


.. tabularcolumns:: |p{0.05\linewidth}|p{0.25\linewidth}|p{0.30\linewidth}|p{0.05\linewidth}|p{0.25\linewidth}|
.. list-table::
    :header-rows: 1
    :widths: 5 20 30 5 30

    * - 項番
      - メソッド
      - 概要
      - 代替
        手段
      - 説明
    * - 8.
      - getSessionDirectoryName(String)
      - 指定されたセッションIDに対応するディレクトリ名を取得する。
      - **無**
      - **Global Frameworkではセッションディレクトリという概念を設けていない。**
    * - 9.
      - getSessionDirectory(String)
      - 指定されたセッションIDに対応するディレクトリをベースディレクトリから取得する。
      - **無**
      - **同上。**
    * - 10.
      - makeSessionDirectory(String)
      - 指定されたセッションIDに対応するディレクトリを作成する。
      - **無**
      - **同上。**
    * - 11.
      - removeSessionDirectory(String)
      - 指定されたセッションIDに対応するディレクトリを削除する。
      - **無**
      - **同上。**
    * - 12.
      - rmdirs(File)
      - 指定されたディレクトリを削除する。ディレクトリ内にファイル、ディレクトリがある場合でも、再帰的に削除される。
      - 有
      - Commons-ioのユーティリティメソッドで代替可能。

\

 .. note:: **セッションディレクトリについて**
 
    Global Frameworkでは、一時的なファイルを格納するためのディレクトリを、
    セッションに紐付けて管理する必要がないと判断している。
    一時的なファイルの格納場所は特定のディレクトリで管理し、
    一定時間アクセスのない(作成してから一定時間経過した)ファイルを削除するといった手法を提案している。

    一時的なファイルの格納場所をセッションと紐付けて管理する必要がある場合は、
    プロジェクト側で同等の機能を実装する事になる。

|

HashUtil
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Java標準のクラスを直接使用することで代替可能である。

.. tabularcolumns:: |p{0.05\linewidth}|p{0.25\linewidth}|p{0.30\linewidth}|p{0.05\linewidth}|p{0.25\linewidth}|
.. list-table::
    :header-rows: 1
    :widths: 5 20 30 5 30

    * - 項番
      - メソッド
      - 概要
      - 代替
        手段
      - 説明
    * - 13.
      - HashUtil#hash(String, String)
      - 指定されたアルゴリズムで文字列のハッシュ値を取得する。
      - 有
      - Java標準の\ ``MessageDigest``\クラスを直接使用することで代替可能。
        本メソッド自体がJava標準の\ ``MessageDigest``\クラスをラップしているだけである。
    * - 14.
      - HashUtil#hashMD5(String)
      - MD5 アルゴリズムで文字列のハッシュ値を取得する。
      - 有
      - 同上。
    * - 15.
      - HashUtil#hashSHA1(String)
      - SHA1 アルゴリズムで文字列のハッシュ値を取得する。
      - 有
      - 同上。

|

PropertyUtil
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

一部のメソッドについてはSpring Frameworkの標準機能で代替可能だが、Spring Framework標準機能に存在しない機能がある。

.. tabularcolumns:: |p{0.05\linewidth}|p{0.25\linewidth}|p{0.30\linewidth}|p{0.05\linewidth}|p{0.25\linewidth}|
.. list-table::
    :header-rows: 1
    :widths: 5 20 30 5 30

    * - 項番
      - メソッド
      - 概要
      - 代替
        手段
      - 説明
    * - 16.
      - addPropertyFile(String)
      - 指定されたプロパティファイルを追加で読み込む。
      - **無**
      - **プロパティファイルを後から追加する仕組みは存在しない。**
    * - 17.
      - getProperty(String)
      - 指定されたキーのプロパティを取得する。
      - 有
      - Spring Frameworkの標準機能で代替可能。キーが固定の場合は\ ``@Value``\アノテーションを使用し、
        キーが可変の場合は\ ``Properties``\をDIしてプロパティを取得する。
    * - 18.
      - getProperty(String, String)
      - 指定されたキーのプロパティを取得する。プロパティが見つからなかった場合には、指定され たデフォルトが返される。
      - 有
      - 同上。
    * - 18.
      - getPropertyNames()
      - プロパティのすべてのキーのリストを取得する。
      - **無**
      - **Spring Framework標準機能に同等の仕組みがない。小細工（工夫）すれば同じような事は実現可能だが、本質的でない。**
    * - 19.
      - getPropertyNames(String)
      - 指定されたプリフィックスから始まるキーのリストを取得する。
      - **無**
      - **Spring Framework標準機能に同等の仕組みがない。**
    * - 20.
      - getPropertiesValues(String, String)
      - プロパティファイル名、部分キー文字列を指定することにより値セットを取得する。
      - **無**
      - **Spring Framework標準機能に同等の仕組みがない。**
    * - 21.
      - getPropertyNames(Properties, String)
      - プロパティを指定し、部分キープリフィックスに合致するキー一覧を取得する。
      - **無**
      - **Spring Framework標準機能に同等の仕組みがない。**
    * - 22.
      - getPropertiesValues(Properties, Enumeration<String>)
      - キー一覧に対し、プロパティより取得した値を取得する。
      - **無**
      - **Spring Framework標準機能に同等の仕組みがない。**
    * - 23.
      - loadProperties(String)
      - 指定したプロパティファイル名で、プロパティオブジェクトを取得する。
      - 有
      - プロパティファイルを読み込み部分はJava標準のAPIやSpring Frameworkの標準機能で代替可能だが、
        **拡張子の付与など細かい部分は代替できない。**

\

 .. note:: **Spring Framework標準機能で用意されていない機能について**

    Global Frameworkでは、Spring Framework標準のプロパティ管理機能を使用するため、
    プレフィックスでプロパティを管理する機能や、複数キーを指定してプロパティの取得する仕組みは存在しない。
    
    Spring Framework標準機能で用意されていない機能が必要がある場合は、
    プロジェクト側で同等の機能を実装する事になる。
    
|

StringUtil
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. tabularcolumns:: |p{0.05\linewidth}|p{0.25\linewidth}|p{0.30\linewidth}|p{0.05\linewidth}|p{0.25\linewidth}|
.. list-table::
    :header-rows: 1
    :widths: 5 20 30 5 30

    * - 項番
      - メソッド
      - 概要
      - 代替
        手段
      - 説明
    * - 24.
      - isWhitespace(char)
      - 指定された文字がホワイトスペースかどうかを判別する。
      - 有
      - Java標準のAPIで代替可能。
    * - 25.
      - rtrim(String)
      - 文字列の右側のホワイトスペースを削除する。
      - 有
      - Spring Frameworkのユーティリティメソッドで代替可能。
    * - 26.
      - ltrim(String)
      - 文字列の左側のホワイトスペースを削除する。
      - 有
      - Spring Frameworkのユーティリティメソッドで代替可能。
    * - 27.
      - trim(String)
      - 文字列の両側のホワイトスペースを削除する。
      - 有
      - Spring Frameworkのユーティリティメソッドで代替可能。
    * - 28.
      - toShortClassName(String)
      - 完全修飾クラス名から短縮クラス名(パッケージ修飾 なし)を取得する。
      - 有
      - Spring FrameworkやCommons-langのユーティリティメソッドで代替可能。
    * - 29.
      - getExtension(String)
      - 指定された文字列から末尾の拡張子を取得する。 拡張子がない場合は空文字列を返す。
      - 有
      - Commons-IOのユーティリティメソッドで代替可能。
    * - 30.
      - toHexString(byte[], String)
      - バイト配列を16進文字列に変換する。
      - **無**
      - 
    * - 31.
      - capitalizeInitial(String)
      - 指定された文字列の頭文字を大文字にする。
      - 有
      - Spring Frameworkのユーティリティメソッドで代替可能。
    * - 32.
      - parseCSV(String)
      - CSV形式の文字列を文字列の配列に変換する。
      - 有
      - Commons-langから提供されている\ ``StrTokenizer``\で代替可能できそう。**(100%同じ動きになるかは未検証)**
    * - 33.
      - parseCSV(String, String)
      - CSV形式の文字列を文字列の配列に変換する。エスケープ文字を指定可能。
      - 有
      - Commons-langから提供されている\ ``StrTokenizer``\で代替可能できそう。**(100%同じ動きになるかは未検証)**
    * - 34.
      - dump(Map<?, ?>)
      - 引数のマップのダンプを取得する。
      - **無**
      - **Java標準のAPIだとMapの中の配列がダンプできない。**
        Common-langから提供されている\ ``ToStringBuilder``\(\ ``ToStringStyle``\)を拡張することで実現可能。
    * - 35.
      - getArraysStr(Object[])
      - ダンプ対象の値オブジェクトが配列形式の場合、配列要素でなくなるまで繰り返し値を取得する。
      - 有
      - Commons-langのユーティリティメソッドで代替可能。
        本メソッド自体がCommons-langのAPIをラップしているだけである。
    * - 36.
      - hankakuToZenkaku(String)
      - 半角文字列を全角文字列に変換する。
      - **無**
      - **半角・全角変換のユーティリティは提供していない。**
    * - 37.
      - zenkakuToHankaku(String)
      - 全角文字列を半角文字列に変換する。
      - **無**
      - **同上**
    * - 38.
      - filter(String)
      - HTMLメタ文字列に変換する。
      - 有
      - Spring Frameworkのユーティリティメソッドで代替可能。
    * - 39.
      - toLikeCondition(String)
      - 検索条件文字列をLIKE述語のパターン文字列に変換する。
      - 有
      - 共通ライブラリから提供している\ ``QueryEscapeUtils``\で代替可能。
    * - 40.
      - getByteLength(String, String)
      - 指定された文字列のバイト列長を取得する。
      - 有
      - Java標準のAPIを直接使用することで代替可能。
        本メソッド自体がJava標準のAPIをラップしているだけである。

\

 .. warning::
 
    機能説明書に記載がないユーティリティメソッド(isZenHankakuSpace, rtrimZ, ltrimZ, trimZ)が存在する。

|

.. _RichComparisonResultDetailsMessageManagement:

CE-01 メッセージ管理機能
--------------------------------------------------------------------------------

プロパティファイルから取得する機能は共にSpring Frameworkの標準機能を使用する前提であるが、
Global Frameworkにはデータベースでメッセージを管理する機能はない。

 .. note:: **メッセージのデータベース管理について**
 
    Global Frameworkでは、メッセージをデータベースで管理する仕組みは提供しない。

    データベースで管理する必要がある場合は、プロジェクト側で拡張実装する事になる。
 
|

.. _RichComparisonResultDetailsRequestMapping:

RA-01 リクエスト・コントローラマッピング機能
--------------------------------------------------------------------------------
Richが提供しているリクエストとコントローラのマッピング方法は、Spring MVCの標準機能で代替可能である。

 .. note:: **リクエストとコントローラのマッピングの推奨スタイルについて**
 
    Richでは、リクエストとコントローラの紐付けをリクエストヘッダに格納されている値(デフォルトは「requestName」ヘッダの設定値)を参照して行っているが、
    Global Frameworkでは、URLにコントローラのメソッドを紐付けるスタイルを推奨している。
    
    Global FrameworkでもRichと同じ方法でマッピングする事は可能であるが、推奨スタイルではない。

|

TERASOLUNA Framework for Rich
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Richの場合は、以下に示す方法でリクエストとコントローラをマッピングを行う。

- :file:`xxx-servlet.xml`

フレームワーク側の設定は以下の通り（ブランクプロジェクトのデフォルトの状態を抜粋）。
制御情報に設定されているリクエスト名を基に、呼び出すControllerを決定するHandlerMappingを設定する。

.. code-block:: xml
    :emphasize-lines: 1-8

    <!-- リクエストマッピングの設定 -->
    <bean id="defaultHandlerMapping" 
        class="jp.terasoluna.fw.web.rich.springmvc.servlet.handler.BeanNameUrlHandlerMappingEx">
        <property name="ctxSupport" ref="ctxSupport"/>
        <property name="prefix" value="/"/>
        <property name="suffix" value="Controller"/>
        <property name="defaultHandler" ref="unknownCommandController"/>
    </bean>
    <bean id="unknownCommandController"
        class="jp.terasoluna.fw.web.rich.springmvc.controller.UnkownRequestNameController" />

    <!-- コントローラの親の設定  -->
    <bean id="pojoController" abstract="true">
        <property name="ctxSupport" ref="ctxSupport"/>
        <!-- 
        <property name="validator" ref="beanValidator" />
        -->
    </bean>

    <bean id="pojoXmlRequestController" abstract="true" parent="pojoController">
        <property name="dataBinderCreator" ref="xmlDataBinderCreator"/>
    </bean>

    <bean id="pojoXmlRequestCastorViewController" abstract="true"
        parent="pojoXmlRequestController"/>

|

- :file:`xxx-controller.xml`

リクエストとコントローラのマッピング定義を行う。
\ ``/{requestName}Controller``\というBean名でコントローラを定義する。

.. code-block:: xml
    :emphasize-lines: 1

    <bean name="/sumController"
        class="jp.terasoluna.sample.controller.SumController"
        parent="pojoXmlRequestCastorViewController" scope="singleton">
        <property name="calculationService" ref="calculationService"/>
    </bean>

|

- HTTPリクエストとレスポンス

requestNameヘッダに呼び出したいコントローラを識別するための値を指定する。
下記例だと、\ ``/sumController``\というBean名で定義したコントローラを呼び出すためのリクエストとなる。

.. code-block:: text
    :emphasize-lines: 3

    POST /rich-blank/secure/blogic.do HTTP/1.1
    ...
    requestName: sum
    ...
    
    <sumInput>
        <field1>1</field1>
        <field2>2</field2>
    </sumInput>

.. code-block:: text

    HTTP/1.1 200 OK
    Server: Apache-Coyote/1.1
    Content-Type: text/xml;charset=UTF-8
    Content-Language: en
    Content-Length: 132
    Date: Sun, 07 Sep 2014 05:20:42 GMT

    <?xml version="1.0" encoding="UTF-8"?>
    <sumOutput xml:space="preserve"><field1>1</field1><sum>3</sum><field2>2</field2></sumOutput>

|

TERASOLUNA Global Framework
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Global Frameworkの場合は、以下に示す方法でリクエストとコントローラをマッピングを行う。

- :file:`spring-mvc.xml`

フレームワーク側の設定は以下の通り。
\ ``<mvc:annotation-driven />``\を定義すると、\ ``@RequestMapping``\アノテーションの定義を参照してリクエストとコントローラをマッピングするコンポーネントが有効となる。

.. code-block:: xml
    :emphasize-lines: 1

    <mvc:annotation-driven />

|

- Controllerクラス

リクエストとコントローラのマッピング定義を行う。Global Frameworkでは、\ ``@RequestMapping``\アノテーションを使用してマッピングを行う。
下記の例だと、\ ``/calculation/plus``\というURLに対して\ ``CalculationController#plus``\メソッドを割り当てている。

.. code-block:: java
    :emphasize-lines: 1,5

    @RequestMapping(value = "calculation", method = RequestMethod.POST)
    @Controller
    public class CalculationController {
        // ...
        @RequestMapping("plus")
        @ResponseBody
        public SumOutput plus(@RequestBody SumInput command) {
            // ...
        }
    
    }
\

 .. note:: **Global Framewokが推奨するアーキテクチャスタイルについて**
 
    Global Frameworkでは、Richクライアントやシステム連携向けのWebアプリケーションは、
    RESTful Web Service(REST API)として設計・実装することを推奨している。
    
    上記のURLマッピングは、RESTful Web Service(REST API)でないという点を補足しておく。
    RESTful Web Service(REST API)については、`ガイドライン <http://terasolunaorg.github.io/guideline/1.0.1.RELEASE/ja/ArchitectureInDetail/REST.html>`_\を参照されたい。

 .. note:: **Richの仕組み(requestNameによる振り分け)を踏襲したい場合は・・・**
 
    Controllerクラスの実装を以下のようにすれば、Richと同じ動きを実現することも可能である。
 
    .. code-block:: java
        :emphasize-lines: 1, 5

        @RequestMapping(value = "**/*.do", method = RequestMethod.POST)
        @Controller
        public class CalculationController {
            // ...
            @RequestMapping(headers = "requestName=sum")
            @ResponseBody
            public SumOutput plus(@RequestBody SumInput command) {
                // ....
            }
        }

|

- HTTPリクエストとレスポンス

呼び出したいコントローラとマッピングされているURLを指定する。
その際に、Content-Typeに電文の形式を指定する必要がある。
下記例だと、XMLの電文を送るので、\ ``application/xml``\を指定している。

.. code-block:: text
    :emphasize-lines: 1,3

    POST /gfw-blank/calculation/plus HTTP/1.1
    ...
    Content-Type: application/xml
    ...

    <sumInput>
      <field1>1</field1>
      <field2>2</field2>
    </sumInput>

.. code-block:: text

    HTTP/1.1 200 OK
    Server: Apache-Coyote/1.1
    X-Track: 561db36079194c0088ce5bdcf4974aba
    Content-Type: application/xml;charset=UTF-8
    Transfer-Encoding: chunked
    Date: Sun, 07 Sep 2014 06:09:48 GMT

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?><sumOutput><field1>1</field1><field2>2</field2><sum>3</sum></sumOutput>

|

.. _RichComparisonResultDetailsController:

RA-02 コントローラ拡張機能
--------------------------------------------------------------------------------

Richが提供している拡張コントローラで行っている処理は、Spring MVCの標準機能で代替可能である。

 .. note::
 
    Richでは、
    
     * リクエストデータの解析(XML->JavaBean変換)
     * 入力チェック(JavaBeanのバリデーション)
     * ビジネスロジックの実行(呼び出し)
     * Viewの解決(JavaBean->XML変換)
    
    をテンプレートメソッドパターンで実装したクラスを提供している。
    
    Global Frameworkでは、
    
     * リクエストデータの解析(XML->JavaBean変換)
     * 入力チェック(JavaBeanのバリデーション)
     * Viewの解決(JavaBean->XML変換)
    
    を、Spring MVCの標準機能の仕組みを使用して実現するため、コントローラを拡張する必要がない。

|

TERASOLUNA Framework for Rich
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Richの場合は、以下に示す方法でコントローラを作成する。
Richでは、リクエスト電文の解析、入力チェックの実行、Viewの解決を、
\ ``TerasolunaController``\及び\ ``BLogicController``\が行う仕組みとなっている。

|

- Controllerクラス(POJOパターン)

以下は、ビジネスロジックをPOJOで実装する場合のコントローラのサンプル。
Richから提供されている\ ``TerasolunaController``\を継承したクラスとして実装する。

.. code-block:: java
    :emphasize-lines: 1

    public class SumController extends TerasolunaController<SumInput, SumOutput> {
    
        private CalculationService calculationService;
    
        public void setCalculationService(CalculationService calculationService) {
            this.calculationService = calculationService;
        }
    
        @Override
        protected SumOutput executeService(SumInput command) throws Exception {
            long sum = calculationService.plus(command.getField1(), command.getField2());
            SumOutput output = new SumOutput();
            BeanUtils.copyProperties(command, output);
            output.setSum(sum);
            return output;
        }
    
    }

|

- Controllerクラス(BLogicパターン)

POJOではなくBLogicを使用する場合は、Richから提供されている\ ``BLogicController``\を使用すればよいので、
Controllerは個別に作成しない。

|

TERASOLUNA Global Framework
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Global Frameworkの場合は、リクエスト電文の解析、入力チェックの実行、
Viewの解決は、Spring MVC標準機能を使用してフレームワーク内の処理として実行する。

 .. note::
 
    Spring MVC標準機能では、

     * メソッド引数に\ ``@RequestBody``\アノテーションを付与すると、リクエスト電文の解析(電文->JavaBean変換)
     * メソッド引数に\ ``@Validated``\アノテーションを付与すると、入力チェックの実行
     * メソッドに\ ``@ResponseBody``\アノテーションを付与すると、Viewの解決(JavaBean->電文変換)
     
    が行われる。

|

- Controllerクラス(POJOパターン)

以下は、ビジネスロジックをPOJOで実装する場合のコントローラのサンプル。
Global Frameworkでは、Controllerクラスに\ ``@Controller``\を付与することで、ControllerクラスもPOJOとして実装する。

.. code-block:: java
    :emphasize-lines: 2-3,11-13

    @RequestMapping(value = "calculation", method = RequestMethod.POST)
    @Controller
    public class CalculationController {
    
        @Inject
        CalculationService calculationService;
    
        @Inject
        Mapper beanMapper;

        @RequestMapping("plus")
        @ResponseBody
        public SumOutput plus(@RequestBody @Validated SumInput command) {
            long sum = calculationService.plus(command.getField1(), command.getField2());
            SumOutput output = beanMapper.map(command, SumOutput.class);
            output.setSum(sum);
            return output;
        }
    
    }

|

- Controllerクラス(BLogicパターン)

以下は、ビジネスロジックをPOJOではなくBLogicで実装する場合のコントローラのサンプル。
Global Frameworkでは、POJOパターンとBLogicパターンで大きな違いはない。

.. code-block:: java
    :emphasize-lines: 5-6, 11

    @RequestMapping(value = "calculation", method = RequestMethod.POST)
    @Controller
    public class CalculationController {
    
        @Inject
        PlusBLogic plusBLogic;
    
        @RequestMapping("plus")
        @ResponseBody
        public SumResult plus(@RequestBody @Validated SumParam params) {
            return plusBLogic.execute(params);
        }
    
    }

|

.. _RichComparisonResultDetailsRequestDataParse:

RB-01 リクエストデータ解析機能
--------------------------------------------------------------------------------

Richが提供しているリクエストデータ解析機能で行っている処理は、Spring MVCの標準機能で代替可能である。
ただし、実現方法は異なる。

 .. note:: **実現方法の違いについて**
 
    Rich及びGlobal FrameworkともにSpring MVC標準機能をベースとしているが、
    RichがSpring Frameworkの2系の機能ベースなのに対して、
    Global FrameworkはSpring Frameworkの3系の機能ベースで実現している。
    
    具体的には、
    
     * Richは、\ ``DataBinder``\の仕組みを利用し拡張している
     * Global Frameworkは、3系から機能追加された\ ``HttpMessageConverter``\の仕組みを利用している
    
    という点が違いである。

|

TERASOLUNA Framework for Rich
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Richの場合は、Spring MVC標準機能の\ ``DataBinder``\の仕組みを拡張してリクエストデータの解析を行う。

- :file:`xxx-servlet.xml`

フレームワーク側の設定は以下の通り。
Query形式とXML形式のリクエストデータを解析するための\ ``DataBinder``\クラスを提供している。

.. code-block:: xml
    :emphasize-lines: 5-7, 9-13, 27, 35

    <!-- オブジェクト-XMLマッピングクラス -->
    <bean id="oxmapper" 
        class="jp.terasoluna.fw.oxm.mapper.castor.CastorOXMapperImpl" />

    <!-- クエリ形式データバインダ生成クラス -->
    <bean id="queryDataBinderCreator" 
        class="jp.terasoluna.fw.web.rich.springmvc.bind.creator.QueryServletRequestDataBinderCreator"/>

    <!-- XML形式データバインダ生成クラス -->
    <bean id="xmlDataBinderCreator"
        class="jp.terasoluna.fw.web.rich.springmvc.bind.creator.XMLServletRequestDataBinderCreator">
        <property name="oxmapper" ref="oxmapper"/>
    </bean>

    <!-- コントローラの親の設定  -->
    <bean id="pojoController" abstract="true">
        <property name="ctxSupport" ref="ctxSupport"/>
        <!--
        <property name="validator" ref="beanValidator" />
        -->
    </bean>

    <!-- XML形式データ向けのコントローラの親の設定 -->
    <bean id="pojoXmlRequestController" abstract="true" parent="pojoController">
        <property name="dataBinderCreator" ref="xmlDataBinderCreator"/>
    </bean>
    <bean id="pojoXmlRequestCastorViewController"
        abstract="true"
        parent="pojoXmlRequestController"/>

    <!-- Query形式データ向けのコントローラの親の設定 -->
    <bean id="pojoQueryRequestController" abstract="true" parent="pojoController">
        <property name="dataBinderCreator" ref="queryDataBinderCreator"/>
    </bean>
    <bean id="pojoQueryRequestCastorViewController"
        abstract="true"
        parent="pojoQueryRequestController"/>

|

- :file:`xxx-controller.xml`

リクエストデータの形式は、ControllerのBean定義のparent属性に指定する。
「xxxQuery〜」を指定するとQuery形式、「xxxXml〜」を指定するとXML形式の電文としてリクエストデータを解析する。

.. code-block:: xml
    :emphasize-lines: 3

    <bean name="/sumController"
        class="jp.terasoluna.sample.controller.SumController"
        parent="pojoXmlRequestCastorViewController"
        scope="singleton">
        <property name="calculationService" ref="calculationService"/>
    </bean>

|

- Controllerクラス

リクエストデータの解析結果を格納するクラスの指定は、\ ``TerasolunaController``\の1番目のジェネリクス型に指定する。

.. code-block:: java
    :emphasize-lines: 1

    public class SumController extends TerasolunaController<SumInput, SumOutput> {
        // ...
        @Override
        protected SumOutput executeService(SumInput command) throws Exception {
            // ...
        }
    }

|

- JavaBean

リクエストデータの解析結果を格納するクラス(JavaBean)を作成する。

.. code-block:: java
    :emphasize-lines: 1

    public class SumInput {
        private Integer field1;
        private Integer field2;
        // ...
    }

|

- リクエストデータ

各形式のリクエストデータのイメージは以下の通り。

XML形式

.. code-block:: text
    :emphasize-lines: 3

    POST /rich-blank/secure/blogic.do HTTP/1.1
    ...
    requestName: sum
    ...
    
    <sumInput>
        <field1>1</field1>
        <field2>2</field2>
    </sumInput>

Query形式

.. code-block:: text
    :emphasize-lines: 3, 5

    POST /rich-blank/secure/blogic.do HTTP/1.1
    ...
    requestName: sum
    ...
    Content-Type: application/x-www-form-urlencoded
    ...

    field1=1&field2=2

|

TERASOLUNA Global Framework
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Global Frameworkの場合は、Spring MVC標準機能を使用してリクエストデータの解析を行う。

- :file:`spring-mvc.xml`

フレームワーク側の設定は以下の通り。
\ ``<mvc:annotation-driven />``\を定義すると、Query形式、JSON形式(Jackson)、XML形式(JAXB2)の電文が使用可能となる。

.. code-block:: xml
    :emphasize-lines: 1

    <mvc:annotation-driven />

\

 .. note::

    \ ``HttpMessageConverter``\は、リクエストBODYに指定されている電文を解析したり、
    レスポンスBODYに出力する電文を生成するためのコンポーネントである。
    \ ``<mvc:annotation-driven />``\を指定することで、
    JSONとXMLを解析するための\ ``HttpMessageConverter``\が有効となる。

    JSONやXML以外の独自形式の電文を扱う場合は、\ ``HttpMessageConverter``\を実装し、
    \ ``<mvc:annotation-driven />``\の中に定義を追加すればよい。

|

- Controllerクラス

リクエストデータの解析結果を格納するクラスの指定は、メソッドの引数として宣言する。
JSON又はXML形式のリクエストデータを解析する場合は、メソッド引数に\ ``@RequestBody``\アノテーションを指定し、
\ ``HttpMessageConverter``\を使用してリクエストデータの解析を行う。


.. code-block:: java
    :emphasize-lines: 7

    @RequestMapping(value = "calculation", method = RequestMethod.POST)
    @Controller
    public class CalculationController {
        // ...
        @RequestMapping("plus")
        @ResponseBody
        public SumOutput plus(@RequestBody SumInput command) {
            // ...
        }
    }

\

 .. note::
 
    Query形式の電文を扱う場合は、メソッドの引数に\ ``@RequestBody``\を指定は不要である。

|

- JavaBean

リクエストデータの解析結果を格納するクラス(JavaBean)を作成する。
XML形式の場合は、JAXB2のアノテーション(\ ``@XmlRootElement``\か\ ``@XmlType``\)をクラスに指定が必須であるが、
JSON形式の場合は、Jacksonのアノテーションの指定を行う必要はない。Query形式の場合もアノテーションの指定は不要である。

.. code-block:: java
    :emphasize-lines: 1

    @XmlRootElement
    public class SumInput {
        private Integer field1;
        private Integer field2;
        // ...
    }

|

- リクエストデータ

各形式のリクエストデータのイメージは以下の通り。

 .. note::
 
    Global Frameworkでは、リクエストヘッダのContent-Typeを切り替えることで、
    サーバ側で行うリクエストデータの解析方法を指定することができる。
    この仕組みにより、リクエストデータとしてJSONとXML形式の両方をサポートする事が出来るため、
    クライアントフレンドリーなアプリケーションの構築が可能である。


XML形式

.. code-block:: text
    :emphasize-lines: 3

    POST /gfw-blank/calculation/plus HTTP/1.1
    ...
    Content-Type: application/xml
    ...

    <sumInput>
      <field1>1</field1>
      <field2>2</field2>
    </sumInput>

JSON形式

.. code-block:: text
    :emphasize-lines: 3

    POST /gfw-blank/calculation/plus HTTP/1.1
    ...
    Content-Type: application/json
    ...

    {
      "field1" : 1,
      "field2" : 2
    }

Query形式

.. code-block:: text
    :emphasize-lines: 3

    POST /gfw-blank/calculation/plus HTTP/1.1
    ...
    Content-Type: application/application/x-www-form-urlencoded
    ...

    field1=1&field2=2


.. _RichComparisonResultDetailsResponseDataFormat:

RB-02 レスポンスデータ生成機能
--------------------------------------------------------------------------------

Richが提供しているレスポンスデータ生成機能で行っている処理は、Spring MVCの標準機能+共通ライブラリから提供しているクラスで代替可能である。
ただし、実現方法は異なる。

 .. note:: **実現方法の違いについて**
 
    Rich及びGlobal FrameworkともにSpring MVC標準機能をベースとしているが、
    RichがSpring Frameworkの2系の機能ベースなのに対して、
    Global FrameworkはSpring Frameworkの3系の機能ベースで実現している。
    
    具体的には、
    
     * Richは、\ ``View``\(\ ``ViewResolver``\)の仕組みを利用し拡張している
     * Global Frameworkは、3系から機能追加された\ ``HttpMessageConverter``\の仕組みを利用している
    
    という点が違いである。

|

TERASOLUNA Framework for Rich
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Richの場合は、Spring MVC標準機能の\ ``View``\(\ ``ViewResolver``\)の仕組みを拡張してレスポンスデータの生成を行う。

- :file:`xxx-servlet.xml`

フレームワーク側の設定は以下の通り。
Richでは、レスポンスデータの形式として、XML形式とバイナリデータ(ダウンロード形式)をサポートしている。
XML形式については、CasterベースとVelocityベースの2種類を提供している。

.. code-block:: xml
    :emphasize-lines: 1-3, 11-13, 30-32

    <!-- Castor用ビューリゾルバ -->
    <bean id="castorViewResolver" 
        class="jp.terasoluna.fw.web.rich.springmvc.servlet.view.castor.CastorViewResolver">
        <property name="cache" value="true"/>
        <property name="requestContextAttribute" value="rc"/>
        <property name="contentType" value="text/xml;charset=UTF-8"/>
        <property name="order" value="2"/>
        <property name="oxmapper" ref="oxmapper"/>
    </bean>
    
    <!-- Velocity用ビューリゾルバ -->
    <bean id="velocityViewResolver" 
        class="jp.terasoluna.fw.web.rich.springmvc.servlet.view.velocity.VelocityViewResolverEx">
        <property name="cache" value="true"/>
        <property name="requestContextAttribute" value="rc"/>
        <property name="prefix" value=""/>
        <property name="suffix" value=".vm"/>
        <property name="exposeSpringMacroHelpers" value="true"/>
        <property name="encoding" value="UTF-8"/>
        <property name="contentType" value="text/xml;charset=UTF-8"/>
        <property name="toolboxConfigLocation" value="/WEB-INF/velocity/toolbox.xml"/>
    </bean>
    
    <!-- Velocity環境をセットアップするクラス。 -->
    <bean id="velocityConfig" 
        class="org.springframework.web.servlet.view.velocity.VelocityConfigurer">
        <property name="resourceLoaderPath" value="/WEB-INF/velocity/"/>
    </bean>
    
    <!-- ファイルダウンロード用 View解決クラス-->
    <bean id="fileDownloadViewResolver" 
        class="org.springframework.web.servlet.view.ResourceBundleViewResolver">
        <property name="basename" value="views"/>
        <property name="order" value="1"/>
    </bean>

    <bean id="oxmapper" 
        class="jp.terasoluna.fw.oxm.mapper.castor.CastorOXMapperImpl" />
        
    <bean id="pojoXmlRequestCastorViewController" abstract="true"
        parent="pojoXmlRequestController"/>

    <bean id="pojoXmlRequestVelocityViewController" abstract="true"
        parent="pojoXmlRequestController">
        <property name="useRequestNameView" value="true"/>
    </bean>

|

- :file:`xxx-controller.xml` (XML形式)

レスポンスデータの形式は、ControllerのBean定義のparent属性に指定する。
「〜CastorView〜」を指定するとCastor、「〜VelocityView〜」を指定するとVelocityを使用してレスポンスデータが生成される。

.. code-block:: xml
    :emphasize-lines: 4, 11

    <!-- CastorViewを使用する場合のコントローラの定義例 -->
    <bean name="/sumController"
        class="jp.terasoluna.sample.controller.SumController"
        parent="pojoXmlRequestCastorViewController" scope="singleton">
        <property name="calculationService" ref="calculationService"/>
    </bean>

\

 .. note::
 
    * Castorを指定した場合は、Richから提供されている\ ``CastorOXMapperImpl``\を実行しレスポンスデータを生成する。
    * Velocityを指定した場合は、\ ``/WEB-INF/velocity/``\配下に、\ ``{requestName}.vm``\ というVelocityのテンプレートファイルを実行してレスポンスデータを生成する。
     

|

- :file:`xxx-controller.xml` (バイナリデータ)

バイナリデータ（ダウンロードデータ）を生成する場合は、\ ``viewName``\を指定して、
Richから提供している\ ``AbstractFileDownloadView``\の継承クラスを使用してレスポンスデータを生成する。

.. code-block:: xml
    :emphasize-lines: 5

    <!-- 上記以外のView(AbstractFileDownloadView)を使用する場合のコントローラの定義例 -->
    <bean name="/sumController"
        class="jp.terasoluna.sample.controller.SumController"
        parent="pojoXmlRequestController" scope="singleton">
        <property name="viewName" value="textDownloadView" />
        <property name="calculationService" ref="calculationService"/>
    </bean>

\

 .. note::
 
    ビュー名とViewクラスのマッピングは、:file:`views.properties` で指定する。

    .. code-block:: properties
    
        textDownloadView.(class)=jp.terasoluna.sample.view.TextDownloadView

|

- Controllerクラス

レスポンスデータを格納するクラスの指定は、\ ``TerasolunaController``\の2番目のジェネリクス型に指定する。

.. code-block:: java
    :emphasize-lines: 1

    public class SumController extends TerasolunaController<SumInput, SumOutput> {
        // ...
        @Override
        protected SumOutput executeService(SumInput command) throws Exception {
            // ...
        }
    }

|

- JavaBean

レスポンスデータを格納するクラス(JavaBean)を作成する。

.. code-block:: java

    public class SumOutput {
        private Integer field1;
        private Integer field2;
        private Long sum;
        // ...
    }

|

TERASOLUNA Global Framework
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Global Frameworkの場合は、Spring MVC標準機能を使用してレスポンスデータの生成を行う。

- :file:`spring-mvc.xml`

フレームワーク側の設定は以下の通り。
Global Frameworkでは、レスポンスデータの形式として、JSON形式、XML形式、バイナリデータ(ダウンロード形式)をサポートしている。

.. code-block:: xml
    :emphasize-lines: 1-2, 4-5

    <!-- JSONとXML形式を有効にするための設定 -->
    <mvc:annotation-driven />
    
    <!-- ファイルダウンロード用 View解決クラスの設定 -->
    <bean class="org.springframework.web.servlet.view.BeanNameViewResolver">
         <property name="order" value="0"/>
    </bean>

\

 .. note::
 
    Richでは、XML形式のレスポンスデータを生成する方法を2種類提供しているが、Global FrameworkではJAXB2の1種類である。
    
    Global Frameworkの推奨ライブラリには入っていないが、
    Spring Frameworkから提供されている\ ``VelocityViewResolver``\を使用する事で、Velocityを使用する事も可能である。

|

- Controllerクラス(JSON & XML形式)

レスポンスするデータを保持するJavaBeanをメソッドの返り値として宣言する。
JSON又はXML形式のレスポンスデータを作成する場合は、メソッドに\ ``@ResponseBody``\アノテーションを指定し、
\ ``HttpMessageConverter``\を使用してレスポンスデータの作成を行う。

.. code-block:: java
    :emphasize-lines: 6-7

    @RequestMapping(value = "calculation", method = RequestMethod.POST)
    @Controller
    public class CalculationController {
        // ...
        @RequestMapping("plus")
        @ResponseBody
        public SumOutput plus(@RequestBody SumInput command) {
            // ...
        }
    }

|

- Controllerクラス(バイナリデータ)

バイナリデータ（ダウンロードデータ）を生成する場合は、メソッドの返り値としてviewNameを返却し、
共通ライブラリから\ ``AbstractFileDownloadView``\の継承クラスを使用してレスポンスデータを生成する。
Viewと連携するデータは、\ ``Model``\オブジェクトに格納する。

.. code-block:: java
    :emphasize-lines: 6, 9, 10

    @RequestMapping(value = "calculation", method = RequestMethod.POST)
    @Controller
    public class CalculationController {

        @RequestMapping("plus")
        public String plus(@RequestBody SumInput command, Model model) {
            // ...
            String text = ...;
            model.addAttribute("text", text);
            return "textDonwloadView";
        }
    }

\

 .. note::

    Bean名をView名と一致させておくことで、\ ``BeanNameViewResolver``\によって使用するViewが解決される。

    .. code-block:: java
        :emphasize-lines: 1

        @Component
        public class TextDonwloadView extends AbstractFileDownloadView {
            // ...
        }

|

- JavaBean

レスポンスデータを格納するクラス(JavaBean)を作成する。
XML形式の場合は、JAXB2のアノテーション(\ ``@XmlRootElement``\か\ ``@XmlType``\)をクラスに指定が必須であるが、
JSON形式の場合は、Jacksonのアノテーションの指定を行う必要はない。
 
.. code-block:: java
    :emphasize-lines: 1

    @XmlRootElement
    public class SumOutput {
        private Integer field1;
        private Integer field2;
        private Long sum;
        // ...
    }

|

.. _RichComparisonResultDetailsXmlObjectConvert:

RB-03 XML-Object 変換機能
--------------------------------------------------------------------------------

Richが提供しているXML-Object 変換機能で行っている処理は、Java標準の機能で代替可能である。
ただし、実現方法は異なる。

 .. note:: **実現方法の違いについて**
 
    RichではCastorというO/X Mapperを使用しているのに対して、
    Global FrameworkではJAXB2(Java標準のO/R Mapperを使用している。
    
    Global Frameworkの推奨ライブラリには入っていないが、
    \ ``MarshallingHttpMessageConverter``\とSpring-Oxmから提供されている\ ``CastorMarshaller``\を使用する事で、
    Castorを使用する事も可能である。

|

.. _RichComparisonResultDetailsRequestContext:

RB-04 制御情報管理機能
--------------------------------------------------------------------------------

|

TERASOLUNA Framework for Rich
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

|

TERASOLUNA Global Framework
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

|

.. _RichComparisonResultDetailsFileUpload:

RB-05 ファイルアップロード機能
--------------------------------------------------------------------------------

Rich及びGlobal Framework両方とも、Spring Frameworkから提供されているファイルアップロード機能を使用する前提である。
ただし、実現方式は同じだが、実装プロバイダが異なる。

実装プロバイダが異なるため、設定値など微妙に異なる。

 .. note:: **実装プロバイダに違いについて**

    RichではCommons-FileUploadというライブラリの実装を利用しているのに対して、
    Global Frameworkではアプリケーションサーバの実装(Servlet3から追加されたファイルアップロード機能)を利用する事を想定している。
    
    Global Frameworkの推奨ライブラリには入っていないが、Commons-FileUploadを使用する事は可能である。
    Servlet3のファイルアップロード機能は一部のアプリケーションサーバ(WebLogicとResin)で文字化けが発生するため、
    Commons-FileUploadを推奨(又は必須)ライブラリにすべきか検討中である。

|

TERASOLUNA Framework for Rich
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Richの場合、実装プロバイダとしてCommons-FileUploadを使用してファイルアップロードを行う。

- :file:`xxx-servlet.xml`

Commons-FileUploadの機能を使用してファイルアップロードを行うためのクラス(\ ``CommonsMultipartResolver``\)をBean定義する。
必要に応じて、設定値に適正値を指定する。

.. code-block:: xml
    :emphasize-lines: 1-7

    <bean id="multipartResolver"
        class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
        <property name="maxUploadSize" value="適正値"/>
        <property name="maxInMemorySize" value="適正値" />
        <property name="defaultEncoding" value="適正値" />
        <property name="uploadTempDir" value="適正値" />
    </bean>

|

TERASOLUNA Global Framework
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Global Frameworkの場合、実装プロバイダとしてアプリケーションサーバの実装(Servlet3から追加されたファイルアップロード機能)を使用してファイルアップロードを行う。

- :file:`web.xml`

Servlet3のアップロード機能を有効化(必要に応じて、設定値に適正値を指定)し、
Spring Frameworkと連携するための設定を追加する。
\ ``MultipartFilter``\を使用すると、ファイルアップロード系の例外がServletFilter内で発生し、
サーブレットコンテナに例外が通知される。
ファイルアップロード系の例外を適切にハンドリングするために、
error-pageに\ ``MultipartException``\をハンドリングするための定義も追加する。

.. code-block:: xml
    :emphasize-lines: 1-8, 18-23, 26-29

    <filter>
        <filter-name>MultipartFilter</filter-name>
        <filter-class>org.springframework.web.multipart.support.MultipartFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>MultipartFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

    <servlet>
        <servlet-name>appServlet</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath*:META-INF/spring/spring-mvc.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
        <multipart-config>
            <location>適正値</location>
            <max-file-size>適正値</max-file-size>
            <max-request-size>適正値</max-request-size>
            <file-size-threshold>適正値</file-size-threshold>
        </multipart-config>
    </servlet>

    <error-page>
        <exception-type>org.springframework.web.multipart.MultipartException</exception-type>
        <location>/WEB-INF/views/common/error/fileUploadError.jsp</location>
    </error-page>

\

 .. note::
 
    \ ``MultipartFilter``\は、マルチパートリクエストの際に、
    ServletFilterの処理でリクエストパラメータから値を取得できるようにするためのServletFilterである。
    
    \ ``MultipartFilter``\を使用する場合は、
    デフォルトでServlet3の機能を使用してファイルアップロードを行うためのクラス(\ ``StandardServletMultipartResolver``\)が使用される。
    \ ``MultipartFilter``\を使用しない場合は、\ :file:`spring-mvc.xml`\に\ ``StandardServletMultipartResolver``\のBean定義が必要になる。
 
    .. code-block:: xml
    
        <bean id="multipartResolver"
            class="org.springframework.web.multipart.support.StandardServletMultipartResolver" />

|

.. _RichComparisonResultDetailsBusinessLogicExecute:

RC-01 ビジネスロジック実行機能
--------------------------------------------------------------------------------

Global Frameworkは、ビジネスロジックはServiceクラス(POJO)で実装する事を想定しているが、
Richが提供するBLogicのようなインタフェースを実装したクラスでも問題ない。

 .. note::
 
    Global Frameworkでは、\ ``TerasolunaController``\や\ ``BLogicController``\のようなコントローラクラスは提供しないため、
    ServiceやBLogicをコントローラにDIし、DIされたオブジェクトのメソッドを呼び出すコードを実装するスタイルとなる。

|

TERASOLUNA Framework for Rich
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Richでは、Serviceクラス(POJO)とBLogicの2パターンを提供している。

- Serviceクラス(POJO)

POJOとして、メソッドを実装する。

.. code-block:: java

    public class CalculationServiceImpl implements CalculationService {
        public long plus(int field1, int field2) {
            return field1 + field2;
        }
    }

|

- BLogic

Richから提供されているBLogicインタフェースを実装する。

.. code-block:: java

    public class PlusBLogic implements BLogic<PlusParam, PlusResult> {
        @Override
        public PlusResult execute(PlusParam params) {
            long sum = params.getField1() + params.getField2();
            PlusResult result = new PlusResult();
            BeanUtils.copyProperties(params, result);
            result.setSum(sum);
            return result;
        }
    }


|

TERASOLUNA Global Framework
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Global Frameworkでは、アーキテクチャ上はServiceクラス(POJO)を推奨しているが、
BLogicインタフェースを実装したクラスを使用しても問題はない。

.. code-block:: java

    public class CalculationServiceImpl implements CalculationService {
        public long plus(int field1, int field2) {
            return field1 + field2;
        }
    }

|

.. _RichComparisonResultDetailsExceptionHandling:

RD-01 例外ハンドリング機能
--------------------------------------------------------------------------------

|

TERASOLUNA Framework for Rich
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

|

TERASOLUNA Global Framework
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

|

.. _RichComparisonResultDetailsAccessControl:

RE-01 URI アクセス制御機能
--------------------------------------------------------------------------------

|

TERASOLUNA Framework for Rich
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

|

TERASOLUNA Global Framework
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

|

.. _RichComparisonResultDetailsSchemaValidate:

RF-01 形式チェック機能
--------------------------------------------------------------------------------

|

TERASOLUNA Framework for Rich
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

|

TERASOLUNA Global Framework
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

|

.. _RichComparisonResultDetailsInputValidate:

RF-02 入力チェック機能
--------------------------------------------------------------------------------

|

TERASOLUNA Framework for Rich
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

|

TERASOLUNA Global Framework
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

|


.. raw:: latex

    \newpage

