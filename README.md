**Spring Boot Microservice** 

**Introduction** 

-> **_Spring Boot Microservice have various services like service-registry, cloud-config-server, cloud-gateway, hystrix-dashboard, user-service and department-service._**
    
-> **_Spring Boot Microservice has used Eureka as Service registry, cloud-config-server which is the config server for all the microservices, cloud-gateway which acts as a API gateway,
        hystrix-dashboard as we will be monitoring hystrix metrics in real time, then we have user-service and department-service._**

**Steps to Start Service**

i) **_Clone the repository and resolve the dependency for all the microservices._**

ii) **_Start service-registry then go to browser and hit http://localhost:8761 you will see the eureka dashboard._**

iii) **_Once Eureka is started start cloud-config-server service and come back to eureka & you will see that cloud-config-server is also registered with Eureka as we had used @EnableEurekaClient annotation._**

iv) **_Now go to https://zipkin.io/ and download the zipkin jar and run that jar using java -jar command._**

v) **_Now start cloud-gateway service which is your API gateway service, here in this service you can see the routes of the API's and also the configurations for hystrix fallback methods and hystrix stream and dashboard stuffs._**

vi) **_Start hystrix-dashboard service and check the endpoint http://localhost:9295/hystrix/ and also the stream ping URL http://localhost:9191/actuator/hystrix.stream. If you are getting the ping then copy the ping actuator URL and paste it in the http://localhost:9295/hystrix/ URL stream path._**

vii) **_Now start department service and user service and see the status in Eureka._**

viii) **_Firstly create the department and check the get API result of it. Then create the user with user json and the department id and then get the user details by get API._**

ix) **_Down any one of the service and check whether you are getting the hystrix fallback result or not._**

x) **_Finally check the zipkin url http://127.0.0.1:9411/zipkin/ and see the logs trace with the help of trace Id._**
