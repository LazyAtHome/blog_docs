## Coding Rule

### File Encoding
	UTF-8

### Members in Class
* Comments for Source
* Package Declaration
* Imports
* Comments for Class
* Class Declaration
* Static Fields
* Dynamic Fields
* **Static Block**
* Constructors
* Static methods
* biz methods
* setters/getters

### Naming
* Naming for projects
	> lowercase or uppercase
* Naming for modules
	> `org.eclipse.samples`

* Naming for folders/packages
	> `org.springframework.orm.suport`
	> 
	> pack by layer or by module
* Naming for classes
	> `NameOfClass`
	> 
	> Convention: Prefix or Postfix
	> 
	> IUserService, UserService
	> 
	> UserService, UserServiceImpl
	> 
	> Listener, Servlet, Action, Service, Dao, Job, Factory, Wrapper
* Naming for methods
	> `public List findByName(String name) {......}`
	> 
	> `findById()` ---> `queryById()`
	> 
	> biz logic method can't named as getXX setXX 
* Naming for fields
	> `private int intVar;`
	> 
	> `public static final int MAX_SIZE = 1000;`



### Comments Style
* Comments for source file
	> /**
	>  *
	>  */
	> Copy Right
	> 
	> License
* Comments for Classes
	> @author
	> 
	> date
	> 
	> description
* Comments for methods
	> @author
	> 
	> date
	> 
	> description
	> 
	> @param
	> 
	> @return
	> 
* Comments for fields
	> should have not comments for fields
* Comments for logic statements
	> 
	
### Coding Formatter
	Export a preference

### Conventions
* Remove all of unused statements, fields and local variables
* Remove all of commented-out lines
* Octal values should not be used
	`int myNumber = 010;`
* 