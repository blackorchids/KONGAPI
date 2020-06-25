# KONGAPI with curl

	127.0.0.1:8001 = Kong Server
	Basic Expose your services
	- curl http://127.0.0.1:8001/services -d name=httpbin -d url=http://httpbin.org
	- curl http://127.0.0.1:8001/services/httpbin/routes -d path[]=/
	- curl http://127.0.0.1:8001/header
	
# SERVICES	
	Add Service
	- curl http://127.0.0.1:8001/services -d name=httpbin -d url=http://httpbin.org
	List Service
	- curl http://127.0.0.1:8001/services | jq
	- curl http://127.0.0.1:8001/services/httpbin | jq
	Update Service
	- curl http://127.0.0.1:8001/services/httpbin -XPATCH -d name=app | jq
	Delete Service
	- curl http://127.0.0.1:8001/services/app -XDELETE | jq
	
	
# ROUTES
	List Route
	- curl -s http://127.0.0.1:8001/services/app{name,id}/routes | jq 
	- curl -s http://127.0.0.1:8001/routes | jq
	Add Route
	  #set paths only "/"
	- curl http://127.0.0.1:8001/services/httpbin{name,id}/routes -d path[]=/
	  #set hosts only "example.com"
	- curl -s http://127.0.0.1:8001/services/app/routes -d host[]=example.com | jq
	  #set hosts "example.com" and paths "/v1"
	- curl -s http://127.0.0.1:8001/services/app/routes -d paths[]=/v1 -d hosts[]=example.com | jq
	  #set multiple paths
	- curl http://127.0.0.1:8001/services/app/routes -d paths[]=/ -d paths[]=/v1 | jq
	  #set multiple hosts
	- curl http://127.0.0.1:8001/services/app/routes -d hosts[]=example.com -d hosts[]=www.example.com | jq
	  #set multiple hosts, paths
	- curl http://127.0.0.1:8001/services/app/routes -d paths[]=/ -d paths[]=/v1 \
	  	-d hosts[]=example.com -d hosts[]=www.example.com | jq
	Update Route
	- curl -s http://127.0.0.1:8001/routes/{id} -XPATCH -d name=example-route | jq
	Delete Route
	- curl -s http://127.0.0.1:8001/services/app/routes/{name,id} -i -XDELETE


# Authentication
	Enable JWT Plugins
	- curl http://127.0.0.1:8001/services -d name=httpbin -d url=http://httpbin.org | jq
	- curl http://127.0.0.1:8001/services/httpbin/routes -d paths[]=/ | jq
	- curl -s http://127.0.0.1:8001/services/httpbin/plugins -d name=jwt | jq
	- curl -w "\n" -s http://127.0.0.1 -i
	- curl -s http://127.0.0.1:8001/consumers/kong/jwt -XPOST | jq
	- curl -s http://127.0.0.1:8001/consumers -d username=kong | jq
	- curl -s http://127.0.0.1:8001/consumers/kong/jwt -XPOST | jq
	JWT.io Debugger for finding Bearer
		https://jwt.io/
	- curl -w "\n" -s http://127.0.0.1/headers -i -H 'Authorization: Bearer xxxxxxx'
