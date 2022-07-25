########################
开放容器计划
########################

*************************
镜像规范
*************************

此规范定义了OCI镜像，包含一个清单，一个镜像索引（可选），一组文件系统层和一个配置。

规范的目标是建立一组可交互的工具，用于构建、传输和准备运行镜像。

=================
概述
=================

镜像清单包含关于镜像内容和依赖的元数据，镜像包含可以基于内容寻址的多个文件系统层变更集归档的标识符，归档解包组成最终运行文件系统。

镜像配置含有应用参数、环境等信息。

镜像索引是一种高维清单，用于指向一系列清单和描述符。这些清单可能有不同的实现，可能是多种的平台属性。

OCI镜像可以通过名字发现、下载和通过哈希验证，通过签名信任，解包成OCI运行时包。

----------------------
理解规范
----------------------

* 镜像清单： 描述组成镜像的组件的文档
* 镜像索引： 镜像清单的注解索引
* 镜像布局： 一种描绘镜像内容的文件系统布局
* 文件系统层： 描述容器文件系统的变更集
* 镜像配置： 决定层级顺序和将镜像转成运行时包的配置的文档
* 转换： 描述如何转换的文档
* 描述符： 类型、元数据和内容地址的引用

------------------------
媒体类型
------------------------


*  application/vnd.oci.descriptor.v1+json: Content Descriptor
*  application/vnd.oci.layout.header.v1+json: OCI Layout
*  application/vnd.oci.image.index.v1+json: Image Index
*  application/vnd.oci.image.manifest.v1+json: Image manifest
*  application/vnd.oci.image.config.v1+json: Image config
*  application/vnd.oci.image.layer.v1.tar: "Layer", as a tar archive
*  application/vnd.oci.image.layer.v1.tar+gzip: "Layer", as a tar archive compressed with gzip
*  application/vnd.oci.image.layer.v1.tar+zstd: "Layer", as a tar archive compressed with zstd
*  application/vnd.oci.image.layer.nondistributable.v1.tar: "Layer", as a tar archive with distribution restrictions
*  application/vnd.oci.image.layer.nondistributable.v1.tar+gzip: "Layer", as a tar archive with distribution restrictions compressed with gzip
*  application/vnd.oci.image.layer.nondistributable.v1.tar+zstd: "Layer", as a tar archive with distribution restrictions compressed with zstd

==================
内容描述符
==================

* OCI镜像由不同的几种组件组成，通过Merkle有向无环图编排
* 组件之间的引用通过内容描述符
* 内容描述符描述目标内容的特性
* 一个内容描述符含有类型、标识符和原生内容的字节大小
* Descriptors **SHOULD** be embedded in other formats to securely reference external content.
* Other formats **SHOULD** use descriptors to securely reference external content.

------------------
属性
------------------

描述由一组属性组成，每个属性是一个key-value字段。

.. list-table::     
    :header-rows: 1

    * - 属性名
      - 属性值类型
      - 必要性
      - 说明
    * - mediaType
      - string
      - REQUIRED
      - 
    * - digest
      - string
      - REQUIRED
      -
    * - size
      - int64
      - REQUIRED
      - 
    * - urls
      - array of strings
      - OPTIONAL
      -
    * - annotations
      - string-string map 
      - OPTIONAL
      -
    * - data
      - string
      - OPTIONAL
      -

^^^^^^^^^^^^^^
digest
^^^^^^^^^^^^^^

.. code-block:: guess

    digest                ::= algorithm ":" encoded
    algorithm             ::= algorithm-component (algorithm-separator algorithm-component)*
    algorithm-component   ::= [a-z0-9]+
    algorithm-separator   ::= [+._-]
    encoded               ::= [a-zA-Z0-9=_-]+

==================
镜像布局
==================

* 镜像布局是一种用于内容寻址blobs和定位寻址refs的目录结构.
* 这种布局可用于多种传输机制：归档、共享文件系统环境或者网络文件提取.

给定一个镜像布局、一个ref、一个工具可以创建一个OCI运行时包：

* 通过ref找到清单
* 通过指定顺序应用文件系统层
* 转换镜像配置到OCI运行时的config.json

----------------
组成
----------------

* blobs目录

    * 包含可内容寻址的blobs
    * blob没有模式和应该是不透明的
    * 目录必须存在，可能为空
    * 详细参考 :ref:`blob-details`

* oci-layout文件

    * 必须存在
    * 必须是一个JSON对象
    * 必须包含一个imageLayoutVersion字段
    * 可以包含附加字段
    * 参考 :ref:`oci-layout-file-details`

* index.json文件

    * 必须存在
    * 必须是一个镜像索引JSON对象
    * 参考 :ref:`index-json-file`


.. _blob-details:

^^^^^^^^^^^^^^^^^^^^^^^
blob 
^^^^^^^^^^^^^^^^^^^^^^^

* 子目录由哈希算法组成,叶子包含真正的内容.
* The content of blobs//<encoded> MUST match the digest :<encoded> (referenced per descriptor). For example, the content of blobs/sha256/da39a3ee5e6b4b0d3255bfef95601890afd80709 MUST match the digest sha256:da39a3ee5e6b4b0d3255bfef95601890afd80709.
* 和<encoded>条目名称的字符集必须匹配描述的文法。
* 目录可含有不被refs引用的blobs
* The blobs directory MAY be missing referenced blobs, in which case the missing blobs SHOULD be fulfilled by an external blob store.

例子：
    
.. code-block::

    $ cat ./blobs/sha256/9b97579de92b1c195b85bb42a11011378ee549b02d7fe9c17bf2a6b35d5cb079 | jq
    {
    "schemaVersion": 2,
    "manifests": [
        {
        "mediaType": "application/vnd.oci.image.manifest.v1+json",
        "size": 7143,
        "digest": "sha256:afff3924849e458c5ef237db5f89539274d5e609db5db935ed3959c90f1f2d51",
        "platform": {
            "architecture": "ppc64le",
            "os": "linux"
        }
        },
    ...

.. _oci-layout-file-details:

^^^^^^^^^^^^^^^^^^^^^
oci-layout文件
^^^^^^^^^^^^^^^^^^^^^

这个JSON对象充当一个镜像布局基础的标志和镜像布局的版本。

例子：

.. code-block::

    {
        "imageLayoutVersion": "1.0.0"
    }

.. _index-json-file:

^^^^^^^^^^^^^^^^^^^^^^^^^
index.json文件
^^^^^^^^^^^^^^^^^^^^^^^^^

这个文件是镜像布局引用和描述符的入口。镜像索引是一个多描述符的入口点。

例子：

.. code-block::

    {
        "schemaVersion": 2,
        "manifests": [
            {
            "mediaType": "application/vnd.oci.image.index.v1+json",
            "size": 7143,
            "digest": "sha256:0228f90e926ba6b96e4f39cf294b2586d38fbb5a1e385c05cd1ee40ea54fe7fd",
            "annotations": {
                "org.opencontainers.image.ref.name": "stable-release"
            }
            },
            {
            "mediaType": "application/vnd.oci.image.manifest.v1+json",
            "size": 7143,
            "digest": "sha256:e692418e4cbaf90ca69d05a66403747baa33ee08806650b51fab815ad7fc331f",
            "platform": {
                "architecture": "ppc64le",
                "os": "linux"
            },
            "annotations": {
                "org.opencontainers.image.ref.name": "v1.0"
            }
            },
            {
            "mediaType": "application/xml",
            "size": 7143,
            "digest": "sha256:b3d63d132d21c3ff4c35a061adf23cf43da8ae054247e32faa95494d904a007e",
            "annotations": {
                "org.freedesktop.specifications.metainfo.version": "1.0",
                "org.freedesktop.specifications.metainfo.type": "AppStream"
            }
            }
        ],
        "annotations": {
            "com.example.index.revision": "r124356"
        }
    }

==================
镜像清单
==================

镜像清单的三个目标：

* 可内容寻址的镜像, 镜像模型的镜像配置可以为镜像和它的组件产生唯一ID。
* 允许多架构镜像
* 转换成OCI运行时

一个镜像清单为特定架构和操作系统提供一个配置和一组层。

-----------------
属性
-----------------

.. list-table::     
    :header-rows: 1

    * - 属性名
      - 属性值类型
      - 必要性
      - 说明
    * - schemaVersion
      - int
      - REQUIRED
      - 
    * - mediaType
      - string
      - REQUIRED
      -
    * - config
      - descriptor
      - REQUIRED
      - 
    * - layers
      - array of objects
      - OPTIONAL
      -
    * - annotations
      - string-string map 
      - OPTIONAL
      -

例子：

.. code-block::

    {
        "schemaVersion": 2,
        "mediaType": "application/vnd.oci.image.manifest.v1+json",
        "config": {
            "mediaType": "application/vnd.oci.image.config.v1+json",
            "size": 7023,
            "digest": "sha256:b5b2b2c507a0944348e0303114d8d93aaaa081732b86451d9bce1f432a537bc7"
        },
        "layers": [
            {
            "mediaType": "application/vnd.oci.image.layer.v1.tar+gzip",
            "size": 32654,
            "digest": "sha256:9834876dcfb05cb167a5c24953eba58c4ac89b1adf57f28f2f9d09af107ee8f0"
            },
            {
            "mediaType": "application/vnd.oci.image.layer.v1.tar+gzip",
            "size": 16724,
            "digest": "sha256:3c3a4604a545cdc127456d94e421cd355bca5b528f4a9c1905b15da2eb4a4c6b"
            },
            {
            "mediaType": "application/vnd.oci.image.layer.v1.tar+gzip",
            "size": 73109,
            "digest": "sha256:ec4b8955958665577945c89419d1af06b5f7636b4ac3da7f12184802ad867736"
            }
        ],
        "annotations": {
            "com.example.key1": "value1",
            "com.example.key2": "value2"
        }
    }

==================
镜像索引
==================

==================
文件系统层
==================

==================
镜像配置
==================

==================
注解
==================

==================
转换
==================

==================
考虑
==================


**************************
运行时规范
**************************


**************************
分发规范
**************************