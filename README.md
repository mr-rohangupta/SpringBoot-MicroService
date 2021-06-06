**Spring Boot Microservice**

**Introduction**

-> **_Spring Boot Microservice have various services like service-registry, cloud-config-server, cloud-gateway,iam-auth-service, hystrix-dashboard, user-service and department-service._**

-> **_Spring Boot Microservice has Eureka as Service registry, cloud-config-server as config server for all the microservices, cloud-gateway which acts as a zuul API gateway, iam-auth-service as the authentication service which uses Oauth2 JWT token to secure all the end points then we have hystrix-dashboard as we will be monitoring hystrix metrics in real time, and also user-service and department-service._**

**Steps to Start Service**

i) **_Clone the repository and resolve the dependency for all the microservices._**

ii) **_Start service-registry then go to browser and hit http://localhost:8761 you will see the eureka dashboard._**

iii) **_Once Eureka is started, start cloud-config-server service and come back to eureka, there you will see that cloud-config-server is also registered with Eureka as all the services will be the client of service-registry which acts as a Eureka Server (@EnableEurekaClient annotation is used to create eureka client)._**

iv) **_Now visit https://zipkin.io/ and download the latest zipkin jar and run that jar using java -jar command._**

v) **_Now start cloud-gateway service (Zuul API gateway service), API gateway as the name defines its the default gateway for all the services with major tasks as maintaining routing details for all the endpoints, configurations for hystrix circuit breaker (fallback methods), hystrix stream, dashboard stuffs and JWT token filtering._**

vi) **_Start hystrix-dashboard service and check its health via http://localhost:9295/hystrix/ and also the stream ping URL using   http://localhost:9191/actuator/hystrix.stream. If you are sucessfully getting the ping response then copy the ping actuator URL and paste it in the http://localhost:9295/hystrix/ URL stream path._**

vii) **_Start iam-auth-service (Service responsible for securing end points using Oauth2 JWT token via generating & validating tokens._**

viii) **_Now start department-service and user-service and see its relevant status in Eureka Dashboard._**

ix) **_Now hit localhost:9191/auth/ and fetch the JWT token. (Token used in passing in all the endpoints)._**

**Generating Bearer Token**

**JWT Token END POINT** : **_http://localhost:9191/auth_**

PayLoad
`{
"userName": "admin",
"password": "12345"
}`

x) **_Firstly create the department and check the created department using its GET API. Then create the user by passing the department id in user payload (Id generated in             response while creating depatment) then you can see the user details using its GET API.
      Note: For all the requests we need to pass the Bearer token in header. (Go to postman in Authorization tab and select type as Bearer Token)_**

**CREATE DEPARTMENT**

**END POINT** : **_http://localhost:9191/department/_**

**METHOD** : **_POST_**

PayLoad
`{
"departmentName" : "IT",
"departmentAddress": "Nelson Street, Byramji Town Road, Nagpur",
"departmentCode": "IT101"
}`

Response
`{
"departmentId": 1,
"departmentName": "IT",
"departmentAddress": "Nelson Street, Byramji Town Road, Nagpur",
"departmentCode": "IT101"
}`

**FETCH DEPARTMENT**

**END POINT** : **_http://localhost:9191/department/1_**

**METHOD** : **_GET_**

Response
`{
"departmentId": 1,
"departmentName": "IT",
"departmentAddress": "Nelson Street, Byramji Town Road, Nagpur",
"departmentCode": "IT101"
}`

**CREATE USER**

**END POINT** : **_http://localhost:9191/users/_**

**METHOD** : **_POST_**

PayLoad
`{
"firstName": "Rohan",
"lastName": "Gupta",
"email": "rohanghanshyamgupta@gmail.com",
"departmentId": "1"
}`

**FETCH USER**

**END POINT** : **_http://localhost:9191/users/1_**

**METHOD** : **_GET_**

Response
`{
"user": {
"userId": 1,
"firstName": "Rohan",
"lastName": "Gupta",
"email": "rohanghanshyamgupta@gmail.com",
"departmentId": "1"
},
"department": {
"departmentId": 1,
"departmentName": "IT",
"departmentAddress": "Nelson Street, Byramji Town Road, Nagpur",
"departmentCode": "IT101"
}
}`

xi) **_Down any one of the service and check whether you are getting the hystrix fallback result or not._**

xii) **_Finally check the zipkin url http://127.0.0.1:9411/zipkin/ and see the logs trace with the help of trace Id._**
