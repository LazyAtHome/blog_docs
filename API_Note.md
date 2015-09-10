##Project Model
BASE
API(WEB) (Service, Restful controller, DAO) (User, Post)


##Package Naming
```
come.laodaojia.blog.dao.
come.laodaojia.blog.web.controller
```


blog-common
blog-service


db design

```
b_user
id,
username,
email,
crypted_password,
role,
version,
deleted_flag,
created_date,
updated_date,
created_by,
updated_by
```


b_post

```
id,
title,
content,
user_id,
view_count,
version,
deleted_flag,
created_date,
updated_date,
created_by,
updated_by,
```

id as Long type

##API design


```
http://127.0.0.1:8080/
/users/login
/users/logout

/blogs/(create,update,delete,id)

/blogs (create,post request)
/blogs/all (?page=xx&limited=xx  pagination, get request)
/blogs/{id} (get a post, get request)
/blogs/{id} (update, put request)
/blogs/{id} (delete, delete request)
```

###Generate API Doc

Spring MVC,
[spring-restdocs](https://github.com/spring-projects/spring-restdocs)


###How to handle error
```
{
	code:2234
	data: {}
}
```

```
{
	user: { username : '', password : ''}
}
```

httpd status 200

```
{
  error: ""
  .. 
}
```

###Topic to discuss

####Need to support I18N
*How to support I18N*
Use DB to store I18N or properties files,

####Configuration file
*How to handle configuration file?*
different configuration file for different environment
mutiple server need to sync the configuration files.
(Use linux sync? nas, file sharing)

####Scalability
*Netty*
 



