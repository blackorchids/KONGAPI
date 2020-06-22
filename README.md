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
	Update service
	- curl http://127.0.0.1:8001/services/httpbin -XPATCH -d name=app | jq
	
	Add Route
	- curl http://127.0.0.1:8001/services/httpbin/routes -d path[]=/
