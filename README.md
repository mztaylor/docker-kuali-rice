# Docker recipe for Kuali Rice

This instantiates a kuali rice instance.  Current edition is being setup to 
run krad-sampleapp app in standalone mode on mysql however the plan is to make this configurable.



Steps
---

Checkout a copy of mztaylor/docker-mysql (handles lower case table names)

		git clone github.com/mztaylor/docker-mysql.git mysql
        docker build -t mysql .

Build a docker image

        docker build -t ricedemo .

Setup mysql:

	docker run --name mysqlrice -e MYSQL_ROOT_PASSWORD=root -d mysql

Run a docker image:

	docker run --name ricedemo --link mysqlrice:mysql -i -t -p 8080:8080 ricedemo

Review Site

        From browser: http://192.168.59.103:8080/

Remove Instance:

       docker ps -a | grep "ricedemo" | awk '{print $1}' | xargs docker rm
