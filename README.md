# spring-stuff

import javax.servlet.http.HttpServletRequest;
import org.slf4j.MDC;
import org.springframework.web.servlet.handler.HandlerInterceptorAdapter;

public class ApiEndpointInterceptor extends HandlerInterceptorAdapter {
  
  @Override
  public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
    String apiEndpoint = request.getRequestURI();
    MDC.put("apiEndpoint", apiEndpoint);
    request.setAttribute("apiEndpoint", apiEndpoint); // set the apiEndpoint in a request attribute
    return true;
  }
  
  @Override
  public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
    MDC.remove("apiEndpoint");
  }
  
}
