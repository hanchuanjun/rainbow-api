本文档中规定，除非特殊说明：
1. 定义的接口采用RESTful风格；
2. 请求和回应数据的内容为JSON格式，编码方式统一采用UTF-8。
3. URL中带$的字符串为变量，例如：
	$APISERVER：API服务器主机名，本文档中均为api.c.inhandnetworks.com或api.g.inhandnetworks.com。
	$AUTHSERVER：授权服务器主机名，本文档中均为auth.c.inhandnetworks.com或auth.g.inhandnetworks.com。
	$XXX：参数
4. 时间（创建、更新、登录、退出等）均采用4字节整数，表示从CUT（Coordinated Universal Time）时间1970年1月1日00:00:00（称为UNIX系统的Epoch时间）到当前时刻的秒数（10位）。
5. 所有对单个指定资源操作的接口，如果资源不存在，则返回结果为资源不存在的错误信息。
6. 变量命名定义：URL参数中的所有变量，均采用小写字母，单词间以下划线分隔的方式命名。请求消息内容（http的body体、返回结果或消息队列中的消息体）中的变量，均采用JAVA中局部变量的命名方式，即：变量中第一个单词首字母小写，其他单词首字母大写，单词间无分隔符。
7. 所有接口中，请求消息内容以及返回结果中的”$变量名”表示该章节中定义的对应的数据结构体，一般为JSON对象。如“$UserInfo”表示用户管理接口定义一章中的小节“用户信息数据结构定义”中定义的用户信息JSON对象格式。
8. 每一章中的数据结构定义中的字段说明，若字段有“创建/更新时忽略请求中的该项参数”，则表示该字段在创建或更新资源接口的请求消息内容中不携带。如用户管理接口一章中的用户信息数据结构定义中的“oid”字段，在创建用户和更新用户信息接口中的请求消息内容“$UserInfo”中不需携带该字段。
9. 所有接口中的“访问授权限制”中，若“访问级别”为“内部接口”，则表示在URL中需携带“server_token”字段（除oauth2的相关接口外）。
10. 除oauth2的相关接口以及内部接口外，其他接口的访问URL均需携带“access_token”字段。
11. 密码都采用md5加密传输。
12. 系统内部API保留字段：oid_user, uid_user, ip_user, username_user,resourceIds
13. 系统内部API之间的调用：访问地址为API服务所在主机地址和端口，路径为本文档定义的路径。
14. oauth2服务响应的content-type为”application/json”.
15. 采用put方法更新资源时尽量不要携带不需要更新的额外属性，以减少网络负荷。
16. 后端部分需要国际化的部分，需要传入language标识参数，默认2为中文，1为英文，其他语言待定。
17. 主干版本的所有日志代码为7位数字。
