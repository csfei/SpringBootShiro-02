1.什么是权限管理
        
        基本上设计到用户的系统都要进行权限权利，属于系统安全的范畴，
    权限管理实现  对用户访问系统的控制，按照安全规则或者安全策略控制用户可以访问而且只能访问自己被授权的的资源
    
        权限管理包括： 身份认证和授权
        
        对需要访问控制的资源用户首先进行身份认证，认证通过后用户具有该资源的访问权限方可访问
        
2.什么是身份认证？

        身份认证就是判断一个用户是否为合法用户的处理过程
        
3.什么是授权？
       
        授权，就是访问控制，控制谁可以访问那些资源，主体进行身份认证后需要分配系统的权限才可以对系统的资源进行访问， 对于没有权限的资源是无法访问的
        

4.什么是shiro？
        
        shiro是apache 下的的一个开源框架，他将软件系统的安全认证相关的功能抽取出来，实现用户身份认证、权限授权、加密、会话管理等功能 组合成了一个通用的安全认证框架
      是一个强大的Java安全框架，Api 易于理解和使用   
     
        MD5 是一种算法，
            作用：一般是用来加密或者签名（校验和）  签名  的实例  比较两个文件是否一致，就可以考虑用MD5的签名
      
    4.1 shiro 的认证;
        最终执行用户名称的比较  ，是在simpleAccountRealm类中的doGetAuthenticatiationInfo 方法完成用户名称校验
        最终密码校验是在AuthenticatingRealm类中的assertCredentialsMatch 方法中进行校验
        
        
        
    4.2 shiro 的授权
    
        可以简单的理解为  主体（subject）  对资源（Resources）的操作许可（Permission）
        
        授权方式：
            a.基于角色的访问控制
            
                if(subject.hasRole('admin')){
                    //操作什么资源
                }
            b.基于资源的访问控制
                if(subject.isPermission('user:*:find')){
                    //对所有用户具有查询权限
                }
            
            
         权限字符串：
            规则：
                资源标识符：操作：资源实例标识符  
                    意思是对哪个资源的哪个实例具有什么操作， ':' 是分割符号  权限字符串也可以使用*通配符
                    
                    例子：
                        用户创建权限： user:create,或者 user:create:*
                        用户修改实例001的权限：  user:update:001
                        用户实例001的所有权限：  user:*:001
                        
 5.shiro 中的授权编程实现方式
        
        编程式：
                 Subject   subject = SecurityUtils.getSubject();
                 if(subject.hasRole('admin') ){
                       //有权限
                 } 
        注解式：
                @RequiresRoles('admin')
                public void hello(){
                    //有权限
                }  
        
        标签式：
                
                JSP页面 通过相应的标签完成：
                    <shiro:hasRole name='admin'>
                        <!-有权限->
                    </shiro:hasRole>              
                    
         注意的是：
                Thymeleaf 中使用shiro 需要集成      
                
                
        git@github.com:csfei/SpringBootShiro-02.git 