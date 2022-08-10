---
title: filter | Java filter 统计 http 信息
date: 2022-02-22
tags:
---

我是短小精悍的文章摘要(๑•̀ㅂ•́) ✧

<!-- more -->

在这里，我们来编写一个过滤器，来打印 http 请求的相关信息

```java
/**
 * description: CommonFilter <br>
 * date: 2022/2/21 下午4:25 <br>
 * author: ngsh <br>
 * version: 1.0 <br>
 */


@WebFilter( "/")
@Component
public class CommonFilter implements Filter {

    public String uuid;

    private final Log log = LogFactory.getLog(CommonFilter.class);

    private final String[] filterList = {
            "/doc.html.*",
            "/webjars.*",
            "/swagger-resources.*",
            "/v2.*",
            "/swagger.*"
    };


    @Override
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        HttpServletRequest req = (HttpServletRequest) request;
        HttpServletResponse resp = (HttpServletResponse) response;


        String url = req.getRequestURL().toString();
        String uri = req.getRequestURI();
        String clientIp=req.getRemoteAddr();//获取客户端的ip
        Integer clientPort=req.getRemotePort(); //获取客户端的端口号
        String serverName=req.getRemoteHost();//获取远程计算机的名字
        String  ua  =   req.getHeader("User-Agent");

        String uuid = UUID.randomUUID().toString().substring(0,8);
        this.uuid = uuid;
        boolean isMatch = true;
        for (String pattern : filterList){
            if (Pattern.matches(pattern, uri)){
                isMatch = false;
                break;
            }
        }
        if (isMatch == true){
            ObjectMapper objectMapper = new ObjectMapper();
            Map<String,String> map = objectMapper.readValue(CommonUtils.httpGet("https://www.fkcoder.com/ip?ip="+clientIp,"GET"),Map.class);
            String address = map.get("country") + "," + map.get("province") + "," + map.get("city") + "," + map.get("isp");

            req.setAttribute("uuid",uuid);
            req.setAttribute("startTime",System.currentTimeMillis());

            log.info(String.format("[-][%s] === 请求开始",uuid));
            log.info(String.format("[-][%s] url: %s",uuid,url));
            log.info(String.format("[-][%s] 客户端信息： ip 地址：%s (%s),端口号:%s,计算机名称:%s",uuid,clientIp,address,clientPort,serverName));
            log.info(String.format("[-][%s] User-Agent:%s",uuid,ua));
            chain.doFilter(request, response);

            long startTime = (long) req.getAttribute("startTime");
            long stopTime =  System.currentTimeMillis();
            String uuid1 = (String) req.getAttribute("uuid");

            log.info(String.format("[-][%s] === 请求完成，请求执行时间 %.4f 秒",uuid1,(stopTime-startTime)/1000.0));
        }else {
            chain.doFilter(request, response);
        }
    }

    @Override
    public void destroy() {

    }
}
```

Java

这个过滤器，可以作为一个通用的组件，存在我们的项目中

统计的信息如下：

- 客户端 ip 地址、端口(port)、ua 、请求的url 等等信息
- http 时间 — 请求到响应