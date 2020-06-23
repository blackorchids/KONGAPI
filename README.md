# KONGAPI

	127.0.0.1:8001 = Kong Server
	Basic Expose your services
	- curl http://127.0.0.1:8001/services -d name=httpbin -d url=http://httpbin.org
	- curl http://127.0.0.1:8001/services/httpbin/routes -d path[]=/
	- curl http://127.0.0.1:8001/header
	
	
	Add Service
	- curl http://127.0.0.1:8001/services -d name=httpbin -d url=http://httpbin.org
	List Service
	- curl http://127.0.0.1:8001/services | jq
	- curl http://127.0.0.1:8001/services/httpbin | jq
	Update Service
	- curl http://127.0.0.1:8001/services/httpbin -XPATCH -d name=app | jq
	Delete Service
	- curl http://127.0.0.1:8001/services/app -XDELETE | jq
	
	
	
	List Route
	- curl -s http://127.0.0.1:8001/services/app{name,id}/routes | jq 
	- curl -s http://127.0.0.1:8001/routes | jq
	Add Route
	  #set paths only "/"
	- curl http://127.0.0.1:8001/services/httpbin{name,id}/routes -d path[]=/
	Delete Route
	- curl -s http://127.0.0.1:8001/services/app/routes/{name,id} -i -XDELETE
