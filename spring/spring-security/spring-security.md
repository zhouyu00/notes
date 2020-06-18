# 10.Authentication

#### Architecture Components

* SecurityContextHolder
* SecurityContext
* Authentication
* GrantedAuthority
* AuthenticationManager
* ProviderManager
* AuthencationProvider
* Request Credentials with AuthenticationEntryPoint
* AbstractAuthenticationProcessingFilter



## 10.1 SecurityContextHolder



## 10.2 SecurityContext



## 10.3 Authentication

Authentication 具有两个功能：

* AuthenticationManager 输入用来验证用户提供的凭证
* 代表当前认证用户

Authentication 包含：

* principal -用户identify
* credentials- 通常是密码
* authorities- GrantedAuthority 用户被颁发的高等级允许 通常就是角色



## 10.4 GrantedAuthority



## 10.5 AuthenticationManager



## 10.6 ProviderManager

