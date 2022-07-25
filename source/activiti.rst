####################################
Activiti（5.23）
####################################

************************************
表
************************************

.. raw:: HTML

    <table style="width: 100%" border="1" cellspacing="0" cellpadding="0">
        <thead>
            <tr>
                <td style="background: rgba(192, 192, 192, 1)" valign="top">表分类</td>
                <td style="background: rgba(192, 192, 192, 1)">表名</td>
                <td style="background: rgba(192, 192, 192, 1)">解释</td>
            </tr>
        </thead>
        <tbody>           
            <tr>
                <td rowspan="2">通用数据</td>
                <td valign="top">ACT_GE_BYTEARRAY</td>
                <td valign="top">通用的流程定义和流程资源</td>
            </tr>
            <tr>
                <td valign="top">ACT_GE_PROPERTY</td>
                <td valign="top">系统相关属性</td>
            </tr>
            <tr>
                <td rowspan="8">流程历史记录&nbsp;</td>
                <td valign="top">ACT_HI_ACTINST</td>
                <td valign="top">历史的节点实例</td>
            </tr>
            <tr>
                <td valign="top">ACT_HI_ATTACHMENT</td>
                <td valign="top">历史的流程附件</td>
            </tr>
            <tr>
                <td valign="top">ACT_HI_COMMENT</td>
                <td valign="top">历史的说明性信息</td>
            </tr>
            <tr>
                <td valign="top">ACT_HI_DETAIL</td>
                <td valign="top">历史的流程运行中的细节信息</td>
            </tr>
            <tr>
                <td valign="top">ACT_HI_IDENTITYLINK</td>
                <td valign="top">历史的流程运行过程中用户关系</td>
            </tr>
            <tr>
                <td valign="top">ACT_HI_PROCINST</td>
                <td valign="top">历史的流程实例</td>
            </tr>
            <tr>
                <td valign="top">ACT_HI_TASKINST</td>
                <td valign="top">历史的任务实例</td>
            </tr>
            <tr>
                <td valign="top">ACT_HI_VARINST</td>
                <td valign="top">历史的流程运行中的变量信息</td>
            </tr>
            <tr>
                <td rowspan="4">用户用户组表</td>
                <td valign="top">ACT_ID_GROUP</td>
                <td valign="top">身份信息-组信息</td>
            </tr>
            <tr>
                <td valign="top">ACT_ID_INFO</td>
                <td valign="top">身份信息-组信息</td>
            </tr>
            <tr>
                <td valign="top">ACT_ID_MEMBERSHIP</td>
                <td valign="top">身份信息-用户和组关系的中间表</td>
            </tr>
            <tr>
                <td valign="top">ACT_ID_USER</td>
                <td valign="top">身份信息-用户信息</td>
            </tr>
            <tr>
                <td rowspan="3">流程定义表</td>
                <td valign="top">ACT_RE_DEPLOYMENT</td>
                <td valign="top">部署单元信息</td>
            </tr>
            <tr>
                <td valign="top">ACT_RE_MODEL</td>
                <td valign="top">模型信息</td>
            </tr>
            <tr>
                <td valign="top">ACT_RE_PROCDEF</td>
                <td valign="top">已部署的流程定义</td>
            </tr>
            <tr>
                <td rowspan="6">运行实例表</td>
                <td valign="top">ACT_RU_EVENT_SUBSCR</td>
                <td valign="top">运行时事件</td>
            </tr>
            <tr>
                <td valign="top">ACT_RU_EXECUTION</td>
                <td valign="top">运行时流程执行实例</td>
            </tr>
            <tr>
                <td valign="top">ACT_RU_IDENTITYLINK</td>
                <td valign="top">运行时用户关系信息</td>
            </tr>
            <tr>
                <td valign="top">ACT_RU_JOB</td>
                <td valign="top">运行时作业</td>
            </tr>
            <tr>
                <td valign="top">ACT_RU_TASK</td>
                <td valign="top">运行时任务</td>
            </tr>
            <tr>
                <td valign="top">ACT_RU_VARIABLE</td>
                <td valign="top">运行时变量表</td>
            </tr>
        </tbody>
    </table>
    

=================================
引擎表
=================================

.. list-table:: ACT_GE_PROPERTY

    * - 字段名 
      - 字段描述      
    * - NAME_
      - 属性名
    * - VALUE_
      - 属性值
    * - REV_
      - revision, 修订版本

.. code-block:: 

    insert into ACT_GE_PROPERTY values ('schema.version', '5.23.0.0', 1);

    insert into ACT_GE_PROPERTY values ('schema.history', 'create(5.23.0.0)', 1);

    insert into ACT_GE_PROPERTY values ('next.dbid', '1', 1);


.. list-table:: ACT_GE_BYTEARRAY

    * - 字段名 
      - 字段描述      
    * - ID_
      -    
    * - REV_
      - revision, 修订版本
    * - NAME_
      - 部署的文件名称      
    * - DEPLOYMENT_ID_
      - 部署ID 
    * - BYTES_
      - 字节流数据   
    * - GENERATED_
      - 是否是引擎生成的，0：为用户生成， 1： 为引擎生成

.. list-table:: ACT_RE_DEPLOYMENT

    * - 字段名 
      - 字段描述      
    * - ID_
      -        
    * - NAME_
      - 部署包的名称      
    * - CATEGORY_
      - 分类
    * - TENANT_ID_
      - 租户   
    * - DEPLOY_TIME_
      - 部署时间

.. list-table:: ACT_RE_MODEL

    * - 字段名 
      - 字段描述      
    * - ID_
      -        
    * - REV_
      - revision, 修订版本
    * - NAME_
      - 模型名称  
    * - KEY_
      - 模型的关键字
    * - CATEGORY_
      - 分类
    * - CREATE_TIME_
      - 创建时间
    * - LAST_UPDATE_TIME_
      - 最后修改时间
    * - VERSION_
      - 版本
    * - META_INFO_
      - 元信息,以json格式保存流程定义的信息
    * - DEPLOYMENT_ID_
      - 部署ID 
    * - EDITOR_SOURCE_VALUE_ID_
      - 编辑源值ID
    * - EDITOR_SOURCE_EXTRA_VALUE_ID_
      - 编辑源附加值ID 
    * - TENANT_ID_
      - 租户       

.. list-table:: ACT_RE_PROCDEF

    * - 字段名 
      - 字段描述      
    * - ID_
      -        
    * - REV_
      - revision, 修订版本
    * - CATEGORY_
      - 分类，流程命名空间（targetNamespace）
    * - NAME_
      - 流程名称（process元素的name属性值）  
    * - KEY_
      - 流程编号（process元素的id属性值） 
    * - VERSION_
      - 版本
    * - DEPLOYMENT_ID_
      - 部署ID 
    * - RESOURCE_NAME_
      - 资源名称
    * - DGRM_RESOURCE_NAME_
      - 图片资源名称    
    * - DESCRIPTION_
      - 描述信息    
    * - HAS_START_FORM_KEY_
      - 是否表单key启动,start节点是否存在formKey 0否  1是
    * - HAS_GRAPHICAL_NOTATION_
      -  
    * - SUSPENSION_STATE_
      - 挂起状态
    * - TENANT_ID_
      - 租户      

.. list-table:: ACT_PROCDEF_INFO

    * - 字段名 
      - 字段描述      
    * - ID_
      -        
    * - PROC_DEF_ID_
      - ACT_RE_PROCDEF.ID_      
    * - REV_
      - 
    * - INFO_JSON_ID_
      -  外键ACT_GE_BYTEARRAY.ID_
   
.. list-table:: ACT_RU_EXECUTION

    * - 字段名 
      - 字段描述      
    * - ID_
      -    
    * - REV_
      -     
    * - PROC_INST_ID_
      -           
    * - BUSINESS_KEY_
      -  
    * - PARENT_ID_
      -    
    * - PROC_DEF_ID_
      -     
    * - SUPER_EXEC_
      -           
    * - ACT_ID_
      - 节点实例ID即ACT_HI_ACTINST中ID 
    * - IS_ACTIVE_
      - 是否存活          
    * - IS_CONCURRENT_
      - 是否为并行(true/false） 
    * - IS_SCOPE_
      -    
    * - IS_EVENT_SCOPE_
      -     
    * - SUSPENSION_STATE_
      - 挂起状态   1激活 2挂起          
    * - CACHED_ENT_STATE_
      - 缓存结束状态 
    * - TENANT_ID_
      -     
    * - NAME_
      -           
    * - LOCK_TIME_
      -  

.. list-table:: ACT_RU_JOB

    * - 字段名 
      - 字段描述      
    * - ID_
      -    
    * - REV_
      -     
    * - TYPE_
      -           
    * - LOCK_EXP_TIME_
      - 锁定释放时间 
    * - LOCK_OWNER_
      - 挂起者   
    * - EXCLUSIVE_
      -     
    * - EXECUTION_ID_
      -           
    * - PROCESS_INSTANCE_ID_
      -  
    * - PROC_DEF_ID_
      -           
    * - RETRIES_
      -  
    * - EXCEPTION_STACK_ID_
      - 异常信息ID   
    * - EXCEPTION_MSG_
      - 异常信息    
    * - DUEDATE_
      - 耗时          
    * - REPEAT_
      - 重复 
    * - HANDLER_TYPE_
      - 处理类型    
    * - HANDLER_CFG_
      - 标识          
    * - TENANT_ID_
      -  

.. list-table:: ACT_RU_TASK

    * - 字段名 
      - 字段描述      
    * - ID_
      -    
    * - REV_
      -     
    * - EXECUTION_ID_
      -           
    * - PROC_INST_ID_
      -  
    * - PROC_DEF_ID_
      -    
    * - NAME_
      - 节点定义名称    
    * - PARENT_TASK_ID_
      - 父节点实例ID          
    * - DESCRIPTION_
      - 节点定义描述
    * - TASK_DEF_KEY_
      - 任务定义的ID          
    * - OWNER_
      - 拥有者（一般情况下为空，只有在委托时才有值） 
    * - ASSIGNEE_
      - 签收人或委托人  
    * - DELEGATION_
      - 委托类型，DelegationState分为两种：PENDING，RESOLVED。如无委托则为空    
    * - PRIORITY_
      - 优先级别，默认为：50          
    * - CREATE_TIME_
      -  
    * - DUE_DATE_
      - 耗时   
    * - CATEGORY_
      -           
    * - SUSPENSION_STATE_
      - 挂起状态，1代表激活 2代表挂起 
    * - TENANT_ID_
      -  
    * - FORM_KEY_
      -  

.. list-table:: ACT_RU_IDENTITYLINK

    * - 字段名 
      - 字段描述      
    * - ID_
      -    
    * - REV_
      -     
    * - GROUP_ID_
      -           
    * - TYPE_
      - 用户组类型，主要分为以下几种：assignee、candidate、owner、starter、participant。即：受让人、候选人、所有者、发起人、参与者 
    * - USER_ID_
      -    
    * - TASK_ID_
      -     
    * - PROC_INST_ID_
      -           
    * - PROC_DEF_ID_
      -  
    

.. list-table:: ACT_RU_VARIABLE

    * - 字段名 
      - 字段描述      
    * - ID_
      -    
    * - REV_
      -     
    * - TYPE_
      - 编码类型，参见VAR_TYPE_类型说明          
    * - NAME_
      - 变量名称 
    * - EXECUTION_ID_
      -    
    * - PROC_INST_ID_
      -     
    * - TASK_ID_
      -           
    * - BYTEARRAY_ID_
      -  
    * - DOUBLE_
      -    
    * - LONG_
      -     
    * - TEXT_
      - 存储变量值类型为String，如此处存储持久化对象时，值jpa对象的class          
    * - TEXT2_
      - 此处存储的是JPA持久化对象时，才会有值。此值为对象ID 


.. list-table:: ACT_RU_EVENT_SUBSCR

    * - 字段名 
      - 字段描述      
    * - ID_
      -    
    * - REV_
      -     
    * - EVENT_TYPE_
      -           
    * - EVENT_NAME_
      -  
    * - EXECUTION_ID_
      -    
    * - PROC_INST_ID_
      -     
    * - ACTIVITY_ID_
      -           
    * - CONFIGURATION_
      -  
    * - CREATED_
      -    
    * - PROC_DEF_ID_
      -     
    * - TENANT_ID_
      -           


.. list-table:: ACT_EVT_LOG

    * - 字段名 
      - 字段描述      
    * - LOG_NR_
      -    
    * - TYPE_
      -     
    * - PROC_DEF_ID_
      -           
    * - PROC_INST_ID_
      -  
    * - EXECUTION_ID_
      -    
    * - TASK_ID_
      -     
    * - TIME_STAMP_
      -           
    * - USER_ID_
      -  
    * - DATA_
      -    
    * - LOCK_OWNER_
      -     
    * - LOCK_TIME_
      -           
    * - IS_PROCESSED_
      -   

=================================
历史表
=================================

.. list-table:: ACT_HI_PROCINST

    * - 字段名 
      - 字段描述      
    * - ID_
      -    
    * - PROC_INST_ID_
      -     
    * - BUSINESS_KEY_
      -           
    * - PROC_DEF_ID_
      -  
    * - START_TIME_
      -    
    * - END_TIME_
      -     
    * - DURATION_
      -           
    * - START_USER_ID_
      - 发起人 
    * - START_ACT_ID_
      - 开始节点   
    * - END_ACT_ID_
      - 结束节点    
    * - SUPER_PROCESS_INSTANCE_ID_
      - 超级流程实例          
    * - DELETE_REASON_
      - 删除理由  
    * - TENANT_ID_
      -   
    * - NAME_
      -   


.. list-table:: ACT_HI_ACTINST

    * - 字段名 
      - 字段描述      
    * - ID_
      -    
    * - PROC_DEF_ID_
      -     
    * - PROC_INST_ID_
      -           
    * - EXECUTION_ID_
      -  
    * - ACT_ID_
      - 节点    
    * - TASK_ID_
      -     
    * - CALL_PROC_INST_ID_
      - 请求流程实例          
    * - ACT_NAME_
      - 节点名称 
    * - ACT_TYPE_
      - 节点类型 ，如startEvent、userTask  
    * - ASSIGNEE_
      - 节点签收人    
    * - START_TIME_
      -           
    * - END_TIME_
      -   
    * - DURATION_
      - 时长，耗时  
    * - TENANT_ID_
      -

.. list-table:: ACT_HI_TASKINST

    * - 字段名 
      - 字段描述      
    * - ID_
      -    
    * - PROC_DEF_ID_
      -     
    * - PROC_INST_ID_
      -           
    * - EXECUTION_ID_
      -  
    * - TASK_DEF_KEY_
      -    
    * - NAME_
      -     
    * - PARENT_TASK_ID_
      -           
    * - DESCRIPTION_
      -  
    * - OWNER_
      - 实际签收人，任务的拥有者，签收人（默认为空，只有在委托时才有值）   
    * - ASSIGNEE_
      - 代理人，签收人或被委托    
    * - START_TIME_
      -           
    * - END_TIME_
      -   
    * - CLAIM_TIME_
      -   
    * - DURATION_
      -
    * - DELETE_REASON_
      -     
    * - PRIORITY_
      -           
    * - DUE_DATE_
      -   
    * - FORM_KEY_
      - desinger节点定义的form_key属性  
    * - CATEGORY_
      -
    * - TENANT_ID_
      - 多租户通常是在软件需要为多个不同组织服务时产生的概念

.. list-table:: ACT_HI_VARINST

    * - 字段名 
      - 字段描述      
    * - ID_
      -    
    * - PROC_DEF_ID_
      -     
    * - PROC_INST_ID_
      -           
    * - TASK_ID_
      -  
    * - NAME_
      -    
    * - VAR_TYPE_
      -     
    * - REV_
      -           
    * - BYTEARRAY_ID_
      -  
    * - DOUBLE_
      -    
    * - LONG_
      -     
    * - TEXT_
      -           
    * - TEXT2_
      -   
    * - CREATE_TIME_
      -   
    * - LAST_UPDATED_TIME_
      -


.. list-table:: ACT_HI_DETAIL

    * - 字段名 
      - 字段描述      
    * - ID_
      -    
    * - TYPE_
      -  
    * - PROC_DEF_ID_
      -     
    * - PROC_INST_ID_
      -           
    * - TASK_ID_
      -  
    * - ACT_INST_ID_
      - ACT_HI_ACTINST表的ID
    * - NAME_
      -    
    * - VAR_TYPE_
      - 变量类型，    
    * - REV_
      -     
    * - TIME_
      -       
    * - BYTEARRAY_ID_
      -  
    * - DOUBLE_
      -    
    * - LONG_
      -     
    * - TEXT_
      -           
    * - TEXT2_
      - 此处存储的是JPA持久化对象时，才会有值。此值为对象ID 


.. list-table:: ACT_HI_COMMENT

    * - 字段名 
      - 字段描述      
    * - ID_
      -    
    * - TYPE_
      - 类型：event（事件），comment（意见） 
    * - TIME_
      -      
    * - USER_ID_
      -     
    * - TASK_ID_
      -           
    * - PROC_INST_ID_
      -  
    * - ACTION_
      - 值为下列内容中的一种：　　　　AddUserLink、DeleteUserLink、AddGroupLink、DeleteGroupLink、AddComment、AddAttachment、DeleteAttachmen   
    * - MESSAGE_
      - 处理意见，用于存放流程产生的信息，比如审批意见    
    * - FULL_MSG_
      - 全部消息    
  
.. list-table:: ACT_HI_ATTACHMENT

    * - 字段名 
      - 字段描述      
    * - ID_
      -    
    * - REV_
      -  
    * - USER_ID_
      -      
    * - NAME_
      -     
    * - DESCRIPTION_
      -           
    * - TYPE_
      -  
    * - TASK_ID_
      -    
    * - PROC_INST_ID_
      -     
    * - URL_
      - 附件地址    
    * - CONTENT_ID_
      - 内容ID或字节表ID     
    * - TIME_
      -   
           

.. list-table:: ACT_HI_IDENTITYLINK

    * - 字段名 
      - 字段描述      
    * - ID_
      -    
    * - GROUP_ID_
      -  
    * - TYPE_
      - 类型，主要分为以下几种：assignee、candidate、owner、starter 、participant     
    * - USER_ID_
      -     
    * - TASK_ID_
      -           
    * - PROC_INST_ID_
      -  
   

========================
身份
========================
   
.. list-table:: ACT_ID_GROUP

    * - 字段名 
      - 字段描述      
    * - ID_
      -    
    * - REV_
      -  
    * - NAME_
      -      
    * - TYPE_
      -     

.. list-table:: ACT_ID_MEMBERSHIP

    * - 字段名 
      - 字段描述      
    * - USER_ID_
      -    
    * - GROUP_ID_
      -  
    
.. list-table:: ACT_ID_USER

    * - 字段名 
      - 字段描述      
    * - ID_
      -    
    * - REV_
      -  
    * - FIRST_
      -      
    * - LAST_
      -   
    * - EMAIL_
      -  
    * - PWD_
      -      
    * - PICTURE_ID_
      -     
  

.. list-table:: ACT_ID_INFO

    * - 字段名 
      - 字段描述      
    * - ID_
      -    
    * - REV_
      -  
    * - USER_ID_
      -      
    * - TYPE_
      -      
    * - KEY_
      - formInput名称
    * - VALUE_
      -      
    * - PASSWORD_
      -      
    * - PARENT_ID_
      -   

*********************************************
对象关系
*********************************************

============================
ProcessInstance
============================

通过runtimeService.startProcessInstance()方法启动，引擎会创建一个流程实例（ProcessInstance）。
简单来说流程实例就是根据一次（一条）业务数据用流程驱动的入口，两者之间是一对一的关系。流程引擎会创建一条数据到ACT_RU_EXECUTION表，同时也会根据history的级别决定是否查询相同的历史数据到ACT_HI_PROCINST表。 
启动完流程之后业务和流程已经建立了关联关系，第一步结束。

启动流程和业务关联区别： 

1. 对于自定义表单来说启动的时候会传入businessKey作为业务和流程的关联属性
2. 对于动态表单来说不需要使用businessKey关联，因为所有的数据都保存在引擎的表中
3. 对于外部表单来说businessKey是可选的，但是一般不会为空，和自定义表单类似

=======================
Execution
=======================

对于初学者来说，最难理解的地方就是ProcessInstance与Execution之间的关系，要分两种情况说明。Execution的含义就是一个流程实例（ProcessInstance）具体要执行的过程对象。
不过在说明之前先声明两者的对象映射关系：ProcessInstance（1）→ Execution(N)，（其中N>=1）。 

1. 值相等的情况：

    除了在流程中启动的子流程之外，流程启动之后在表ACT_RU_EXECUTION中的字段ID_和PROC_INST_ID_字段值是相同的。 

2. 值不相等的情况：

    不相等的情况目前只会出现在子流程中（包含：嵌套、引入），例如一个购物流程中除了下单、出库节点之外可能还有一个付款子流程，在实际企业应用中付款流程通常是作为公用的，所以使用子流程作为主流程（购物流程）的一部分。


======================
Task 
======================

前面说了ProcessInstance和业务是一对一关联的，和业务数据最亲密；而Task则和用户最亲密的（UserTask），用户每天的待办事项就是一个个的Task对象。 

Execution和Task是一对一关系，Task可以是任何类型的Task实现，可以是用户任务（UserTask）、Java服务（JavaServiceTask）等，在实际流程运行中只不过面向对象不同，用户任务(UserTask)需要有人为参与完成（complete），Java服务需要由系统自动执行（execution）。

Task是在流程定义中看到的最大单位，每当一个Task完成的时候引擎会把当前的任务移动到历史中，然后插入下一个任务插入到表ACT_RU_TASK中。结合请假流程来说就是让用户点击“完成”按钮提交当前任务是的动作，引擎自动根据任务的顺序流或者排他分支判断走向。

======================
HistoryActivity
======================

Activity包含了流程中所有的活动数据，例如开始事件、各种分支（排他分支、并行分支等）、以及刚刚提到的Task执行记录。
 

有些人认为Activity和Task是多对一关系，其实不是。
 

结合请假流程来说，如Task中提到的当完成流程的时候所有下一步要执行的任务（包括各种分支）都会创建一个Activity记录到数据库中。例如领导审核节点点击“同意”按钮就会流转到人事审批节点，如果“驳回”那就流转到调整请假内容节点，每一次操作的Task背后实际记录更详细的活动（Activity）。

.. uml:: 

   Alice -> Bob: Hi!
   Alice <- Bob: How are you?