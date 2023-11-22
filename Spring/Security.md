`필터`

  - ![filter](https://github.com/pnci1029/TIL/assets/81909140/bc1e1583-0521-4577-863c-b3c1192bcfa2)

```
@Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {

        HttpServletRequest request = (HttpServletRequest) servletRequest;
        HttpServletResponse response = (HttpServletResponse) servletResponse;

        if (!loginUrl.equals(request.getRequestURI())) {
            throw new UnknownHostException("url error");
        }
        String tokenValue = request.getHeader("Authorization");
        if (tokenValue.startsWith("Bearer ")) {
            String userInfo = tokenValue.split("Bearer ")[1];
            String[] datas = Arrays.toString(Base64.getDecoder().decode(userInfo)).split(":");
            String requestUserInfo = datas[0];
            String requestUserPassword = datas[1];

            if (requestUserInfo.equals(userName) && requestUserPassword.equals(password)) {
                // TODO: 2023/11/22 ??????
                filterChain.doFilter(servletRequest, servletResponse);
            }
        } else {
            log.warn("로그인 실패");
        }
        filterChain.doFilter(servletRequest, servletResponse);
    }
`필터가 뭔가요?`
```
#  
#  
#  
#  
#  
출처 (https://velog.io/@e1psycongr00/%ED%95%84%ED%84%B0-%EB%8B%A8%EC%9C%84-%ED%85%8C%EC%8A%A4%ED%8A%B8, https://jiwondev.tistory.com/270,
https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-%EC%8B%9C%ED%81%90%EB%A6%AC%ED%8B%B0/dashboard,
https://www.inflearn.com/chats/786858/filter%EB%A5%BC-%EB%93%B1%EB%A1%9D%ED%95%98%EB%8A%94-4%EA%B0%80%EC%A7%80-%EB%B0%A9%EB%B2%95,)
