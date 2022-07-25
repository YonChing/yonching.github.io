###############################
角色工程
###############################

*******************************
RBAC模型
*******************************

基本规则：

1. Role assignment: a user can access a permission only if the user has been assigned a role.
2. Role authorization: a user’s active role must be authorized for this user.
3. Permission authorization: a user can access a permission only if the permission
is authorized for the user’s active role.

附加控制：

1. Separation of duty (SoD): 权限互斥
2. 一个角色包含的用户数量限制
3. 不同系统在不同时间所拥有的权限不同
